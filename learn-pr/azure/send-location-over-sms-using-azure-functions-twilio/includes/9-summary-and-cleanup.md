You've successfully created a cross-platform mobile app using Xamarin and an Azure function with a Twilio binding.

## Clean up
<!---TODO: Update for sandbox?--->

When you're done working with this Azure Functions application, you can delete all resources created during the tutorial from the Azure portal.

1. From Visual Studio, select *View->Cloud Explorer*.

1. From the drop-down at the top of this panel, select *Resource Groups*.

1. Expand the subscription that you used to create the resource group. Right-click on the "ImHere" resource group and select *Open in Portal*.

    ![Open the resource group in the portal from the cloud explorer window](../media-drafts/9-open-resource-group-in-portal.png)

1. Log into the Azure portal in your browser, if necessary.

1. The portal will open on the "ImHere" resource group. Click the **Delete Resource Group** button.

    ![Delete the resource group](../media-drafts/9-delete-resource-group.png)

1. Enter the name of the resource group to confirm the deletion and click **Delete**.

    ![Enter the resource group name to confirm the deletion](../media-drafts/9-confirm-delete-resource-group.png)

## Summary

In this module, you learned how to:

- Create a cross-platform Xamarin.Forms app that uses Xamarin.Essentials.
- Create a cross-platform UI using XAML with application logic in a ViewModel, as well as bind properties in a ViewModel to the UI.
- Detect the user's location.
- Create an Azure Function with an HTTP trigger and run it locally.
- Call an Azure Function from a mobile app, passing data as JSON.
- Bind an Azure Function to Twilio to send an SMS message.
- Publish an Azure Function to Azure.