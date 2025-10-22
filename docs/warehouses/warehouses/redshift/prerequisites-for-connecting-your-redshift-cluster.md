# Prerequisites for connecting your Redshift Cluster

* If you don't already have an AWS account, create and activate an AWS account. Set up your data warehouse with AWS Redshift. The AWS Redshift console will allow you to create and manage your Redshift resources.
* Connect to your AWS Redshift as an admin user ( Or any user which has permissions to create databases, users and schemas). Using the AWS Redshift console you can launch query editor v2 by clicking on the Query data button. The query editor v2 connects from your client machine to the AWS Redshift environment. You need to create a database to be used for DataChannel by running this query:

````sql
create database <DATABASE_NAME>;```

Substitute the placeholder in the above query with the desired *Database name*. You may choose any name  for your Database but keep in mind that the Database name should be 1-64 characters. Valid characters are lowercase alphanumeric characters. This database is where DataChannel will actually create tables, load data, and run queries.

If you don’t have access to query editor v2, you can use any database client ( E.g Dbeaver) to connect to your redshift and run the same queries.

* By default, only the admin user that you created when you created your AWS Account has access to the resources that you have created. Thus, to grant DataChannel access to your resources you will need to create a new user. At the time of creating a new DataChannel user, you will need to specify a name  and a password for this new user. The password for the user must have 8–64 characters, and it must include at least one uppercase letter, one lowercase letter, and one numeral. A database comprises one or more schemas which contain tables and other database objects. Schemas help to organize database objects into logical groups so that their management becomes easier. So, on running this query using the Query Editor v2/ your Database Client,  you can connect to this database and create a new user and schema.Substitute the placeholder in the above query with the desired Database name.

```sql
create user <USERNAME> password '<PASSWORD>';
create schema <SCHEMA_NAME> authorization <USERNAME>; # This will create and give ownership of the schema to this user
````

Substitute the placeholders in the above query with the desired _Username_, _password_ and _Schema name_. Please make a note of these as you will require them when configuring your warehouse with DataChannel.

* Ensure that you've created an S3 bucket in your AWS Redshift Warehouse. You can use the following steps to create an Amazon S3 Bucket. 1. Use your AWS account's _email address_ and _password_ to Sign in to your AWS Management Console.
* Open the Console _Home_ page.
* In the Services search Box, search for S3. From the search results, select _S3_. Choose Buckets from the Amazon S3 menu in the left navigation pane and then choose the Create bucket button.
* Enter a _name_ for your bucket.&#x20;
* Select the _AWS Region_ where you would like your bucket to be created.
* You may choose to enable or disable Bucket Versioning.
* Navigate to the bottom of the page and click on Create bucket.
* To grant DataChannel access to your S3 bucket, you will need to create an IAM role with appropriate permissions. Refer AWS documentation [here](https://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-create-an-iam-role.html) to learn how to create and manage your IAM Role.

> Please make a note of the S3 bucket name and region as you will need them later.

{% hint style="info" %}
**Tips**

* It is recommended to create a new schema for DataChannel in your database.
* Ensure that the S3 bucket name and region are correct, as they will be used later during the configuration process.
{% endhint %}
