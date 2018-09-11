Sie haben Ihrer Anwendung die erforderlichen Clientbibliotheken hinzugefügt und können eine Verbindung mit Ihrem Azure Storage-Konto herstellen. Aber wie kann Ihre App wissen, mit welchem Konto sie eine Verbindung herstellen soll, und in welcher Region das Speicherkonto vorhanden ist? Ohne entsprechende Konfiguration weiß Ihre App nicht, wie sie eine Verbindung mit Ihrem Azure Storage-Konto herstellen soll. 

Sie finden die Informationen zum Herstellen der Verbindung mit dem Speicherkonto im Azure-Portal und nehmen sie in Ihre Anwendungskonfiguration auf, sodass Ihre App bereit ist, die Verbindung mit Ihrem Azure Storage-Konto herzustellen.

## <a name="access-keys"></a>Zugriffsschlüssel

Jedes Speicherkonto verfügt über einen Satz von Zugriffsschlüsseln, die Zugriff auf das Speicherkonto ermöglichen. Wenn Ihre App mit mehreren Speicherkonten eine Verbindung herstellen muss, benötigt sie für jedes Speicherkonto Zugriffsschlüssel.

![mehrere Konten](..\media-draft\7-multiple-accounts.png)

Da Azure ein Cloudanbieter ist, benötigt Ihre App nicht nur Zugriffsschlüssel für die Authentifizierung bei Speicherkonten, sondern muss auch die Speicherdienstendpunkte kennen, die Zugriff auf Ihr Speicherkonto über das Internet ermöglichen. Die einfachste Möglichkeit zum Verarbeiten dieser Informationen ist die Verwendung der Verbindungszeichenfolge für das Speicherkonto, die alle erforderlichen Konnektivitätsinformationen enthält.

Azure Storage-Verbindungszeichenfolgen ähneln dem folgenden Beispiel – abgesehen von Zugriffsschlüssel und Kontoname, die für Ihr Speicherkonto spezifisch sind:

```csharp
DefaultEndpointsProtocol=https;AccountName={your-storage};AccountKey={your-access-key};EndpointSuffix=core.windows.net
```

## <a name="security"></a>Sicherheit

Zugriffsschlüssel sind entscheidend für den Zugriff auf Ihr Speicherkonto und dürfen daher nicht für Systeme oder Personen bereitgestellt werden, die keinen Zugriff auf Ihr Speicherkonto haben sollen. Zugriffsschlüssel entsprechen dem Benutzernamen und dem Kennwort, die zum Zugriff auf Ihren Computer erforderlich sind.

![Schlüssel im Tresor](..\media-draft\8-keys-vault.png)

Informationen zur Speicherkonto-Konnektivität werden in der Regel in einer Umgebungsvariablen, Datenbank oder Konfigurationsdatei gespeichert.

Beachten Sie unbedingt, dass das Speichern dieser Informationen in einer Konfigurationsdatei auch gefährlich sein kann, wenn Sie diese Datei in die Quellcodeverwaltung einbeziehen und in einem öffentlichen Repository speichern. Dies ist ein häufiger Fehler und bedeutet, dass jeder Ihren Quellcode im öffentlichen Repository durchsuchen und Ihre Speicherkonto-Verbindungsinformationen finden kann.

Für Speicherkonten ist der separate Authentifizierungsmechanismus Shared Access Signatures verfügbar, der Ablauf und eingeschränkte Berechtigungen für Szenarios unterstützt, in denen Sie eingeschränkten Zugriff gewähren müssen. Zwar wird dieses Thema hier nicht behandelt, und Kenntnisse darüber sind für dieses Modul nicht erforderlich, aber weitere Informationen finden Sie [hier](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1).

Jedes Speicherkonto verfügt über zwei Zugriffsschlüssel. Dies ermöglicht eine Rotation (neue Generierung) der Schlüssel in regelmäßigen Abständen als Teil der bewährten Sicherheitsmethode zum Schutz Ihres Speicherkontos. Dieser Vorgang kann im Azure-Portal oder über die CLI erfolgen.

Bei der Rotation eines Schlüssels wird der ursprüngliche Schlüsselwert sofort ungültig und jeder Person, die den Schlüssel unberechtigterweise erhalten hat, der Zugriff entzogen. Bei der Unterstützung von zwei Schlüsseln können Sie die Schlüsselrotation ohne Ausfallzeiten in den Anwendungen, die die Schlüssel verwenden, durchführen. Während ein Schlüssel neu generiert wird, kann Ihre App zur Verwendung des anderen Zugriffsschlüssels wechseln. Wenn mehrere Ihrer Apps dieses Speicherkonto verwenden, sollten sie alle denselben Schlüssel verwenden, um diese Technik zu unterstützen. Weitere Informationen finden Sie [hier](https://docs.microsoft.com/en-us/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys).

## <a name="advanced-security-options"></a>Erweiterte Sicherheitsoptionen

Azure bietet einen leistungsstarken Sicherheitsspeicher namens Azure Key Vault, der zum sicheren Speichern von Geheimnissen in jeder Form wie Zugriffsschlüssel, Kennwörter oder Zertifikate konzipiert ist. Mit diesem Feature können Sie Ihre Zugriffsschlüssel sicher speichern und automatisch rotieren.

Dieses Feature liegt nicht im Bereich dieses Moduls, aber weitere Informationen finden Sie [hier](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-storage-keys).

## <a name="summary"></a>Zusammenfassung

Um eine Verbindung mit einem Azure Storage-Konto herzustellen, benötigen Sie zwei Dinge: Einen Zugriffsschlüssel, der mit einem Benutzernamen und Kennwort vergleichbar ist und vertraulich behandelt werden sollte. Außerdem benötigen Sie einen Speicherdienst-Endpunkt, der durch eine Verbindungszeichenfolge dargestellt wird.

