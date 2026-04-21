# BigQuery

This guide helps you connect a Google BigQuery data warehouse to DataChannel. You can either connect your existing BigQuery warehouse or let DataChannel manage one for you.

### ✍️ Getting Started

To connect BigQuery, you’ll need:

* A BigQuery project and dataset
* A Google Cloud Storage (GCS) bucket for staging data
* One of the supported authentication methods
* Required IAM roles or permissions granted to a service account

### 🧭 Warehouse Setup Options

DataChannel supports two ways to set up BigQuery:

#### Option 1: Let DataChannel manage BigQuery for me

(DataChannel-managed warehouse)

#### Option 2: Yes, I would like to connect my own BigQuery warehouse

(Client-managed warehouse)

Choose the option that best fits your setup.

### 🛠 Common Configuration

These fields apply regardless of the setup option you choose.

#### Name

A unique name for this BigQuery warehouse configuration.

> Examples: bigquery-prod, analytics-bq

{% hint style="warning" %}
This name must be unique across all warehouses.
{% endhint %}

### 🧩 Option 1: DataChannel-Managed BigQuery Warehouse

Choose this option if you want DataChannel to automatically manage:

* The BigQuery warehouse
* The service account
* Required permissions

#### Google Accounts to Grant Access

Add the Google email addresses of users who should have access to the DataChannel-managed service account.

Press Enter after each email.

#### Authentication

DataChannel uses a managed Service Account for authentication.

No manual credential setup is required.

#### GCS Configuration

DataChannel automatically manages GCS configuration for staging and data operations.

### 🧩 Option 2: Connect Your Own BigQuery Warehouse

Choose this option if you already have a BigQuery setup and want full control.

#### 🔐 Authentication (Client-Managed)

**Service Account Authentication**

DataChannel generates or displays a Service Account email in the UI.

{% hint style="warning" %}
You must grant the required permissions to this service account email in your Google Cloud project before proceeding.
{% endhint %}

**Required IAM Roles**

Assign one of the following approaches:

**Option A: Predefined Roles (Recommended)**

Grant these roles to the service account:

| Role Name            | Purpose                                  |
| -------------------- | ---------------------------------------- |
| BigQuery Data Editor | Read/write access to datasets and tables |
| BigQuery Job User    | Permission to run BigQuery jobs          |
| Storage Admin        | Access to GCS buckets used for staging   |

**Option B: Custom IAM Role**

You may create a **custom role** with the following permissions:

| Permissions                   | Permissions                        | Permissions                    |
| ----------------------------- | ---------------------------------- | ------------------------------ |
| bigquery.config.get           | bigquery.datasets.get              | bigquery.jobs.create           |
| bigquery.tables.create        | bigquery.tables.delete             | bigquery.tables.get            |
| bigquery.tables.getData       | bigquery.tables.list               | bigquery.tables.update         |
| bigquery.tables.updateData    | bigquery.routines.get              | bigquery.routines.list         |
| resourcemanager.projects.get  | storage.buckets.get                | storage.objects.list           |
| storage.objects.get           | storage.objects.create             | storage.objects.update         |
| storage.objects.delete        | storage.multipartUploads.create    | storage.multipartUploads.abort |
| storage.multipartUploads.list | storage.multipartUploads.listParts |                                |

{% hint style="info" %}
Use this option only if your organization restricts predefined roles.
{% endhint %}

#### Location

Select the BigQuery dataset location.

> Examples:\
> US, EU, asia-northeast1

This must match your dataset’s location.

#### Project ID

The GCP project ID that contains your BigQuery dataset.

> Example:\
> my-analytics-project

#### Dataset ID

The dataset DataChannel will read from and write to.

> Example:\
> events\_analytics

### ☁️ GCS Configuration (Required)

BigQuery uses Google Cloud Storage for staging data.

#### GCS Bucket Name

The name of the GCS bucket used for BigQuery data operations.

> Example:\
> datacontainer-bq-staging

Ensure the service account has access to this bucket.

### ✅ Final Notes

* Make sure the service account has permissions **before saving** the configuration
* Dataset location must match the selected region
* GCS bucket access is required for data load and unload operations

Once configured, DataChannel validates the setup and makes your BigQuery warehouse available for querying and analytics.
