# Add New Data Warehouse

### Step by Step guide for adding your own Redshift Data warehouse to your DataChannel Account

Step 3: Select _Redshift_ from the listed Warehouse options.

Step 4: Click on 'Add Warehouse details.'

Step 5: Enter the details for your **AWS Redshift and S3 Bucket** in the form and click on Validate Configuration to add the warehouse.&#x20;

#### Adding AWS Redshift Details

**Name:** Provide a name for your warehouse. It needs to be unique across your account.

**Host:** Provide the hostname or end-point for the cluster.

**Username:** Provide a username which will be used to create the tables and load data. This user needs to have all rights on the schema that you intend to use. In case you are creating a dedicated schema for the data from DataChannel (which is recommended), then this user can be the schema owner.

**Password:** Provide the password for the load user.

**DB Users:** Comma separated list of users who should get select rights on tables created by DataChannel using the schema and username specified by you.

**Port:** Provide the port number for your cluster. The default value for this is 5439 unless you have changed it while creating your redshift cluster.

**DB Name:** Provide the name of the database you have created in your cluster.

**Schema Name:** Provide the database schema where DataChannel should push the data. As mentioned above, it is recommended to create a new schema for DataChannel in your database.

#### Adding S3 Bucket Details

**AWS Location:** Provide the AWS region where your S3 bucket has been created. This should typically be same as the region in which your Redshift cluster is hosted. Example `us-east-1`

**Bucket Name:** Provide name of the S3 bucket where DataChannel should copy files before loading them into your Redshift instance. Note that DataChannel does not remove the files after they have been copied into Redshift so it is advisable to use life cycle properties to manage the removal / archival of the raw files to manage S3 costs.

**Access Key:** Provide the access key required to access the S3 bucket using the API. Refer AWS documentation [here](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) to learn how to manage your access keys.

**Secret Key:** Provide the secret key required to access the S3 bucket using the API. Refer AWS documentation [here](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) to learn how to manage your secret keys.

**IAM Role:** Provide the IAM role required to access the S3 bucket using the API. Refer AWS documentation [here](https://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-create-an-iam-role.html) to learn how to create and manage your IAM Role.

