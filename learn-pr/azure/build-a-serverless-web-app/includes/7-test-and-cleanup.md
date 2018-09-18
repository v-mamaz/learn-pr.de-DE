Sie haben mithilfe von Azure-Diensten eine serverlose Anwendung mit vollem Funktionsumfang erstellt.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox--->

Wenn Sie die Arbeit mit dieser Anwendung beendet haben, können Sie mit dem folgenden Befehl alle im Tutorial erstellten Ressourcen löschen:

```azurecli
az group delete --name first-serverless-app
```

Geben Sie `y` ein, wenn Sie dazu aufgefordert werden.  

## <a name="next-steps"></a>Nächste Schritte

In diesem Artikel haben Sie Folgendes gelernt:
  - Konfigurieren von Azure Blob Storage zum Hosten einer statischen Website und von hochgeladenen Bildern
  - Hochladen von Bildern in Azure Blob Storage mit Azure Functions
  - Ändern der Größe von Bildern mit Azure Functions
  - Speichern von Imagemetadaten in Azure Cosmos DB 
  - Verwenden der Maschinelles Sehen-API von Cognitive Services zum automatischen Generieren von Bildtiteln
  - Nutzen von Azure Active Directory zum Schützen der Web-App durch das Authentifizieren von Benutzern.

Fahren Sie mit dem Tutorial [Erstellen einer Funktion, die in Azure Logic Apps integriert ist](https://docs.microsoft.com/azure/azure-functions/functions-twitter-email) fort, wenn Sie noch mehr Dienste mit Functions verbinden möchten.