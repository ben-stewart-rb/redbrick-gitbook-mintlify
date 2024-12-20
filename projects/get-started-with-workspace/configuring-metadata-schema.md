# Configuring Metadata Schema

Metadata Schema allows you to configure the workspace according to the metadata schema extracted from a CSV file or the DICOM headers. This schema is highly flexible and not strictly enforced on the uploaded data, providing maximum adaptability to your data format and allowing the schema to evolve.

Metadata schemas support the following data types for your metadata:

* NUMBER = "number"
* STRING = "string"
* DATETIME = "datetime"
* ENUM = "enum"

### Importing Metadata to RedBrick AI

```python
# A script for converting from CSV to a JSON file for uploading to RedBrick AI
import csv
import json


def csv_to_list_of_dicts(filename):
    with open(filename, "r") as file:
        reader = csv.DictReader(file)
        data = list(reader)
    return data


# Use the function
cases = csv_to_list_of_dicts("tags_and_paths.csv")


def item_to_redbrick_usable_url(item: str) -> str:
    """
    Convert the item stored in the csv file to something that RedBrick can use.

    This will vary depending on where your images are stored. In this case, images are stored
    at a public url. Yours is probably stored in an S3 bucket and your paths will be generated differently.

    Check docs.redbrickai.com for more information.
    """
    return "https://datasets.redbrickai.com/chest_ct_lidc_idri/" + item


upload_format = []
for case_ in cases:
    # ['LIDC-IDRI-0195/1-102.dcm', 'LIDC-IDRI-0195/1-103.dcm', ...]
    items = case_["items"]

    # parse the way items were stored in the csv file
    items = json.loads(items.replace("'", '"'))
    del case_["items"]

    metadata = case_

    upload_format.append(
        {
            "items": [item_to_redbrick_usable_url(item) for item in items],
            "metaData": metadata,
        }
    )


# Write to a JSON file
with open("upload_format.json", "w+") as file:
    json.dump(upload_format, file, indent=2)
```

This will produce a JSON file in the following format:

```json

[
  {
    "items": [
      "https://datasets.redbrickai.com/chest_ct_lidc_idri/LIDC-IDRI-0125/1-013.dcm",
      ...
    ],
    "metaData": {
      "PatientID": "ABC-125",
      "StudyDate": "20000101",
      "StudyTime": "",
      "AccessionNumber": "",
      "Modality": "CT",
      "Manufacturer": "GE MEDICAL SYSTEMS",
      "StudyDescription": "",
      "SeriesDescription": "",
      "PatientName": "",
      "PatientBirthDate": "",
      "PatientSex": "",
      "BodyPartExamined": "CHEST",
      "SliceThickness": "1.250000",
      "KVP": "120",
      "DistanceSourceToDetector": "949.075012",
      "DistanceSourceToPatient": "541.000000",
      "GantryDetectorTilt": "0.000000",
      "TableHeight": "156.500000",
      "RotationDirection": "CW",
      "XRayTubeCurrent": "400",
      "CountryOfResidence": "",
      "PatientIdentityRemoved": "YES",
      "PatientPosition": "FFS"
    }
  },
  ...
]
```

{% hint style="info" %}
Before creating the metadata schema in RedBrick AI, we recommend that you import metadata into RedBrick AI.
{% endhint %}

### Creating Metadata Schema in RedBrick AI

{% embed url="https://share.redbrickai.com/rxsH3BJG" %}

Once you've imported the metadata, you can create Cohorts based on your custom metadata schema and then send those Cohorts to Annotate.

To create a Metadata schema, follow these steps:

1. Go to "Settings."
2. Click on "Metadata Schema."
3. Choose from the four schema types: Date, Number, Enum, and Textfield.
4. Create the desired schema.

After creating the schema, you can use it as follows:

1. Go to "Data."
2. Click on the "Filter" button in the top right corner.
3. Apply the filter to the metadata you want to view, sort, or add to a cohort.
4. Once filtered, select all the filtered data points.
5. Add the selected data points to a cohort or a project.
