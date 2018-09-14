In diesem Modul haben Sie die Konfiguration des Geheimnisses einer App in Azure Key Vault gesichert. Unser App-Code authentifiziert sich mit der verwalteten Identität beim Tresor und lädt beim Start automatisch die Geheimnisse aus dem Tresor in das ASP.NET Core-Konfigurationssystem.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Führen Sie die folgenden Schritte in Azure Cloud Shell aus, um die Ressourcengruppe zu löschen, die alle Ressourcen enthält, die wir in diesem Modul erstellt haben, um so Ihr Azure-Abonnement zu bereinigen.

```console
az group delete --name keyvault-exercise-group
```

Löschen Sie zum Bereinigen Ihres Cloud Shell-Speichers das Verzeichnis `KeyVaultDemoApp`.

## <a name="next-steps"></a>Nächste Schritte

Wenn dies eine echte App wäre, wie würde es weitergehen?

- Speichern Sie all Ihre App-Geheimnisse in Ihren Tresoren! Es gibt keinen Grund mehr, sie in Konfigurationsdateien zu speichern.
- Fahren Sie mit der Entwicklung der Anwendung fort. Ihre Produktionsumgebung ist vollständig eingerichtet, Sie müssen die Einrichtung also für zukünftige Bereitstellungen nicht erneut durchführen.
- Um die Entwicklung zu unterstützen, erstellen Sie einen Tresor für die Entwicklungsumgebung, der Geheimnisse mit den gleichen Namen, aber unterschiedlichen Werten enthält. Gewähren Sie dem Entwicklungsteam Berechtigungen, und konfigurieren Sie den Namen des Tresors in der Konfigurationsdatei für die Entwicklungsumgebung der App. Wenn Entwickler die App lokal ausführen, erkennt `AddAzureKeyVault` lokale Installationen von Visual Studio und der Azure CLI automatisch und verwendet die in diesen Anwendungen konfigurierten Azure-Anmeldeinformationen, um sich beim Tresor anzumelden und darauf zuzugreifen.
- Erstellen Sie weitere Umgebungen für andere Zwecke, beispielsweise für Benutzerakzeptanztests.
- Trennen Sie Tresore verschiedener Abonnements und/oder Ressourcengruppen, um sie voneinander zu isolieren.
- Gewähren Sie den richtigen Personen Zugriff auf andere Umgebungstresore.

## <a name="further-reading"></a>Weitere nützliche Informationen

- [Dokumentation zu Key Vault](https://docs.microsoft.com/azure/key-vault/)
- [Weitere Informationen zu AddAzureKeyVault und den erweiterten Optionen](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)
- [Dieses Tutorial](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application) führt durch die Verwendung von `KeyVaultClient` und erläutert die manuelle Authentifizierung bei Azure Active Directory mithilfe eines Clientgeheimnisses anstelle einer verwalteten Identität.
- In der [Dokumentation zu verwalteten Identitäten für den Tokendienst für Azure-Ressourcen](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol) finden Sie weitere Informationen zur Implementierung des Authentifizierungsworkflows.