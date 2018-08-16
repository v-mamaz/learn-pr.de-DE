Sie haben erfolgreich eine voll funktionsfähige, serverlose Anwendung, die mit Azure-Diensten erstellt werden.

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Wenn Sie fertig sind arbeiten mit dieser Anwendung können Sie den folgenden Befehl auf um alle während des Tutorials erstellte Ressourcen zu löschen:

```azurecli
az group delete --name first-serverless-app
```

Geben Sie `y` ein, wenn Sie dazu aufgefordert werden.  

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie Folgendes gelernt:
> [!div class="checklist"]
> * Konfigurieren Sie Azure Blob Storage zum Hosten einer statischen Website und hochgeladene Bilder.
> * Hochladen von Bildern in Azure Blob Storage mit Azure Functions.
> * Ändern der Bildgröße mithilfe von Azure Functions.
> * Store Bildmetadaten in Azure Cosmos DB.
> * Verwenden Sie Cognitive Services-maschinelles sehen-API, um das Image Untertitel automatisch generieren.
> * Verwenden Sie Azure Active Directory, um die Web-app zu sichern, indem Sie die Authentifizierung von Benutzern.

Informationen zur Verbindung mit Funktionen noch weitere Dienste, weiterhin mit dem Logik-Apps-Tutorial. 

> [!div class="nextstepaction"]
> [Functions mit Logic Apps](https://docs.microsoft.com/azure/azure-functions/functions-twitter-email)