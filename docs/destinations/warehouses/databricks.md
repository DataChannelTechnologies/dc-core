# Databricks

You can connect your Databricks (Unity Catalog, Delta Lake) workspace to DataChannel by providing a few essential configuration details. This guide walks you through each required setting step by step, including warehouse identifiers and authentication credentials.

### ✍️ Getting Started

To connect Databricks, you'll need:

* Workspace Details: Server Hostname and HTTP Path.
* Unity Catalog: Catalog name, Schema, and Volume name.
* Authentication: Personal Access Token or OAuth M2M Client ID and Client Secret (Service Principal).

### 🛠 Connection Details

Below are the details required to configure a Databricks connection.

#### 1. Name

Choose a unique name for this Databricks destination configuration. This helps you identify it later if you have multiple Databricks or other data warehouse connections.

> Examples: prod-databricks, finance-delta-east

{% hint style="warning" %}
The name must be unique for each destination you add.
{% endhint %}

#### 2. Server Hostname

Enter your Databricks workspace hostname. You can find this in the Databricks UI under **SQL Warehouses → your warehouse → Connection details**, or directly from your workspace URL.

> Example: adb-1234567890.12.azuredatabricks.net

{% hint style="info" %}
Do not include `https://` — enter the hostname only.
{% endhint %}

#### 3. HTTP Path

Enter the HTTP path for the SQL Warehouse that DataChannel will use to run queries. Find this under **SQL Warehouses → your warehouse → Connection details**.

> Example: /sql/1.0/warehouses/abc123def456

#### 4. Catalog

Enter the Unity Catalog name where your target schema lives. DataChannel will write all tables under `<catalog>.<schema>`.

#### 5. Schema

Enter the schema (database) inside the catalog where DataChannel will create and write Delta tables.

{% hint style="warning" %}
The schema must already exist in Databricks before connecting. DataChannel does not create it automatically.
{% endhint %}

#### 6. Volume Name

Enter the Unity Catalog Volume name to use as a staging area. DataChannel uploads Parquet files here before loading them into the target Delta table. The staging path resolves to `/Volumes/<catalog>/<schema>/<volume_name>/`.

{% hint style="warning" %}
The volume must already exist in Databricks. DataChannel does not create it automatically.
{% endhint %}

### 🔐 Authentication

DataChannel supports two authentication methods for Databricks.

<details>

<summary><code>Option 1</code> Personal Access Token (PAT)</summary>

**Access Token**

A long-lived token tied to a specific Databricks user account. Generate one in the Databricks UI under **Settings → Developer → Access Tokens**.

This value is securely masked in the UI.

{% hint style="info" %}
PATs are tied to the generating user account. If that account is deactivated, the token stops working. Prefer OAuth M2M for production use.
{% endhint %}

</details>

<details>

<summary><code>Option 2</code> OAuth M2M (Service Principal)</summary>

DataChannel uses OAuth Machine-to-Machine authentication to securely connect to Databricks using an Azure Service Principal. Tokens are automatically refreshed — no manual rotation required. Configure your Service Principal in Databricks under **Settings → Identity and Access → Service Principals.**

**Client ID**

The application (client) ID of your Azure Service Principal.

> Example: 12345678-abcd-1234-efgh-1234567890ab

**Client Secret**

The client secret associated with your Service Principal.

This value is securely masked in the UI.

{% hint style="info" %}
Ensure that your Service Principal has the necessary permissions on the target catalog, schema, and volume in Unity Catalog to perform data operations.
{% endhint %}

</details>

### ✅ Final Notes

* **Insert Modes**: DataChannel supports Append (new rows added), Replace (table truncated then reloaded), and Upsert (rows merged on specified key columns).
* **Table Creation**: If the target Delta table does not exist, DataChannel creates it automatically with schema evolution enabled.
* **Security**: Using a Service Principal (OAuth M2M) is the recommended way to manage programmatic access to Databricks without using individual user credentials.
* **Verification**: Once configured, DataChannel will validate the connection to ensure it can successfully reach your SQL Warehouse and Unity Catalog.
