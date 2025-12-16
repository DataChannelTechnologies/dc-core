# Contacts

## Contacts

This sync can be used to load data of contacts from your data warehouse into Active Campaign platform.

### SETUP

#### Configuring the CredentialsSelect the account credentials which has access to relevant Active Campaign data from the given list & Click on Next

***

Credentials not listed ?: Click on + for adding new credentials and fill the form that pops-up.

***

![](<../../../../../.gitbook/assets/active-campaign-new-creds (1).png>)

### Data Sync Details

Data Sync:: Select _Contacts_ & click on Next

![](<../../../../../.gitbook/assets/active-campaign-contacts-list (1).png>)

Account::Select an account from the drop-down.

Data Model::Select a Data Model from the drop-down.

### Setting Parameters

![](<../../../../../.gitbook/assets/active-campaign-contacts-config (1).png>)

| Parameter        | Description                                                                                                                                                                                                                                                                                              | Values                                                     |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Fields Selection | <p><em>Required</em><br>Select the field(s) you would like to push in your Active Campaign platform here. Note that it is mandatory to map the <code>email</code> field to a respective model field.</p>                                                                                                 | {Destination Field Name, Model Field Name}                 |
| Fetch Mode       | <p><em>Required</em><br>This refers to the manner in which data will get updated : FULL will update the entire column(s) from the selected data, INCREMENTAL will update the fresh record(S) added since last fetch</p>                                                                                  | <p>{Incremental, Full}<br><em>Default Value:</em> FULL</p> |
| Incremental Key  | <p><em>Dependant</em><br><em>Required (If Fetch Mode = Incremental)</em></p>                                                                                                                                                                                                                             | Choose the field which will serve as Incremental key.      |
| Insert Mode      | <p><em>Required</em><br>This refers to the manner in which data will be updated in the Active Campaign Platform; with 'Update' selected, the data will be updated (only existing records) and with 'Append' selected, all data fetched will be inserted. Selecting 'Delete' will delete the records.</p> | `Update`, `Append`, `Delete`                               |

## Scheduling Syncs

{% include "../../../../../ROOT/partials/name_schedule_syncs.md" %}
