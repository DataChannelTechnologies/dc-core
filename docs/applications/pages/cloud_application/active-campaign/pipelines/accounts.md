# Accounts

This Accounts pipeline can be used to request and retrieve details of all existing accounts. The Accounts pipeline contains information about each business you work with.

Read more about the Accounts pipeline [here](https://developers.activecampaign.com/reference/list-all-accounts "window=_blank")

## Configuring the CredentialsSelect the account credentials which has access to relevant Active Campaign data from the dropdown menu and click on **Next**.

****

Credentials not listed in dropdown? Click on **+ Add New** for adding new credentials
****

## Data Pipelines DetailsData Pipeline:
Select *Accounts* from the dropdown

![Active Campaign Accounts List](../images/active-campaign-accounts-list.png)

## Setting Parameters
| Parameter | Description | Values |
|-----------|-------------|--------|
| Insert Mode | **Required**<br>This refers to the manner in which data will get updated in the data warehouse, with 'Upsert' selected, the data will be upserted (only new records or records with changes) and with 'Append' selected, all data fetched will be inserted. Selecting 'Replace' will ensure the table is dropped and recreated with fresh data on each run. Recommended to use "Upsert" option unless there is a specific requirement. | `Upsert`, `Append`, `Replace` <br> **Default Value:** Upsert |

![Active Campaign Accounts Config](../images/active-campaign-accounts-config.png)