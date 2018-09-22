In diesem Modul haben Sie erfahren, wie Azure Blob Storage zum Speichern von Webanwendungsdaten verwendet wird. Wir haben Tipps für die Entwicklung einer Strategie zur Verwendung von Blob Storage in einer Web-App und des Azure Storage SDK für .NET Core zum Schreiben und Lesen von Blobs diskutiert. Die von uns erstellte App akzeptiert von Benutzern hochgeladene Dateien, speichert sie in Blob Storage und stellt sie zum Download bereit.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

Löschen Sie zum Bereinigen Ihres Cloud Shell-Speichers das Verzeichnis `mslearn-store-data-in-azure`.

<!---TODO: Remove further reading
## Further reading

- **Securely storing secrets like connection strings**: The most robust end-to-end solution for storing secret configuration values is Azure Key Vault. See [here](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) for information about using Key Vault in an ASP.NET Core application. Alternatively, you can safely store connection strings in App Service application settings and use the [ASP.NET Core Secret Manager tool](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) to support developer environments.
- [Uploading large files with streaming in ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
- [Blob concurrency: AccessConditions and blob leases](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
- [Granting limited access to Azure Storage object with shared access signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
- [Indexing Blob storage with Azure Search](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
- [Container and blob name restrictions](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)
--->