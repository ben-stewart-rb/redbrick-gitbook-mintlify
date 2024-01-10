# Creating, Editing and Deleting Annotations

All of the Object Labels that you created inside of your Taxonomy will display in the the left side bar of the Annotation Tool. Depending on the elements you included in your Taxonomy, the left side bar will contain up to 4 sections: **Study Classification**, **Series Classification, Instance Classification** and **Object Labels.**

<figure><img src="../.gitbook/assets/app.redbrickai.com_a717f7d8-8a19-4346-b9b4-a90c8d6875ba_projects_7532ec0d-c308-4274-a68e-a88da9eaa887_tool_Label_taskid=f7cf207e-989e-4d52-9bb0-34e2549a306e (1).png" alt=""><figcaption></figcaption></figure>

## Study, Series and Instance Classification

If present, your Study, Series and Instance Classifications will be present under their own expansion panels in the lefthand toolbar.&#x20;

Depending on the type (**Boolean**, **Text**, **Select**, or **Multiselect**), you can directly fill in the corresponding checkbox, select value, or textfield in the grid.&#x20;

{% hint style="info" %}
Click and drag to adjust the size of the grid for easy interaction and viewing!
{% endhint %}

<figure><img src="../.gitbook/assets/ezgif.com-gif-maker (14).gif" alt=""><figcaption></figcaption></figure>

## Object Labels

An Object Label has three components:&#x20;

1. a **Name** (e.g. "Aortic Calcification")
2. a **Type** (e.g. "Segmentation", "Polygon", "Bounding Box", etc.)
3. **Attributes** ("Boolean", "Text", "Select" and "Multiselect", all of which are **optional**)

### Creating Object Labels

The left side bar will show all the Object Labels with an option to create _Entities of that Object Label_. There are two ways to create an Entity of an Object Label:

1. Click on the **"+"** button next to the corresponding Object Label;
2. Use the numeric hotkeys (e.g. 1, 2, 3, etc.) displayed next to the corresponding Object Label&#x20;

When you create an Entity, the default tool for that Label type will be automatically selected (e.g. the **Brush Tool** will be selected by default when creating an Entity of a **Segmentation**).&#x20;

