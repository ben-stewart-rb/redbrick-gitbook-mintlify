# Creating an Items List

An Items List is a JSON file that points the RedBrick AI platform to the data in your external storage and allows you to selectively import data points. The format of your Items List depends on both the type of cloud storage you have integrated with RedBrick AI and the type of data you are uploading.

For solution-specific instructions regarding how to format your Items List with [AWS S3](../configuring-external-storage/configuring-aws-s3.md#items-path), [GCS](../configuring-external-storage/configuring-gcs.md#items-path), or [Azure Blob Storage](configuring-azure-blob.md#items-path), please refer to the corresponding configuration guide.

It's important to note that each entry in your Items List **will be created as a separate task**, which can then be annotated as a single unit. You can find detailed explanations of each key in our [format reference](https://docs.redbrickai.com/python-sdk/reference/annotation-format#tasks-json).

After creating your JSON Items List, you can upload it from RedBrick AI's Project Dashboard or by using the [SDK](../../python-sdk/sdk-overview/importing-data-and-annotations.md).

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Click on Upload Data</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/items_list_popout.png" alt=""><figcaption><p>Select a Storage Method and upload your Items List</p></figcaption></figure>

{% hint style="info" %}
Please note that there is no need to create an Items List when using [Direct Upload](../direct-data-upload.md).
{% endhint %}

###

### Example Items Path

The example below contains fields relevant to image-only uploads.

```typescript
type Items = Task[];

interface Task { 
    // A unique, user-defined ID 
    // After import, you can search tasks using this field. 
    name: string;

    // You can upload a single series, or an entire study (array of series) 
    series: Series[]; 
}

interface Series { 
    // Filepath/URL's of all the instances in a single series. 
    items: string[] | string; 
    name: string; 
}
```

{% hint style="info" %}
The `items` entry enumerates the file paths referencing your data in your cloud storage. Depending on the storage method, this file path may be relative to your bucket name or the root folder in your bucket. Please reference the relevant documentation to verify the format of the Items path for each of RedBrick AI’s supported storage methods:

* [AWS S3 Items Path](../configuring-external-storage/configuring-aws-s3.md#items-path)
* [Azure Blob Items Path](configuring-azure-blob.md#items-path)
* [GCS Items Path](../configuring-external-storage/configuring-gcs.md#items-path)
* Public Storage Items Path
{% endhint %}



### Example Item Lists by Format

#### 3D DICOM

{% tabs %}
{% tab title="3D DICOM Study" %}
This Items List will upload a single task containing two series.

```javascript
[
  {
    name: 'study001',
    series: [
      {
        items: [
          'study001/series001/001.dcm',
          'study001/series001/002.dcm',
          'study001/series001/003.dcm',
        ],
      },
      {
        items: [
          'study001/series002/001.dcm',
          'study001/series002/002.dcm',
          'study001/series002/003.dcm',
        ],
      },
    ],
  },
];
```
{% endtab %}

{% tab title="3D DICOM Series" %}
This Items List will upload two tasks, each containing a single series.

```javascript
[
  {
    name: 'series001',
    series: [
      {
        items: ['series001/001.dcm', 'series001/002.dcm', 'series001/003.dcm'],
      },
    ],
  },
  {
    name: 'series002',
    series: [
      {
        items: ['series002/001.dcm', 'series002/002.dcm', 'series002/003.dcm'],
      },
    ],
  },
];
```
{% endtab %}
{% endtabs %}



#### NIfTI

{% hint style="warning" %}
Please note that`items` must be a single string for NIfTI uploads.&#x20;
{% endhint %}

{% tabs %}
{% tab title="NIfTI Series" %}
This Items List will upload a single task containing two series.

<pre class="language-javascript"><code class="lang-javascript">[
<strong>  {
</strong>    name: 'study001',
    series: [
      {
        items: 'series001.nii',
      },
      {
        items: 'series002.nii',
      },
    ],
  },
];
</code></pre>
{% endtab %}

{% tab title="NIfTI Study" %}
This Items List will upload two tasks, each containing one series.

```javascript
[
  {
    name: 'series1',
    series: [
      {
        items: 'series001.nii',
      },
    ],
  },
  {
    name: 'series2',
    series: [
      {
        items: 'series002.nii',
      },
    ],
  },
];
s
```
{% endtab %}
{% endtabs %}



#### 2D Image

{% tabs %}
{% tab title="2D Image Study" %}
This Items List will upload a single task containing two images.

```javascript
[
  {
    name: 'patient1',
    series: [
      {
        items: 'scan1.dcm',
      },
      {
        items: 'scan2.dcm',
      },
    ],
  },
];
```
{% endtab %}

{% tab title="2D Image Series" %}
This Items List will upload two tasks, each containing a single image.

```javascript
[
  {
    name: 'patient1',
    series: [
      {
        items: 'scan.dcm',
      },
    ],
  },
  {
    name: 'patient2',
    series: [
      {
        items: 'scan.dcm',
      },
    ],
  },
];
```
{% endtab %}
{% endtabs %}



#### Video Frames

{% hint style="warning" %}
The frames must be in the correct order in the `items` array.
{% endhint %}

{% tabs %}
{% tab title="Video Frames Study" %}
This Items List will upload a single task with two videos, where each video contains three frames.

```javascript
[
  {
    name: 'study001',
    series: [
      {
        items: [
          'study001/series001/001.png',
          'study001/series001/002.png',
          'study001/series001/003.png',
        ],
      },
      {
        items: [
          'study001/series002/001.png',
          'study001/series002/002.png',
          'study001/series002/003.png',
        ],
      },
    ],
  },
];
```
{% endtab %}

{% tab title="Video Frames Series" %}
This Items List will upload two tasks, each containing a single video with three frames.

```javascript
[
  {
    name: 'video1',
    series: [
      {
        items: ['001.png', '002.png', '003.png'],
      },
    ],
  },
  {
    name: 'video2',
    series: [
      {
        items: ['001.png', '002.png', '003.png'],
      },
    ],
  },
];h
```
{% endtab %}
{% endtabs %}

## Automatically Split Study

In some use cases, you can rely on RedBrick AI to split your Study into a list of Series. This can be especially useful if you do not follow a strict naming convention for your studies.

You can upload a single Series or multiple Series per task using the simplified Study-Level format.

```javascript
type Items = Task[];

interface Task {
  // A unique, user-defined ID
  // After import, you can search tasks using this field.
  name: String;

  // You can upload a single series, or an entire study (array of .dcm files)
  // The items array will automatically be split into individual series. 
  items: String[]
}
```

{% hint style="info" %}
This format is the same as the Legacy Items List format (pre-July 2022)
{% endhint %}

{% tabs %}
{% tab title="DICOM" %}
The Items List below will create a single task containing one or more series. RedBrick AI will parse the DICOM files on the client side and automatically split this list of `.dcm` into one or more series (depending on the DICOM headers).&#x20;

```javascript
[
  {
    name: 'study001',
    items: [
      'bbfa85feb36f.dcm',
      'd4a49634cd4c.dcm',
      'eed2e7462ba5.dcm',
      '45455dd0e45b.dcm',
    ],
  },
]
```
{% endtab %}

{% tab title="NIfTI" %}
The Items List below will create a single task containing exactly two series. RedBrick AI will assume each of the NIfTI files in the `items` array is an individual series.

```javascript
[
  {
    name: 'study001',
    items: [
      'bbfa85feb36f.nii.gz',
      'd4a49634cd4c.nii'
    ],
  },
]
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Please note that any tasks uploaded using this format will only be automatically split _**after**_ a user opens it in the labeling interface.&#x20;
{% endhint %}
