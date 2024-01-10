# Import Cloud Data

RedBrick AI supports integration with a range of cloud providers, allowing you to make use of its suite of tools without having to upload your data directly to our servers.&#x20;

While the steps and configurations required for uploading data from cloud storage vary depending on your provider, the overall procedure remains the same.

1. [Configure your cloud storage](import-cloud-data/creating-an-items-list.md) - AWS s3, Google Cloud Storage, Azure Blob Storage
2. Create and upload an [Items List](import-cloud-data.md#items-list) - your Items List communicates the location of your data in your cloud storage to RedBrick AI's platform.&#x20;

***

## Configuring Cloud Storage

RedBrick AI currently supports the following external storage methods:

* [AWS S3 Buckets](configuring-external-storage/configuring-aws-s3.md)
* [Google Cloud Storage](configuring-external-storage/configuring-gcs.md)
* [Azure Blob Storage](import-cloud-data/configuring-azure-blob.md)
* Public - this includes data stored on your computer, as well as data stored on any public server accessible via URL

After opening the Storage tab in the lefthand sidebar, click on **New Storage Method** to configure your new Storage Method for further use with RedBrick AI. After inputting the required credentials, click on **Create Storage** to integrate your cloud storage with RedBrick AI.

If you are using AWS, GCS, or Azure for third-party storage, you can also make use of the **Verify** action to ensure that your Storage Method has been successfully configured.

<figure><img src="../.gitbook/assets/sample-path-verification.gif" alt=""><figcaption></figcaption></figure>

If your Storage Method has been configured correctly, pasting a sample file path to one of your visual assets into the field will display the following:

<figure><img src="../.gitbook/assets/Screenshot 2023-08-15 at 11.29.03 AM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The **Sample File Path** field expects a file path starting at your bucket, not a full URL.

:heavy\_multiplication\_x: **Don't Do:** https://s3.region-1.amazonaws.com/redbrick-bucket/project-2/brain-mri.dcm

:heavy\_check\_mark: **Do:** redbrick-bucket/project-2/brain-mri.dcm
{% endhint %}

Once your Storage Method has been integrated, you can move on to creating an Items List.

***

## Items List

### Overview

Your Items List is a JSON file that points the RedBrick AI platform to the data in your external storage and allows you to selectively import data points that can be annotated as single units of work.&#x20;

{% hint style="danger" %}
Jargon Alert! Single units of work (i.e. a single row on the Data Page) are referred to as **Tasks** within RedBrick AI.
{% endhint %}

Your Items List can be uploaded to RedBrick from the Project Dashboard or by using the [SDK](../python-sdk/sdk-overview/importing-data-and-annotations.md). Each entry in your Items List will be created as a separate Task, and you can find detailed explanations of each key in our [Format Reference](../python-sdk/formats/full-format-reference.md#tasks-json).&#x20;

### Creating & Configuring an Items List

The format of your Items List depends on both the type of cloud storage you have integrated with RedBrick AI and the type of data you are uploading.

For solution-specific instructions regarding how to format your Items List with [AWS S3](configuring-external-storage/configuring-aws-s3.md#items-path), [GCS](configuring-external-storage/configuring-gcs.md#items-path), [Azure Blob Storage](import-cloud-data/configuring-azure-blob.md#items-path), or a [Public source](https://docs.redbrickai.com/importing-data/import-cloud-data/creating-an-items-list#example-items-path), please refer to the corresponding configuration guide.

***

## Importing Data

Once you have integrated your third-party Storage Method (where applicable) and generated an Items Path, all that you have to do is click on **Import Data** within your Project and upload the Items Path.&#x20;

<figure><img src="../.gitbook/assets/items_list_popout.png" alt=""><figcaption><p>Clicking on Import Data will allow you to upload your Items List</p></figcaption></figure>

Congratulations! Now you're ready to begin working on RedBrick AI!

***

## Data Privacy

When using an external storage method with RedBrick AI, all of your data is transferred directly from your storage method to your browser.

<figure><img src="../.gitbook/assets/Group 476.png" alt=""><figcaption></figcaption></figure>

Your raw data will never be routed through RedBrick AI's servers, downloaded, or duplicated (unless specifically requested for certain features - please review our [Privacy Policy](https://redbrickai.com/policies/privacy.pdf)).&#x20;

## Supported Data Formats

RedBrick AI supports a variety of different image and volume formats:&#x20;

1. DICOM - .dcm, .ima, .dicom, .dicm
2. NIfTI - .nii, .nii.gz
3. Videos - .mp4, .mov, .avi
4. RGB Images - .png, .jpeg, .jpg, .bmp
5. NRRD - .nrrd

{% hint style="success" %}
If you require additional support for a file format that is not present in this list, please reach out to us at support@redbrickai.com.&#x20;
{% endhint %}
