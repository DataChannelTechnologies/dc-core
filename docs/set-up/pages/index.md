# Set-up

In today's day and age, companies are using a wide range of cloud / SaaS-based software/services. The data that these software services provide can offer much more insight than what you can access on their internal dashboards. Combining this data with your internal data can open new avenues for generating insights.

Many of these services offer APIs (Application Programming Interface) for accessing or extracting data from them via a direct and secure internet connection. DataChannel uses these APIs to connect to and get your data from these platforms and, after cleaning and normalizing it, pushes it to your selected [data warehouse](destinations:index.adoc).

## Supported integrations

DataChannel has pre-built connectors for various API Cloud Applications. For a full list of supported APIs, see the list to the left. If there is an integration that you would like but that is not yet supported, please let us know by [sending us an email](mailto://support@datachannel.co).

## Overview of connecting to Cloud Applications

1. Authorize DataChannel to connect to the cloud application on your behalf by creating a set of [credentials](set-up:authentication.adoc). If the cloud application supports it, DataChannel's preferred way of connecting is OAuth. OAuth or Open Authorization lets you connect with DataChannel by directly logging into the application you're connecting with. It grants us restricted access to your account and protects your sensitive information.
2. Select a destination data warehouse for your data.

**IMPORTANT:** Data Warehouse once selected cannot be changed.

3. Start creating your data pipelines by clicking on **+ Data Pipeline** as shown below.

![Data Source Detail](<../../.gitbook/assets/data-source-detail-4 (1).png>)

4. For each pipeline that you create, a table is created in the destination data warehouse selected by you. The table name is always the name given by you to the data-pipeline, prefixed by a standard prefix which differs from data-source to data-source. For example, all data-pipelines created for Facebook ads will start with the prefix `fb_`, and those for Google Sheets will start with `gs_`.

**NOTE:** DataChannel adds two fields, `row_id` and `ts_created`, to all tables created by it for internal audit purposes.
