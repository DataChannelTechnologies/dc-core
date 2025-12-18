# Azure Synapse Analytics

This guide helps you configure a connection to Azure Synapse Analytics so you can securely query and ingest data from your Synapse workspace into DataChannel. It explains all required fields, authentication details, and Azure Blob Storage settings used for data staging.

### ✍️ Getting Started <a href="#getting-started" id="getting-started"></a>

To set up an Azure Synapse Analytics warehouse in DataChannel, you’ll need:

* Your Synapse SQL server host
* Target database and schema
* Username and password for authentication
* Azure Blob Storage account details for data staging

### 🛠 Connection Details <a href="#connection-details" id="connection-details"></a>

Here’s a breakdown of what each field means and how to fill it:

**1. Name**

Choose a unique name to identify this Synapse warehouse within DataChannel.

This helps you distinguish it later when managing multiple warehouses.

Examples: synapse-prod, azure-datawarehouse, marketing-synapse

> ⚠️ This name must be **unique** across all your sources.

**2. Host**

Enter the fully qualified domain name (FQDN) of your Azure Synapse SQL server.

Example: your-synapse.sql.azuresynapse.net

This value can be found in the Azure portal under your Synapse workspace → SQL pools.

**4. Database**

Specify the name of the SQL pool (database) you want to connect to.

Example: synapse\_sql\_pool, analytics\_dw

Ensure this database exists and is accessible to the provided user.

**5. Schema**

The default schema to use within the selected database. Example: _dbo, marketing, events_

All queries and data operations will run within this schema by default.

### 🔐 Authentication Options <a href="#authentication-options" id="authentication-options"></a>

Azure Synapse Analytics currently supports **Standard Username & Password authentication** in DataChannel.

#### **✅ Standard Authentication**

Use this option if your Synapse SQL pool is accessed using a SQL username and password.

You’ll need to provide:

**Username**

The login username for your Synapse SQL pool

Example: data\_reader, synapse\_admin

**Password**

The password associated with the user

This value is securely masked in the UI.

{% hint style="info" %}
🔐 Ensure that this user has sufficient permissions to access the specified database and schema.
{% endhint %}

#### ☁️ Azure Blob Storage (Required)

Azure Synapse uses **Azure Blob Storage** for data staging operations such as loading and unloading data. DataChannel requires these details to perform data movement efficiently.

You’ll need to configure the following:

**Account Name**

The name of your Azure Blob Storage account.

Example: datastorageaccount

**Account Key**

The access key for the Blob Storage account.

This value is securely masked in the UI.

**Endpoint Suffix**

The endpoint suffix for your storage account.

Default value: core.windows.net

Only change this if you’re using a custom or sovereign cloud environment.

**Container Name**

The name of the Blob Storage container used for staging data.

Example: synapse-staging, datacontainer

Make sure the container exists and the provided account key has read and write access.

***

### ✅ Final Notes

* Verify that all required fields are filled in before saving the warehouse configuration.
* The Synapse user must have access to both the database schema and external data operations.
* Azure Blob Storage permissions are critical for successful data ingestion and querying.

Once configured, DataChannel will validate the connection and make your Azure Synapse Analytics warehouse available for querying and data workflows.
