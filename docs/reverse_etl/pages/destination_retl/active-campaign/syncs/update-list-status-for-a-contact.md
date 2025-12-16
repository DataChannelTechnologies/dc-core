# Update List Status For A Contact

This sync can be used to subscribe a contact to a list or unsubscribe a contact from a list in your Active Campaign platform.

## SETUP

### Configuring the CredentialsSelect the account credentials which has access to relevant Active Campaign account from the given list & Click on Next

***

Credentials not listed ?: Click on + for adding new credentials and fill the form that pops-up.

***

![](<../../../../../.gitbook/assets/active-campaign-new-creds (1).png>)

## Data Sync Details

Data Sync:: Select _Update List Status for a Contact_ & click on Next

![](../../../../../.gitbook/assets/active-campaign-update-list-status-for-a-contact-list.png)

Data Model::Select a Data Model from the drop-down.

## Setting Parameters

![](../../../../../.gitbook/assets/active-campaign-update-list-status-for-a-contact-config.png)

| Parameter        | Description                                                                                                                                                                                                                      | Values                                                     |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Fields Selection | <p><em>Required</em><br>Select the field(s) you would like to push in your Active Campaign platform here. Note that it is mandatory to map the <code>list</code> and <code>contact</code> fields to respective model fields.</p> | {Destination Field Name, Model Field Name}                 |
| Fetch Mode       | <p><em>Required</em><br>This refers to the manner in which data will get updated : FULL will update the entire column(s) from the selected data, INCREMENTAL will update the fresh record(S) added since last fetch</p>          | <p>{Incremental, Full}<br><em>Default Value:</em> FULL</p> |
| Incremental Key  | <p><em>Dependant</em><br><em>Required (If Fetch Mode = Incremental)</em><br>Choose the field which will serve as Incremental key.</p>                                                                                            | Select Incremental Key                                     |

## Scheduling Syncs

{% include "../../../../../ROOT/partials/name_schedule_syncs.md" %}
