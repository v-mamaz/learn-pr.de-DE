Mithilfe von Azure Event Hubs können Big Data-Anwendungen große Datenmengen verarbeiten. Außerdem besteht zu Zeiten hoher Bedarfsanforderungen die Möglichkeit einer horizontalen Hochskalierung. Azure Event Hubs entkoppelt das Senden und Empfangen von Nachrichten, um die Datenverarbeitung zu verwalten. Dadurch wird das Risiko verringert, dass Consumeranwendungen überladen sind und aufgrund von ungeplanten Unterbrechungen Daten verloren gehen.

In diesem Modul haben Sie erfahren, wie Sie Azure Event Hubs als Teil einer Lösung zur Ereignisverarbeitung bereitstellen können. Es wurde Folgendes vermittelt:

- Das Verwenden der Azure CLI zum Erstellen eines Event Hubs-Namespace und eines darin enthaltenen Event Hubs 
- Das Konfigurieren von Absender- und Empfängeranwendungen zum Senden und Empfangen von Nachrichten über den Event Hub
- Das Verwenden des Azure-Portals zum Anzeigen des Status und der Leistung eines Event Hubs

## <a name="clean-up"></a>Bereinigen 
<!---TODO: Update for sandbox?--->

Aufgrund der Ressourcen, die Sie zum Testen Ihres Event Hubs verwendet haben, fallen Kosten für Ihr Abonnement an. Wenn Sie den Event Hub nicht mehr verwenden, sollten Sie ihn entfernen, damit keine unnötigen Änderungen an ihm vorgenommen werden können.

Da Sie den Hub, den Namespace und den Speicher in nur einer Ressourcengruppe erstellt haben, können Sie Ihr Azure-Abonnement am einfachsten bereinigen, indem Sie die Ressourcengruppe entfernen, die wiederum all ihre Inhalte entfernt. 

Führen Sie den folgenden Befehl aus, um die Ressourcengruppe, den Namespace, das Speicherkonto und alle zugehörigen Ressourcen zu entfernen. Ersetzen Sie `myResourceGroup` durch die weiter oben erstellte Ressourcengruppe:

```azurecli
az group delete --resource-group myResourceGroup
```

Wenn Sie aufgefordert werden, den Löschvorgang zu bestätigen, klicken Sie auf **Ja**.

Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen.