{% hint style="success" %}
Your default Segmentation Tool can be configured on the [Tool Settings page](segmentation/segmentation-tools.md#tool-configuration) within your Project Settings.
{% endhint %}

All Entities are organized within each Object Label's expansion panel.

{% embed url="https://www.loom.com/share/ddf38c93fd5646b9af04f631f368b745?sid=23646aeb-6066-4716-840f-2ec51d1bbe16" %}

#### A Quick Note on Annotation Mapping and Exports

When an annotation is created inside of the Annotation Tool, a corresponding `segmentMap` value is also generated to reflect the order in which the annotation was created.&#x20;

In other words, when exporting a Task's annotations, the first annotation created by a labeler will have a `segmentMap` value of "1" in the accompanying JSON file; the second annotation will have a `segmentMap` value of "2", and so on. For more detailed information about how segmentations are mapped, please see our [Format Reference for Exported Annotations](https://docs.redbrickai.com/python-sdk/reference/export-annotation-format#segmentation).

The RedBrick AI SDK also supports both semantic export and exports of binary masks using the [`export_tasks()` SDK method](https://redbrick-sdk.readthedocs.io/en/stable/sdk.html#redbrick.export.Export.export\_tasks).&#x20;

### Selecting and Editing Object Labels

To edit an Object Label, you must first select it from the left sidebar. Once you select the Entity from the left side bar, the default tool for that label type will be selected automatically, and you can interact with the canvas to apply edits to that Entity.&#x20;

{% hint style="info" %}
When a Object Label Entity is selected, all interactions with the canvas will only modify that particular Entity.
{% endhint %}

### Other Object Label Actions

There are several actions available that are designed to make selecting, viewing, and editing Object Labels as easy as possible for labelers and reviewers.

All actions can be accessed by clicking the three-dot menu button on a Label Entity.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-08-03 at 2.04.17 PM.png" alt=""><figcaption></figcaption></figure>

#### Editing a Selected Label and Attributes&#x20;

You can quickly swap between existing Labels of the same Type (i.e. all of your Segmentation Object Labels, all of your Polygon Object Labels, all of your Bounding Boxes, etc.) in the right side context panel.&#x20;

To reveal this menu in the right hand Context Panel, either click on the Object Label in the viewport or use the "Edit" label action.&#x20;

With the Context Panel open, you can also add, modify, and delete Attributes for an Object Label.

{% embed url="https://www.loom.com/share/55eaf5f270a2407788dc99439201bb29?sid=275eb3c4-2091-4c70-804b-133b61495235" %}

#### Deleting Object Labels

You can delete the selected Object Label by using the `delete` / `backspace` hotkey. Alternatively, you can use the Delete Action in the actions dropdown.&#x20;

To delete all Labels, use the shortcut `shift + delete`/`shift + backspace`.&#x20;

{% hint style="danger" %}
The Delete All Labels action **cannot be undone**. Please ensure that you wish to irrecoverably delete the most recent version of all of your labels before using the Delete All Labels action.
{% endhint %}

Alternatively, you can use the Delete All action in the Object Labels three-dot menu dropdown.&#x20;

#### Hide and Show Labels

You can hide the label you are currently hovering over by using the `h` hotkey. If you are not hovering over a label (either on the canvas or on the left side bar), the `h` hotkey will hide/show the currently selected label.&#x20;

To hide/show all labels use the shortcut `shift + h` or the hide all action in the _Object Labels_ three dot menu dropdown.&#x20;

#### Lock and Unlock Labels

You can lock/unlock the label you are currently hovering over by using the `u` hotkey. If you are not hovering over a label (either on the canvas or in the left side bar), the `u` hotkey will lock/unlock the currently selected label.

To lock/unlock all labels, use the shortcut `shift + u` or the Lock All Action in the Object Labels three-dot menu dropdown.&#x20;

Watch the video below to understand how to prevent/allow the overwriting of annotations.

{% embed url="https://www.loom.com/share/7daf374f6967429dad43b2962c6ccd8f" %}

#### Toggle Vibrant Mode

Vibrant Mode allows you to temporarily highlight a particular Entity. For example, if you have several small Entities of nodules in a chest CT, you can hover over any particular Entity on the left side bar or on the canvas and use the `v` shortcut to activate Vibrant Mode to highlight that Entity. &#x20;

#### Jump to Label

The Jump to Label Action will change the current slice position to the closest slice position that contains a particular annotation. This is useful for revealing annotations on the canvas.&#x20;

***

## Annotation Version Explorer

RedBrick AI's Version Explorer allows users to reference (and, if necessary, restore) previous versions of their annotations within the Annotation Tool.&#x20;

To reference a previously saved set of annotations, click on the Version Explorer button in the top right corner of the screen. The Version Explorer will then display in the right hand Context Panel., allowing you to access previously saved versions of your annotations.

<figure><img src="../.gitbook/assets/image (14).png" alt="" width="563"><figcaption></figcaption></figure>

Restoring an older set of annotations will both:

1. Force a save of the most current set of annotations;
2. Duplicate the older version of annotations and create a new version based on that duplicate.

For example, let's say you (a reviewer) open a Task and see that the latest version of a labeler's annotations is **Version 5**, but you'd like to restore **Version 3**. Choosing to restore **Version 3** will immediately create a duplicate of that version, designate it as the most current version (in this case, **Version 6**), and display the labels in the Editor.

Please see the short video tutorial below for a full overview:

{% embed url="https://www.loom.com/share/1962d135c2b843d58e27b42a64fbf219?sid=54e492df-b065-4907-a0ec-c7d916ba52c1" %}
Version Explorer Tutorial
{% endembed %}

&#x20;