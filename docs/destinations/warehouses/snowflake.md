# Snowflake

To connect your Snowflake data warehouse to DataChannel, you’ll need a few essential details like your account name, database, and authentication credentials.

### ✍️ Getting Started

To connect to Snowflake, you’ll need to fill in:

* Your **account**, **warehouse**, **database**, and **schema**
* An authentication method:
  * **Standard (Username & Password)**
  * **Key Pair Authentication** (for enhanced security)

### 🛠 Connection Details

Here’s what each field means and how to fill it out:

#### 1. Name

Give this source a unique name so you can easily identify it later.

Example: _snowflake-prod, marketing-snowflake, team-analytics-wh_

> ⚠️ This name must be unique across all sources you configure.

#### 2. Account

Provide your **Snowflake account identifier**. This usually looks like: _your\_org-account\_name_\
or\
&#xNAN;_&#x78;yz12345.us-east-1_

Check your Snowflake URL—it’s usually the part before .snowflakecomputing.com.

#### 3. Warehouse

This is the compute resource that runs your queries.\
Specify the warehouse you want to use for this connection.\
Example: _COMPUTE\_WH_, _ANALYTICS\_WH_

#### 4. Database

Enter the **database name** where your data resides.\
Example: _sales\_data, customer\_360, internal\_metrics_

#### 5. Schema Name

Specify the schema inside the selected database.

Examples: public, analytics

#### 6. Stage Name

Provide the name of the Snowflake stage used for data loading operations.

This stage must already exist and be accessible to the selected user.

Examples: internal\_stage, datacontainer\_stage

### 🔐 Choose Your Authentication Method

You can authenticate using:

* **Standard Authentication** (username & password)
* **Key Pair Authentication** (for secure, key-based login)

#### ✅ Option 1: Standard Authentication

This is the simplest method if you have a username/password for your Snowflake account.

You’ll need:

*   **Username**: Your Snowflake login name

    Example: _readonly\_user_
*   **Password**: The associated password

    This field is securely hidden in the UI.

Use this if you already log in manually to Snowflake using a username and password.

#### 🔐 Option 2: Key Pair Authentication

This method is recommended for automated, production environments.

You’ll need:

*   **User**: Your Snowflake username

    Same as in Standard Auth.
* **Private Key**: A **private key in PKCS#8 PEM format**\
  ❗ **Formatting Requirements:**
  * The key **must be in PEM format (not raw base64 or DER).**
  * It should start with -----BEGIN PRIVATE KEY----- and end with -----END PRIVATE KEY-----.
  * Ensure the key is in **PKCS#8** format (not PKCS#1).
  * The key should be **unencrypted**, or if encrypted, provide the correct passphrase.

Example:

```
-----BEGIN PRIVATE KEY-----
MIIEv...your_key...AB
-----END PRIVATE KEY-----
```

*   **Private Key Passphrase (optional):**\
    If your private key is encrypted, enter the exact passphrase here.

    If your key is unencrypted, leave this blank.

> ℹ️ The private key will be automatically converted to the format expected by Snowflake during connection, so just ensure you copy-paste the PEM content correctly (with all line breaks).

***

### ✅ Final Notes

* Ensure the selected warehouse, database, schema, and stage are accessible.
* Key Pair Authentication is recommended for better security.
* All required fields must be filled before saving.

Once configured, DataChannel will validate the connection and make your Snowflake warehouse available for querying.
