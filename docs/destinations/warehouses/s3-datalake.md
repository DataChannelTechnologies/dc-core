# S3 Datalake

You can use your own Amazon S3 bucket as a data lake destination in DataChannel. Data is stored as **Apache Iceberg** tables registered in the **AWS Glue Data Catalog** and written through **Amazon Athena**, so the tables can be queried right away from Athena or any other Iceberg-compatible engine (Spark, Trino, EMR, Snowflake, Redshift Spectrum and others).

This guide walks you through the details needed to connect and the AWS setup DataChannel requires.

#### ✍️ Getting Started

To connect S3 Data Lake, you'll need:

* An **S3 bucket** where the table data will be stored
* An **AWS Glue database** in the same region as the bucket
* **Amazon Athena** set up in that region, with the `primary` workgroup able to run queries
* An **IAM role** that DataChannel can assume, with access to S3, Glue and Athena

#### 🛠 Connection Details

Below are the details required to configure an S3 Data Lake connection.

**1. Name**

Choose a unique name for this S3 Data Lake destination. This helps you identify it later if you have several data lake or warehouse connections.

> Examples:\
> prod-s3-lake\
> marketing-iceberg-lake

{% hint style="warning" %}
The name **must be unique** for each destination you add.
{% endhint %}

**2. Glue Database**

Enter the name of the AWS Glue database where DataChannel will register its tables.

> Example: _analytics\_lake_

{% hint style="warning" %}
The Glue database must already exist. DataChannel does not create it. Only letters, numbers and underscores are allowed.
{% endhint %}

To create one, go to **AWS Glue → Data Catalog → Databases → Add database**, or run this in Athena:

```sql
CREATE DATABASE analytics_lake;
```

**3. AWS Region**

The AWS region where your S3 bucket, Glue database and Athena are located.\
Default: **us-east-1**

{% hint style="info" %}
The bucket, the Glue database and Athena must all be in this region.
{% endhint %}

**4. S3 Bucket Name**

The name of the S3 bucket where DataChannel will store the table data. Enter only the bucket name, without `s3://`.

> Example: _acme-data-lake_

Each table is stored under its own folder in the bucket:

```
s3://<bucket>/<table_name>/          ← Iceberg table data and metadata
s3://<bucket>/_staging/              ← temporary load files (cleaned up automatically)
```

#### 🔐 Authentication: IAM Role (Assume Role)

DataChannel connects to your AWS account by assuming an IAM role you create. No access keys are stored. DataChannel receives short-lived credentials that are refreshed automatically.

You'll need:

* **Role ARN**: The Amazon Resource Name (ARN) of the IAM role to assume

> Example: _arn:aws:iam::123456789012:role/DataChannelS3DataLakeRole_

**🔧 Step 1: Set Up the Trust Relationship**

To allow DataChannel to assume your IAM role, configure its trust relationship.

**Steps:**

1. Go to **IAM → Roles → \[your IAM role] → Trust relationships**
2. Click **Edit trust policy** and paste the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::556040221475:user/dc-assume-role-user"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

**🔧 Step 2: Grant Permissions to the Role**

Attach a permissions policy to the role. Replace `<bucket>`, `<region>`, `<account_id>` and `<glue_database>` with your values.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "gluePermissions",
            "Effect": "Allow",
            "Action": [
                "glue:GetDatabase",
                "glue:GetTables",
                "glue:GetTable",
                "glue:CreateTable",
                "glue:UpdateTable",
                "glue:DeleteTable"
            ],
            "Resource": [
                "arn:aws:glue:<region>:<account_id>:catalog",
                "arn:aws:glue:<region>:<account_id>:database/<glue_database>",
                "arn:aws:glue:<region>:<account_id>:table/<glue_database>/*"
            ]
        },
        {
            "Sid": "s3Permissions",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:DeleteObject",
                "s3:GetBucketLocation"
            ],
            "Resource": [
                "arn:aws:s3:::<bucket>",
                "arn:aws:s3:::<bucket>/*"
            ]
        },
        {
            "Sid": "AllowAthenaQueryExecution",
            "Effect": "Allow",
            "Action": [
                "athena:StartQueryExecution",
                "athena:StopQueryExecution",
                "athena:GetQueryExecution",
                "athena:GetQueryResults"
            ],
            "Resource": [
                "arn:aws:athena:<region>:<account_id>:workgroup/primary"
            ]
        },
        {
            "Sid": "AllowAthenaMetadataAccess",
            "Effect": "Allow",
            "Action": [
                "athena:GetTableMetadata",
                "athena:GetDatabase",
                "athena:ListDataCatalogs",
                "athena:ListDatabases",
                "athena:ListTableMetadata"
            ],
            "Resource": [
                "arn:aws:athena:<region>:<account_id>:datacatalog/AwsDataCatalog",
                "arn:aws:athena:<region>:<account_id>:workgroup/primary"
            ]
        },
        {
            "Sid": "AllowListAllBuckets",
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets"
            ],
            "Resource": "*"
        }
    ]
}
```

{% hint style="info" %}
**Athena query results:** DataChannel runs its queries in the `primary` Athena workgroup and uses that workgroup's own settings. Make sure the workgroup has a **query result location** set (or uses Athena managed query results). If the result location is in a different bucket, also give the role `s3:GetObject`, `s3:PutObject` and `s3:ListBucket` on that bucket.
{% endhint %}

#### 📦 How Data Is Loaded

* Tables are created automatically as **Apache Iceberg** tables in your Glue database on the first load.
* **Table and column names are stored in lowercase**, because Glue stores all names in lowercase. Names may contain only letters, numbers and underscores. `_staging` is reserved and cannot be used as a table name.
* **New columns** that appear in your source are added to the table automatically. Existing columns are never removed.
* All three load modes are supported:

| Mode        | Behaviour                                                                |
| ----------- | ------------------------------------------------------------------------ |
| **Append**  | New rows are added to the table.                                         |
| **Replace** | Existing rows are removed, then the new data is loaded.                  |
| **Upsert**  | Rows matching the selected key columns are replaced; new rows are added. |

* Load files are first written to `s3://<bucket>/_staging/` and are removed once the load finishes.

{% hint style="info" %}
Every write creates a new **Iceberg snapshot**. You can query an earlier version of a table in Athena with `FOR VERSION AS OF <snapshot_id>` or `FOR TIMESTAMP AS OF <timestamp>`.
{% endhint %}

{% hint style="warning" %}
Queries run in your AWS account, so Athena query charges and S3/Glue costs are billed to your AWS account.
{% endhint %}

#### ✅ Final Notes

* Make sure all required fields are filled before saving the connection.
* The Glue database must exist before you connect, and the bucket, Glue database and Athena must be in the selected region.
* When you save, DataChannel validates the connection: it checks access to the bucket and the Glue database and runs a test query in Athena. If any check fails, the AWS error is shown so you can fix the role or settings.
* Avoid editing or deleting DataChannel-managed tables and the `_staging/` folder outside DataChannel while loads are running.

Once configured, DataChannel will validate the connection and start loading your data into Iceberg tables you can query from Athena.
