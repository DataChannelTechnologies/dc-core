# Sap Hana

This guide helps you configure a connection to an SAP HANA data warehouse in DataChannel so you can securely query data from your HANA system. You only need a few core connection details and standard login credentials to get started.

### ✍️ Getting Started

To connect to an SAP HANA warehouse, you’ll need:

* SAP HANA host and port
* Target schema
* Standard authentication credentials (username and password)

### 🛠 Connection Details

Below is an explanation of each field and how to fill it correctly.

**1. Name**

Choose a unique name for this SAP HANA warehouse configuration.

This helps you identify the warehouse later when managing multiple warehouses across different systems.

Examples: sap-hana-prod, finance-hana, erp-reporting-hana

{% hint style="info" %}
The name must be unique across all warehouses configured in DataChannel.
{% endhint %}

**2. Host**

Provide the hostname or IP address of your SAP HANA database server.

Examples: hana.company.internal, 10.20.30.40

This should be the address where the HANA SQL service is reachable.

**3. Port**

The port used to connect to the SAP HANA database.

* Default: 30015

This is the standard SQL port for SAP HANA systems. Change it only if your HANA instance is configured to use a different port.

**4. Schema**

Specify the schema you want DataChannel to use for queries.

This schema should already exist and be accessible by the user you authenticate with.

Examples: SYSTEM, SALES, FINANCE\_REPORTING

### 🔐 Authentication Method

SAP HANA connections in DataChannel use Standard Authentication.

#### ✅ Standard Authentication

Use this method if your SAP HANA system authenticates users with a username and password.

You’ll need to provide:

**Username**

The SAP HANA database user

Examples: SYSTEM, REPORT\_USER

**Password**

The password associated with the user

The password is securely masked in the UI.

{% hint style="info" %}
Ensure that the user has sufficient privileges to access the specified schema and execute queries.
{% endhint %}

***

### ✅ Final Notes

* Verify that the SAP HANA host and port are reachable from DataChannel’s network.
* Ensure the authenticated user has read access (and any required permissions) on the selected schema.
* If you are unsure about ports or schema access, confirm the details with your SAP HANA administrator.

Once configured, DataChannel will validate the connection and make your SAP HANA warehouse available for querying and analysis.
