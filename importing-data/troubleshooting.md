# Troubleshooting

This section covers troubleshooting issues with data loading in the Annotation Tool. If there is an error in loading your data, you will encounter something very similar to the following:&#x20;

<figure><img src="../.gitbook/assets/Frame 27495 (1).png" alt=""><figcaption><p>A typical 404 error</p></figcaption></figure>

## General Troubleshooting Walkthrough with Example

Data can fail to load for a variety of reasons, from network issues to invalid file pathing to incompatible image headers and more.

Let's walk through some basic steps using the example above that will help you determine how to best troubleshoot an error.

1. **Check for specific information** - you may have a specific error message under **Failed to load image**, such as in the example above - "Request failed with status code 404". The error messages that RedBrick AI generates for you can provide valuable insight into why your data is not loading.&#x20;

In this example, a 404 error, or a "Not Found" error, likely means you have an issue with your [external storage integration](import-cloud-data/creating-an-items-list.md) or internet connection.&#x20;

2. **Use the context you have** - RedBrick AI displays a 404 error when you attempt to open an image/volume that RedBrick AI can't find, which typically implies that:
   1. There is an issue with your **file path**, i.e. you're asking RedBrick to open something that doesn't actually exist in that specific location;
   2. There is an issue with the **image/volume itself,** i.e. you're asking RedBrick to access a file that may have been renamed, moved, deleted, etc.;
   3. There is an issue with your **network**, i.e. your internet connection was disrupted or failed while you were trying to load the image/volume;
   4. There is an issue with your **integration**, i.e. there's something wrong with the configuration of your external storage.&#x20;

{% hint style="success" %}
Your admins can verify the validity of any Storage Method on the [Storage Page](https://docs.redbrickai.com/importing-data/import-cloud-data#configuring-cloud-storage).
{% endhint %}

2. **Escalate appropriately** - in the case of our 404 error, it may be best to reach out to a Team Lead to verify that all files were correctly uploaded to your Project.

### Contacting RedBrick AI Support

If you don't have a specific error message to work with or would simply like RedBrick AI's Support Team to investigate, we're always standing by to help!

You can either email us at support@redbrickai.com or click on the Help Button, and then on **Email support**.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

#### Common Information to Include in an Email to RBAI Support

When emailing RedBrick AI's Support Team, please include as much context as you can so that we can get to work right away! Some things that will help often include:

1. **The Task URL** - the URL of the Task that is failing to load. This URL contains the ID of both the Task itself and the Project that the Task is located in;
2. **The Error** - A screenshot of the error message (or a copy/pasted version of the content of the error message);
3. **Additional Context (for technical users)-**  screenshots or logs from the Console or Network tabs of Developer Tools, where applicable;

### Continuing Work

If you'd simply prefer to continue work on other Tasks, you have several options.

**Raise Issue** - if you'd like to inform your Admin of an issue within RedBrick AI, you can click on the **Raise Issue** button. This will remove the Task from your Labeling Queue, preventing it from appearing over and over again while you work. You can learn more about [raising an Issue here](../projects/comments-and-raised-issues.md). Once you raise an Issue, you will automatically be presented with the next Task in your Labeling Queue;

If you don't want to raise an Issue, you can simply navigate to another Task in your queue by either:

1. clicking on another Task **at the bottom of the error screen**, or
2. backing out of the Annotation Tool and selecting another Task.

### Other Situational Troubleshooting Tips

#### Error Message: Failed to load these URLs

If you're using an external Storage Method and can see URLs listed under the "Failed to load these URLs" message, try opening the link in your browser.&#x20;

If the browser loads a screen with an error message, there is likely an **issue with your Storage Method integration** (possibly your bucket name or access keys).&#x20;

#### CORS Configuration Error

If you are seeing a data file is being downloaded but not displayed, it's likely that your team **has not not enabled CORS on your storage method**. If CORS is not enabled on your storage method, your browser will not be able to load the image (as it comes from[ a different origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)_)._
