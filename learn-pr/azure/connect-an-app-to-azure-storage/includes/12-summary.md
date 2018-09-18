Sie haben gelernt, wie ein Azure-Speicherkonto erstellt und eine Verbindung damit hergestellt wird. Sie haben eine einfache Anwendung zum Herstellen einer Verbindung mit einem Speicherkonto und zum Erstellen eines Blobcontainers geschrieben. Diese Kenntnisse werden in anderen Modulen in diesem Lernpfad als Basis verwendet, um Ihnen zu zeigen, wie Blob Storage und Warteschlangen zum Speichern von Daten und Verbinden von Apps verwendet werden.

Wir haben nur Beispiele für JavaScript und C# verwendet, aber Azure unterstützt eine Vielzahl anderer Sprachen. Auf der offiziellen [Dokumentationsseite zu SDKs/Tools](https://docs.microsoft.com/azure/#pivot=sdkstools) finden Sie die offizielle Liste von Links zu den Clientbibliotheken für sämtliche derzeit unterstützte Sprachen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Referenz zur REST-API von Azure Storage-Diensten](https://docs.microsoft.com/rest/api/storageservices/)
- [Verwenden von Shared Access Signatures (SAS) für begrenzten Zugriff auf ein Speicherkonto](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
- [Verwalten von Geheimnissen mit Azure Key Vault](https://docs.microsoft.com/learn/modules/manage-secrets-with-azure-key-vault/)
- [Verwenden von Azure Key Vault-Speicherkontoschlüsseln mit Server-Apps](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-storage-keys)
- [Quellcode für die Azure SDKs für .NET](https://github.com/Azure/azure-sdk-for-net)
- [Azure-Speicherclientbibliothek für JavaScript](https://github.com/Azure/azure-storage-node#azure-storage-javascript-client-library-for-browsers)

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Es ist eine gute Idee, Ihre Ressourcen in Azure zu bereinigen, wenn Sie mit ihnen fertig sind. Bei Verwendung der kostenlosen Sandbox ist dieser Schritt nicht erforderlich, aber in Ihren eigenen Abonnements sollten Sie nicht verwendete Ressourcen löschen, um unnötige Gebühren zu vermeiden. Am Einfachsten löschen Sie hierzu die Ressourcengruppe, in der Sie sämtliche Ressourcen platziert haben. Dies kann über das Azure-Portal oder mithilfe der Befehlszeile erfolgen.