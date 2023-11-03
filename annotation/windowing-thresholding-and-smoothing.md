# Visualization and Masking

{% hint style="warning" %}
As of v2023.10.31.1:\
\- **Thresholding** is now referred to as **Masking;**\
\- the **Windowing Panel** is now referred to as the **Visualization Panel;**
{% endhint %}

RedBrick AI allows you to apply filters to your images and volumes to help with visualization and segmentation.&#x20;

For a brief visual overview, please see the following video tutorial:

{% embed url="https://www.loom.com/share/775da2c8809d4dc2813db013b8bd7a61?sid=1c1806a9-22d7-4c4b-948e-d672e4e5e326" %}

## Visualization

You can adjust the Window Width and Level of your volumes by pressing `CTRL` and `LEFT CLICK` dragging on any viewport - `up/down` to adjust Window Level, `left/right` to adjust Window Width.&#x20;

You see and/or modify the current Visualization settings by selecting the Visualization Panel on the top right of the tool bar.&#x20;

When the Visualization Panel is open, its settings will display in the right hand Context Panel:

* Window Width
* Window Level
* Optional Presets
* Inverted View
* Pixel Interpolation
* Label Opacity
* Label Outlines

## Masking

The Masking Panel consists of the following elements:

* **Editable Area** dropdown
* **Modify Other Segments** dropdown
* **Restrict by pixel intensity** toggle
  * Masking Range slider
  * Threshold Range Selector

### Editable Area

The Editable Area dropdown has two selections - **Everywhere** and **Inside all segments**.

Selecting **Everywhere** allows you to draw on any part of the canvas.

Selecting **Inside all segments** makes it impossible for the user to annotate on an unannotated area of the canvas. In other words, the user must annotate within the bounds of an existing annotation.

### Modify Other Segments

The Modify Other Segments dropdown helps you control how your painting affects other existing annotations.

Selecting **Overlap** will allow you to paint on top of other annotations. This process is additive, which means annotating with **Overlap** does not alter or delete other annotations.

Selecting **Overwrite unlocked segments** will also allow you to paint on top of other annotations, but you will overwrite (and therefore delete) anything else that you paint on top of.

For a visual walkthrough of how to configure **Editable Area** and **Modify Other Segments** settings, as well as a demonstration of the differences between them, please see the following video tutorial:

{% embed url="https://www.loom.com/share/536fa33679814e2f909e4944b1c0f8ba?sid=53421d5e-bc67-4651-952b-c62511ccc520" %}

### Restrict by Pixel Intensity

To speed up segmentation, you can create a masking range by applying an upper and lower boundary for the HU values/intensities of your image or volume.&#x20;

To enable Masking, select any Object Label of type **Segmentation** in the left hand toolbar and click on **Restrict by pixel intensity** in the right hand Context Panel.&#x20;

With Masking enabled, you will only be able to create annotations within the range that you set, making it easy to avoid painting "outside the lines" of your target structure.

You can also use the **Threshold Range Selector**, which allows you to interactively define the bounds of your masking range. With the Range selector activated, `left click` any part of a viewport to include it in the range or `right click` to exclude it from the range. &#x20;

{% hint style="warning" %}
The pixel restriction will be applied as long as the masking filter is toggled ON. These settings are visible in the right hand Context Panel.
{% endhint %}
