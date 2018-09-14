Sie haben Ihrer Anwendung die erforderlichen Clientbibliotheken hinzugefügt und können eine Verbindung mit Ihrem Azure-Speicherkonto herstellen.

Um mit Daten in einem Speicherkonto arbeiten, ist Ihre app zwei Datenelemente erforderlich:

1. Zugriffstaste
1. Der REST-API-Endpunkt

## <a name="security-access-keys"></a>Security-Zugriffsschlüssel

Jedes Speicherkonto verfügt über zwei eindeutige _Zugriffsschlüssel_ , die zum Schutz des Storage-Kontos verwendet werden. Wenn Ihre app mit mehrere Speicherkonten verbinden muss, wird Ihre app einen Zugriffsschlüssel für jedes Speicherkonto benötigen.

![Eine Abbildung, die mit einer Anwendung mit zwei unterschiedlichen Speicherkonten in der Cloud verbunden ist. Jedes Speicherkonto kann mit einem eindeutigen Schlüssel zugegriffen werden.](..\media\6-multiple-accounts.png)

## <a name="rest-api-endpoint"></a>REST-API-Endpunkt

Zusätzlich zu den Zugriffsschlüssel für die Authentifizierung bei Speicherkonten müssen Ihre app wissen, die Speicher-Dienstendpunkte, die REST-Anforderungen ausgeben kann. 

Der REST-Endpunkt ist eine Kombination aus Ihrem Speicherkonto _Namen_, den Datentyp und einer bekannten Domäne. Beispiel:

| Datentyp | Beispiel für einen Endpunkt |
|-----------|------------------|
| Blobs (in englischer Sprache)     | `https://[name].blob.core.windows.net/` |
| Warteschlangen    | `https://[name].queue.core.windows.net/` |
| Table     | `https://[name].table.core.windows.net/` |
| Dateien     | `https://[name].file.core.windows.net/` |

Wenn Sie eine benutzerdefinierte Domäne mit Azure verknüpft haben, können Sie auch eine benutzerdefinierte Domänen-URL für den Endpunkt erstellen.

## <a name="connection-strings"></a>Verbindungszeichenfolgen

Die einfachste Möglichkeit zum Verarbeiten dieser Informationen ist die Verwendung einer **Speicherkonto-Verbindungszeichenfolge**. Eine Verbindungszeichenfolge enthält, dass alle Verbindungsinformationen in einer einzelnen Textzeichenfolge benötigt.

Azure Storage-Verbindungszeichenfolgen ähneln dem folgenden Beispiel – abgesehen von Zugriffsschlüssel und Kontoname, die für Ihr Speicherkonto spezifisch sind:

```
DefaultEndpointsProtocol=https;AccountName={your-storage};
   AccountKey={your-access-key};
   EndpointSuffix=core.windows.net
```

## <a name="security"></a>Sicherheit

Zugriffsschlüssel sind entscheidend für den Zugriff auf Ihr Speicherkonto und dürfen daher nicht für Systeme oder Personen bereitgestellt werden, die keinen Zugriff auf Ihr Speicherkonto haben sollen. Zugriffsschlüssel entsprechen dem Benutzernamen und dem Kennwort, die zum Zugriff auf Ihren Computer erforderlich sind.

Informationen zur Speicherkonto-Konnektivität werden in der Regel in einer Umgebungsvariablen, Datenbank oder Konfigurationsdatei gespeichert.

> [!IMPORTANT]
> Es ist wichtig zu beachten, dass das Speichern dieser Informationen in einer Konfigurationsdatei gefährlich sein kann, wenn Sie diese Datei in der quellcodeverwaltung enthalten und in einem öffentlichen Repository speichern. Dies ist ein häufiger Fehler und bedeutet, dass jeder Ihren Quellcode im öffentlichen Repository durchsuchen und Ihre Speicherkonto-Verbindungsinformationen finden kann.

Jedes Speicherkonto verfügt über zwei Zugriffsschlüssel. Dies ermöglicht eine Rotation (neue Generierung) der Schlüssel in regelmäßigen Abständen als Teil der bewährten Sicherheitsmethode zum Schutz Ihres Speicherkontos. Dieser Prozess kann erfolgen über das Azure-Portal oder die Azure-Befehlszeilenschnittstelle / PowerShell-Befehlszeilentools.

Bei der Rotation eines Schlüssels wird der ursprüngliche Schlüsselwert sofort ungültig und jeder Person, die den Schlüssel unberechtigterweise erhalten hat, der Zugriff entzogen. Bei der Unterstützung von zwei Schlüsseln können Sie die Schlüsselrotation ohne Ausfallzeiten in den Anwendungen, die die Schlüssel verwenden, durchführen. Mit den anderen Zugriffsschlüssel während der andere Schlüssel neu generiert wird, kann Ihre app wechseln. Wenn mehrere Ihrer Apps dieses Speicherkonto verwenden, sollten sie alle denselben Schlüssel verwenden, um diese Technik zu unterstützen. Hier ist die grundlegende Idee:

1. Aktualisieren Sie die Verbindungszeichenfolgen im Anwendungscode, damit sie auf den sekundären Zugriffsschlüssel des Speicherkontos verweisen.
2. Generieren Sie den primären Zugriffsschlüssel für Ihr Speicherkonto mit dem Azure-Portal oder über die Befehlszeile das Tool neu.
3. Aktualisieren Sie die Verbindungszeichenfolgen in Ihrem Code, um auf den neuen primären Zugriffsschlüssel zu verweisen.
4. Generieren Sie den sekundären Zugriffsschlüssel auf die gleiche Weise neu.

> [!TIP]
> Es wird dringend empfohlen, dass Sie in regelmäßigen Abständen der Zugriffsschlüssel rotieren, um sicherzustellen, dass sie genau, wie Sie Ihre Kennwörter ändern privat bleiben. Wenn Sie den Schlüssel in einer Serveranwendung verwenden, können Sie mithilfe einer **Azure Key Vault** um den Zugriffsschlüssel für Sie zu speichern. Key Vault-Instanzen umfassen, Support, um direkt mit dem Storage-Konto synchronisieren und automatisch die Schlüssel in regelmäßigen Abständen zu rotieren. Mit einem Key Vault bietet eine zusätzliche Sicherheitsschicht, damit Ihre app niemals direkt mit einer Zugriffstaste arbeiten muss.

### <a name="shared-access-signatures-sas"></a>Shared Access Signatures (SAS)

Zugriffsschlüssel sind der einfachste Ansatz für die Authentifizierung des Zugriffs auf ein Speicherkonto. Aber sie Vollzugriff auf alle Elemente in das Speicherkonto an, wie ein Stammkennwort auf einem Computer bieten.

Speicherkonten bieten einen separaten Authentifizierungsmechanismus namens _von shared Access Signatures_ , Ablauf- und eingeschränkte Berechtigungen zu unterstützen, für Szenarien, in dem Sie eingeschränkten Zugriff gewähren möchten. Sie sollten diesen Ansatz verwenden, wenn Sie andere Benutzer zu lesen und Schreiben von Daten in Ihrem Storage-Konto erlauben. Es sind Links zu unserer Dokumentation zu diesem erweiterten Thema am Ende des Moduls.
