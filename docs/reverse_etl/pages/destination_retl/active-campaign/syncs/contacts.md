# Contacts

This sync can be used to load data of contacts from your data warehouse into Active Campaign platform.

## SETUP
### Configuring the CredentialsSelect the account credentials which has access to relevant Active Campaign data from the given list & Click on Next

****

Credentials not listed ?:
Click on + for adding new credentials and fill the form that pops-up.
****

![](../images/active-campaign-new-creds.png)

## Data Sync Details
Data Sync::
Select *Contacts* & click on Next

![](../images/active-campaign-contacts-list.png)

Account::Select an account from the drop-down.

Data Model::Select a Data Model from the drop-down.

## Setting Parameters

![](../images/active-campaign-contacts-config.png)

| Parameter | Description | Values |
|-----------|-------------|--------|
| Fields Selection | *Required* <br> Select the field(s) you would like to push in your Active Campaign platform here. Note that it is mandatory to map the `email` field to a respective model field. | {Destination Field Name, Model Field Name} |
| Fetch Mode | *Required* <br> This refers to the manner in which data will get updated : FULL will update the entire column(s) from the selected data, INCREMENTAL will update the fresh record(S) added since last fetch | {Incremental, Full} <br> _Default Value:_ FULL |
| Incremental Key | *Dependant* <br> *Required (If Fetch Mode = Incremental)* | Choose the field which will serve as Incremental key. |
| Insert Mode | *Required* <br> This refers to the manner in which data will be updated in the Active Campaign Platform; with 'Update' selected, the data will be updated (only existing records) and with 'Append' selected, all data fetched will be inserted. Selecting 'Delete' will delete the records. | `Update`, `Append`, `Delete` |

# Scheduling Syncs
include::ROOT:partial$name_schedule_syncs.adoc[]