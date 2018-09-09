In this module, you've seen how queues in Azure storage accounts are used to pass messages between components in a distributed application. Using queues in this way can help to make a distributed application more reliable and resilient to failures and periods of high demand. If you use the Microsoft Azure Storage Client Library for .NET, you can easily write C# or VB.NET code that creates queues, adds messages, or retrieves and removes messages from queues.

## Clean up the resources

Storage accounts that contain data can incur costs against your Azure subscription. The amounts of data we're using here are small - so it would be low, however it's always a good idea to remove all the resources.

Because you created all the resources in the same resource group, the easiest way to cleanup your Azure subscription is to remove the resource group that will remove all its contents:

```azurecli
az group delete --name ExerciseResources --yes --no-wait
```

The `--no-wait` option will let you move onto the next module without waiting for the command to complete.