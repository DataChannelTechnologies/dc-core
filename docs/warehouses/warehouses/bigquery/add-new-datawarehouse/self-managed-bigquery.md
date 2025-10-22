# Self Managed BigQuery

#### Option 1 : Adding your own BigQuery Data warehouse to your DataChannel Account

**Step 1:** Add the given email to your google cloud account and ensure that you have granted the permissions listed. Click on **Next**.&#x20;

**Step 2:** Enter the details for your BigQuery Dataset in the form and click on **Validate Configuration** to add the warehouse. An explanation of each of the fields in the form is given below.

> Note: Users are requested to fill out all the required fields in the Warehouse Details section.

1. **Name:** Provide a name for your warehouse. It needs to be unique across your account.
2. **Dataset Name:** Provide the name of your BigQuery Dataset (you can get this from the BigQuery console).
3. **Project ID:** Provide the project ID for the cloud project which has the BigQuery Dataset.
4. **BigQuery Region:** Provide the region / location where your Dataset is located.
5. **BigQuery Authentication Code:** Click on the link **Generate Authentication Code** and follow the process given [here](set-up:authentication.adoc) to generate a code using OAuth2
6. **Use DataChannel GCS:** Leave this toggle off so that you can specify your own GCS bucket.
7. **GCS Project ID:** Provide the project ID where you have created the Google Cloud Storage Bucket to store the raw data files. Note that DataChannel does not remove the files after they have been copied into GCS so it is advisable to use life cycle properties to manage the removal / archival of the raw files to manage GCS costs.
8. **GCS Bucket Name:** Provide the name of the cloud storage bucket you have created for DataChannel.
9. **GCS Region Name:** Provide the name of the region where your GCS Bucket is stored. Note:- This should be same as the region for your BigQuery Dataset.
10. **GCS Authentication Code:** Click on the link **Generate Authentication Code** and follow the process given [here](set-up:authentication.adoc) to generate a code using OAuth2



