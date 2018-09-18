In diesem Modul haben Sie erfahren, wie Azure Blob Storage zum Speichern von Webanwendungsdaten verwendet wird. Wir haben Tipps für die Entwicklung einer Strategie zur Verwendung von Blob Storage in einer Web-App und des Azure Storage SDK für .NET Core zum Schreiben und Lesen von Blobs diskutiert. Die von uns erstellte App akzeptiert von Benutzern hochgeladene Dateien, speichert sie in Blob Storage und stellt sie zum Download bereit.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Um Ihr Azure-Abonnement zu bereinigen, führen Sie die folgenden Schritte in Azure Cloud Shell aus, um die Ressourcengruppe zu löschen, die alle in diesem Modul erstellten Ressourcen enthält.

```console
az group delete --name blob-exercise-group --yes --no-wait
```

Löschen Sie zum Bereinigen Ihres Cloud Shell-Speichers das Verzeichnis `mslearn-store-data-in-azure`.

## <a name="further-reading"></a>Weitere nützliche Informationen

- **Sicheres Speichern von Geheimnissen wie z.B. Verbindungszeichenfolgen**: Die zuverlässigste Komplettlösung zur Speicherung von Konfigurationswerten für Geheimnisse ist Azure Key Vault. [Hier](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) finden Sie Informationen zur Verwendung von Key Vault in einer ASP.NET Core-Anwendung. Alternativ können Sie Verbindungszeichenfolgen sicher in App Service-Anwendungseinstellungen speichern und das Tool [ASP.NET Core Secret Manager ](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) zur Unterstützung von Entwicklungsumgebungen verwenden.
- [Hochladen großer Dateien per Streaming in ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
- [Parallelität von Blobs: AccessConditions und Leases von Blobs](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
- [Gewähren eines eingeschränkten Zugriffs auf ein Azure Storage-Objekt mit Shared Access Signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
- [Indizieren von Blob Storage mit Azure Search](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
- [Einschränkungen von Container- und Blobnamen](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)