In diesem Modul können Sie der app-Geheimnis-Konfiguration in Key Vault gesichert. Diesem app-Code authentifiziert in den Tresor mit verwalteter Dienstidentität Andautomatically Lasten die geheimen Schlüssel aus dem Tresor in ASP.NET Core-Konfigurationssystem beim Start.

## <a name="cleanup"></a>Cleanup

Um Ihr Azure-Abonnement zu bereinigen, führen Sie Folgendes in die Cloud-Shell, um die Ressourcengruppe, die mit den in diesem Modul erstellten Ressourcen löschen.

```console
az group delete --name keyvault-exercise-group
```

Um Ihre Cloud Shell-Speicher zu bereinigen, löschen Sie die `KeyVaultDemoApp` Verzeichnis.

## <a name="next-steps"></a>Nächste Schritte

Wenn dies eine echte app war, würde was als Nächstes getan?

* Fügen Sie alle Ihre app-Geheimnisse in Ihren Tresoren! Es ist nicht mehr aus irgendeinem Grund, um diese in Konfigurationsdateien zu erhalten.
* Fahren Sie mit der Entwicklung der Anwendung. Unsere produktionsumgebung ist alle eingerichtet, damit für künftige Bereitstellungen, wir nicht alle Setup wiederholt werden soll müssen.
* Zum unterstützen der Entwicklung eines Entwicklungsumgebung Tresors enthält, geheime Schlüssel, mit dem gleichen Namen, aber unterschiedliche Werte. Gewähren von Berechtigungen für das Entwicklungsteam, und konfigurieren Sie den Namen des schlüsseltresors, in der app-Entwicklungsumgebung-Konfigurationsdatei. Wenn Entwickler die app lokal ausführen `AddAzureKeyVault` erkennt automatisch lokale Installationen von Visual Studio und der Azure-Befehlszeilenschnittstelle und Azure-Anmeldeinformationen konfiguriert, die in diesen Anwendungen anmelden und Zugriff auf den Tresor verwenden.
* Erstellen Sie zusätzliche Umgebungen für Zwecke wie Benutzerakzeptanztests.
* Separate Tresore in verschiedenen Abonnements und/oder Ressourcengruppen, um sie zu isolieren.
* Gewähren des Zugriffs auf die richtigen Personen andere Umgebung-Tresore.

## <a name="further-reading"></a>Weitere Informationen

* [Key Vault-Dokumentation](https://docs.microsoft.com/azure/key-vault/)
* [Weitere Informationen zu `AddAzureKeyVault` und erweiterte Optionen](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)
* [In diesem Tutorial](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application) führt durch die Verwendung `KeyVaultClient`, u. a. die Authentifizierung sie manuell in Azure Active Directory-MSI-Datei anstelle ein geheimen clientschlüssels
* [MSI-Tokendienst Dokumentation](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol)für den Workflow der Authentifizierung selbst implementieren.