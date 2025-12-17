# Redshift

You can connect your Amazon Redshift data warehouse to DataChannel by providing a few essential configuration details. This guide walks you through each required setting step by step, including authentication and S3 credentials used for data operations.

### ✍️ Getting Started

To connect Redshift, you’ll need:

* Redshift **host**, **port**, **database**, and **schema**
* One of two authentication methods:
  * **Standard Username/Password**
  * **IAM-based AWS Credentials**
* S3 credentials and location for Redshift data load/unload operations

### 🛠 Connection Details

Below are the details required to configure a Redshift connection.

**1. Name**

Choose a unique name for this Redshift data warehouse configuration.

This helps you identify the warehouse later if you have multiple Redshift or other data warehouse connections.

Examples:\
prod-redshift-west\
team-finance-redshift

> ⚠️ The name **must be unique** for each warehouse you add.

**2. Host**

Enter the hostname of your Redshift cluster.\
It typically looks like: \
redshift-cluster-1.abc123xyz.us-west-2.redshift.amazonaws.com

**3. Port**

Redshift uses port 5439 by default. Change this only if your Redshift cluster uses a different port.

**4. Database**

Provide the name of the Redshift database you want to connect to. Example: _analytics\_db_

**5. Schema**

Specify the schema inside your database that contains your data. Example: _public, sales, marketing\_data_

**6. Connection Timeout (Optional)**

This is the time (in seconds) that the system will wait while trying to connect before giving up. If you’re unsure, stick with the default: **60 seconds.**

**7. Use Reverse SSH Tunnel (Optional)**

Enable this option if your Redshift cluster is not publicly accessible and must be reached through a reverse SSH tunnel.

* Default: _Disabled_

Turn this on only if your infrastructure requires SSH-based access.

### 🔐 Choose Your Authentication Method

You can authenticate using either:

* Standard Authentication
* IAM Credentials Authentication

Select one based on your setup and security requirements.

#### **✅ Option 1: Standard Authentication**

Use this method if you connect to Redshift using a database username and password.

You’ll need to provide:

* **Username**: Your Redshift database user\
  Example: _readonly\_user_
* **Password**: The password for that user\
  🔒 The password is securely masked in the UI.

#### **🛡️ Option 2: IAM Credentials Authentication**

Use this if you want to authenticate using AWS IAM. This method is recommended for production environments and provides better access control.\
You’ll need:

* **Cluster ID**: The actual Redshift cluster ID—not the host.\
  Example: _redshift-cluster-1_
* **Region**: The AWS region where your Redshift cluster is hosted\
  Example: _us-west-2_
* **Database User:** The database user to connect as  - Default: _awsuser_
* **Access Key ID (Optional):** The AWS access key used for IAM role assumption\
  Will be securely hidden in the UI.
* **Secret Access Key (Optional):** The corresponding secret key\
  Also hidden in the UI for security

> ℹ️ DataChannel assumes an IAM role using these credentials. Ensure the IAM user or role has the required permissions to access Redshift.

### ☁️ S3 Credentials (Required)

Redshift uses Amazon S3 for data operations such as UNLOAD and COPY. DataChannel requires S3 credentials and location details to support these operations.

**1. S3 Region**

The AWS region where your S3 bucket is located.Default: us-east-1

**2. S3 Bucket**

The name of the S3 bucket used for Redshift data operations. Example: dc-redshift-staging-bucket

**3. S3 Access Key**

The AWS access key for the S3 account used by Redshift. This value is securely masked in the UI.

**4. S3 Secret Key**

The corresponding AWS secret key. This value is also securely masked.
