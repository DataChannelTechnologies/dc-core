# Redshift

You can connect your Amazon Redshift data warehouse to DataChannel by providing a few essential configuration details. This guide walks you through each required setting step by step, including authentication and S3 credentials used for data operations.

### ✍️ Getting Started

To connect Redshift, you'll need:

* Redshift **host**, **port**, **database**, and **schema**
* **Standard Username/Password authentication**
* S3 credentials and location for Redshift data load/unload operations
  * One of two S3 authentication methods:
    * **Access Key Authentication**
    * **IAM Role (Assume Role)**

### 🛠 Connection Details

Below are the details required to configure a Redshift connection.

#### 1. Name

Choose a unique name for this Redshift data warehouse configuration.

This helps you identify the warehouse later if you have multiple Redshift or other data warehouse connections.

> Examples:\
> prod-redshift-west\
> team-finance-redshift

{% hint style="warning" %}
The name **must be unique** for each warehouse you add.
{% endhint %}

#### 2. Host

Enter the hostname of your Redshift cluster.\
It typically looks like:\
redshift-cluster-1.abc123xyz.us-west-2.redshift.amazonaws.com

#### 3. Port

Redshift uses port 5439 by default. Change this only if your Redshift cluster uses a different port.

#### 4. Database

Provide the name of the Redshift database you want to connect to.&#x20;

> Example: _analytics\_db_

#### 5. Schema

Specify the schema inside your database that contains your data.&#x20;

> Example: _public, sales, marketing\_data_

#### 6. Connection Timeout (Optional)

This is the time (in seconds) that the system will wait while trying to connect before giving up. If you're unsure, stick with the default: **60 seconds.**

#### 7. Use Reverse SSH Tunnel (Optional)

Enable this option if your Redshift cluster is not publicly accessible and must be reached through a reverse SSH tunnel.

* Default: _Disabled_

Turn this on only if your infrastructure requires SSH-based access.

### 🔐 Authentication Method

#### **✅** Standard Authentication

Use this method if you connect to Redshift using a database username and password.

You'll need to provide:

* **Username**: Your Redshift database user
* **Password**: The password for that user\
  🔒 The password is securely masked in the UI.

{% hint style="info" %}
Currently, this is the supported authentication method for Redshift connections.
{% endhint %}

### ☁️ S3 Credentials (Required)

Redshift uses Amazon S3 for data operations such as UNLOAD and COPY. DataChannel requires S3 credentials and location details to support these operations.

#### S3 Region

The AWS region where your S3 bucket is located.\
Default: us-east-1

#### S3 Bucket

The name of the S3 bucket used for Redshift data operations.&#x20;

> Example: dc-redshift-staging-bucket

### 🔐 S3 Authentication Method

You must choose one of the following methods to allow DataChannel to access your S3 staging area.

<details>

<summary><code>Option 1</code> Access Key Authentication</summary>

Use this method if you want to provide AWS credentials directly.

You'll need:

* **S3 Access Key**: The AWS access key for the S3 account used by Redshift\
  🔒 This value is securely masked in the UI.
* **S3 Secret Key**: The corresponding AWS secret key\
  🔒 This value is also securely masked.

This method is simple to set up and works well for development or controlled environments. However, it requires managing long-lived credentials.

</details>

<details>

<summary><code>Option 2</code>  IAM Role (Assume Role)</summary>

Use this method if you prefer to authenticate using an IAM role instead of static credentials.

You'll need:

* **Role ARN**: The Amazon Resource Name (ARN) of the IAM role to assume

> Example: _arn:aws:iam::123456789012:role/MyRedshiftRole_

In this setup, DataChannel assumes the specified IAM role to access the S3 bucket. This eliminates the need to store access keys and is generally more secure.

{% hint style="info" %}
Ensure that the IAM role has the necessary permissions to access the specified S3 bucket and perform Redshift data operations.
{% endhint %}

**🔧 Setting Up Trust Relationship for Assume Role**

To allow DataChannel to assume your IAM role, you must configure a trust relationship.

**Steps:**

1. Go to **IAM → Roles → \[your IAM role] → Trust Relationships**
2. Edit the trust relationship policy and attach the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::539123038454:user/dc-assume-role-user"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

</details>

### ✅ Final Notes

* Make sure all required fields are filled before saving the connection.
* S3 credentials are required for Redshift data operations.
* IAM role-based authentication is recommended for improved security and easier credential management.
* Ensure your S3 bucket permissions allow Redshift to load and unload data successfully.

Once configured, DataChannel will validate the connection and make your Redshift data available for querying and analysis.
