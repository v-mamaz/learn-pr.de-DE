<span data-ttu-id="39588-101">In diesem Modul haben Sie erfahren, wie mit Warteschlangen in Azure-Speicherkonten Nachrichten zwischen Komponenten in einer verteilten Anwendung ausgetauscht werden.</span><span class="sxs-lookup"><span data-stu-id="39588-101">In this module, you've seen how queues in Azure storage accounts are used to pass messages between components in a distributed application.</span></span> <span data-ttu-id="39588-102">Dadurch kann die Zuverlässigkeit und Fehlerresilienz bei starker Auslastung erhöht werden.</span><span class="sxs-lookup"><span data-stu-id="39588-102">Using queues in this way can help to make a distributed application more reliable and resilient to failures and periods of high demand.</span></span> <span data-ttu-id="39588-103">Wenn Sie die Microsoft Azure Storage-Clientbibliothek für .NET verwenden, können Sie problemlos C#- oder VB.NET-Code schreiben, mit dem Warteschlangen erstellt oder diesen Warteschlangen Nachrichten hinzugefügt bzw. aus diesen abgerufen oder entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="39588-103">If you use the Microsoft Azure Storage Client Library for .NET, you can easily write C# or VB.NET code that creates queues, adds messages, or retrieves and removes messages from queues.</span></span>

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

<span data-ttu-id="39588-104">Wenn Sie in Ihrem eigenen Abonnement arbeiten, können Sie den folgenden Azure CLI-Befehl zum Löschen der Ressourcengruppe und aller zugehörigen Ressourcen ausführen.</span><span class="sxs-lookup"><span data-stu-id="39588-104">When you are working in your own subscription, you can execute the following Azure CLI command to delete the resource group and all associated resources.</span></span>

```azurecli
az group delete --name [resource-group-name] --yes --no-wait
```

<span data-ttu-id="39588-105">Die optionale Option `--no-wait` weist die Shell an, nicht auf den Abschluss des Vorgangs in Azure zu warten.</span><span class="sxs-lookup"><span data-stu-id="39588-105">The optional `--no-wait` option tells the shell to not wait for Azure to complete the operation.</span></span>