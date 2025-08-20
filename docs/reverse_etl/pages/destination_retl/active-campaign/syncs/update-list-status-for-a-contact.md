# Update List Status for a Contact

This sync can be used to subscribe a contact to a list or unsubscribe a contact from a list in your Active Campaign platform.

## SETUP
### Configuring the CredentialsSelect the account credentials which has access to relevant Active Campaign account from the given list & Click on Next

****

Credentials not listed ?:
Click on + for adding new credentials and fill the form that pops-up.
****

![](../images/active-campaign-new-creds.png)


## Data Sync Details
Data Sync::
Select *Update List Status for a Contact* & click on Next

![](../images/active-campaign-update-list-status-for-a-contact-list.png)

Data Model::Select a Data Model from the drop-down.

## Setting Parameters

![](../images/active-campaign-update-list-status-for-a-contact-config.png)

| Parameter | Description | Values |
|-----------|-------------|--------|
| Fields Selection | *Required* <br> Select the field(s) you would like to push in your Active Campaign platform here. Note that it is mandatory to map the `list` and `contact` fields to respective model fields. | {Destination Field Name, Model Field Name} |
| Fetch Mode | *Required* <br> This refers to the manner in which data will get updated : FULL will update the entire column(s) from the selected data, INCREMENTAL will update the fresh record(S) added since last fetch | {Incremental, Full} <br> _Default Value:_ FULL |
| Incremental Key | *Dependant* <br> *Required (If Fetch Mode = Incremental)* <br> Choose the field which will serve as Incremental key. | Select Incremental Key |

## Scheduling Syncs
include::ROOT:partial$name_schedule_syncs.adoc[]