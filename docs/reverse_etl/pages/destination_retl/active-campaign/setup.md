# Setup Guide - Active Campaign

Follow our setup guide to reverse ETL to Active Campaign platform using DataChannel.

## Prerequisites

To connect Active Campaign to DataChannel, you need:

* An active Active Campaign account with permissions to write data to the accounts you'd like to sync.
* An API Key. The process to retrieve this key is described [here](https://developers.activecampaign.com/reference/authentication).

## Setup Instructions

1. Create a data model and specify the **data warehouse** from which you want the data for your Active Campaign platform. If you have not yet added a data warehouse, go to the **Data Warehouse** tab and add a warehouse.
2. Authorise DataChannel to connect to your Active Campaign account using the API key and Account name. For example, the URL for an account uses the format: `abcd.activehosted.com`, then please enter only `abcd` in the given field.

![New Credentials](../images/reverse_etl/active-campaign-new-creds.png)

3. Click on **+ Data Sync** to start adding data syncs to your account.

![Add Sync](../images/reverse_etl/active-campaign-add-sync.png)

4. Details of individual syncs are available [here](reverse_etl/destinations_retl/active-campaign/syncs.adoc).

[Question]