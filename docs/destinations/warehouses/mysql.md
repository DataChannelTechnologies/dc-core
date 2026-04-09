# MySQL

You can connect your MySQL database to DataChannel using a small set of connection details and credentials. This guide walks you through the setup step by step—whether you’re using a standard username/password login or secure SSL-based authentication.

### ✍️ Getting Started

To connect to a MySQL database, you’ll need:

* Basic connection details like **host, port, database**
* One of two authentication options:
  * **Standard Authentication (userame & password)**
  * **SSL Authentication (certificate-based, recommended for production)**

### 🛠 Connection Details

Here’s what each field means and how to fill it out:

#### 1. Name

Pick a **unique name** for this MySQL warehouse.\
This name helps you identify the warehouse later, especially when managing multiple MySQL or other database connections.

> Example: mysql-prod, user-service-db, team-marketing-mysql

{% hint style="warning" %}
This name must be **unique** across all your sources.
{% endhint %}

#### 2. Host

Provide the hostname or IP address of your MySQL server.

> Examples: mysql.internal.company.com, 10.0.0.12

If your database is hosted on a cloud provider (AWS RDS, GCP Cloud SQL, Azure Database for MySQL), use the endpoint provided by the service.

#### 3. Port

The port used to connect to MySQL server.\
Default is **3306** — change it only if your server uses a different port.

#### 4. Database

Enter the name of the **database** you want to connect to.

> Example: _customer\_data, inventory_

### 🔐 Authentication Options

Depending on how your server is configured, you can choose between:

<details open>

<summary><code>Option 1</code>  Standard Authentication</summary>

Use this if your database uses a username and password for login.

You’ll need:

*   **Username**: The username you use to access MySQL

    Example: _readonly\_user_
*   **Password**: The corresponding password

    This will be securely masked in the UI.

</details>

<details open>

<summary><code>Option 2</code>  SSL Authentication</summary>

Use this if your server requires SSL certificate-based authentication for enhanced security.

You’ll need:

* **Username:** Your MySQL login name
* **Password:** The corresponding password for the user
*   **SSL Root Certificate (ssl\_ca)**

    The contents of the root CA certificate (ca.pem)

    This is used to verify the identity of the MySQL server.
*   **SSL Client Certificate (ssl\_cert)**

    Your client certificate (client-cert.pem)

    This identifies the client during the SSL handshake.
*   **SSL Client Key (ssl\_key)**

    Your private key (client-key.pem) corresponding to the client certificate.<br>

    🔐 Certificate requirements:

    * All certificates must be in PEM format
    * Paste the full contents of each file, including:
      * \-----BEGIN CERTIFICATE-----
      * \-----END CERTIFICATE-----
* The private key must match the provided client certificate

</details>

### ✅ Final Notes

* Make sure the MySQL user has sufficient permissions to access the selected database.
* If SSL is enabled on the server, Standard Authentication without certificates may fail.
* Network-level access (VPC peering, IP allowlists, firewalls) must allow DataChannel to reach the MySQL host.

Once configured, DataChannel will validate the connection and make your MySQL warehouse available for querying and analysis.
