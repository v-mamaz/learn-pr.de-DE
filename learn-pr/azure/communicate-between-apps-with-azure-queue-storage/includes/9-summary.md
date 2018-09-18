In diesem Modul haben Sie erfahren, wie mit Warteschlangen in Azure-Speicherkonten Nachrichten zwischen Komponenten in einer verteilten Anwendung ausgetauscht werden. Dadurch kann die Zuverlässigkeit und Fehlerresilienz bei starker Auslastung erhöht werden. Wenn Sie die Microsoft Azure Storage-Clientbibliothek für .NET verwenden, können Sie problemlos C#- oder VB.NET-Code schreiben, mit dem Warteschlangen erstellt oder diesen Warteschlangen Nachrichten hinzugefügt bzw. aus diesen abgerufen oder entfernt werden.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

Wenn Sie in Ihrem eigenen Abonnement arbeiten, können Sie den folgenden Azure CLI-Befehl zum Löschen der Ressourcengruppe und aller zugehörigen Ressourcen ausführen.

```azurecli
az group delete --name [resource-group-name] --yes --no-wait
```

Die optionale Option `--no-wait` weist die Shell an, nicht auf den Abschluss des Vorgangs in Azure zu warten.