Sie haben Ihrer Anwendung die erforderlichen Clientbibliotheken hinzugefügt und können eine Verbindung mit Ihrem Azure-Speicherkonto herstellen.

Für Ihre App werden zwei Datenelemente benötigt, um mit Daten in einem Speicherkonto arbeiten zu können:

1. [Ein Zugriffsschlüssel](#access-key)
1. [Der REST-API-Endpunkt](#rest-endpoint)

<a name="access-key"></a>

## <a name="security-access-keys"></a>Sicherheitszugriffsschlüssel

Jedes Speicherkonto verfügt über zwei eindeutige _Zugriffsschlüssel_, die zum Schützen des Speicherkontos verwendet werden. Wenn Ihre App mit mehreren Speicherkonten eine Verbindung herstellen muss, benötigt sie für jedes Speicherkonto einen Zugriffsschlüssel.

![Eine Abbildung einer Anwendung, die mit zwei verschiedenen Speicherkonten in der Cloud verbunden ist. Auf jedes Speicherkonto kann mit einem eindeutigen Schlüssel zugegriffen werden.](..\media\6-multiple-accounts.png)

<a name="rest-endpoint"></a>

## <a name="rest-api-endpoint"></a>REST-API-Endpunkt

Zusätzlich zu Zugriffsschlüsseln für die Authentifizierung gegenüber Speicherkonten muss Ihre App über die Information verfügen, welche Speicherdienstendpunkte für die REST-Anforderungen ausgegeben werden sollen. 

Der REST-Endpunkt ist eine Kombination aus dem _Namen_ Ihres Speicherkontos, des Datentyps und einer bekannten Domäne. Beispiel:

| Datentyp | Beispiel für einen Endpunkt |
|-----------|------------------|
| Blobs     | `https://[name].blob.core.windows.net/` |
| Warteschlangen    | `https://[name].queue.core.windows.net/` |
| Tabelle     | `https://[name].table.core.windows.net/` |
| Dateien     | `https://[name].file.core.windows.net/` |

Wenn Sie eine benutzerdefinierte Domäne mit Azure verknüpft haben, können Sie auch eine benutzerdefinierte Domänen-URL für den Endpunkt erstellen.

## <a name="connection-strings"></a>Verbindungszeichenfolgen

Die einfachste Möglichkeit zum Verarbeiten dieser Informationen ist die Verwendung einer **Verbindungszeichenfolge für das Speicherkonto**. Eine Verbindungszeichenfolge enthält alle erforderlichen Konnektivitätsinformationen in nur einer Textzeichenfolge.

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
> Beachten Sie unbedingt, dass das Speichern dieser Informationen in einer Konfigurationsdatei gefährlich sein kann, wenn Sie diese Datei in die Quellcodeverwaltung einbeziehen und in einem öffentlichen Repository speichern. Dies ist ein häufiger Fehler und bedeutet, dass jeder Ihren Quellcode im öffentlichen Repository durchsuchen und Ihre Speicherkonto-Verbindungsinformationen finden kann.

Jedes Speicherkonto verfügt über zwei Zugriffsschlüssel. Dies ermöglicht eine Rotation (neue Generierung) der Schlüssel in regelmäßigen Abständen als Teil der bewährten Sicherheitsmethode zum Schutz Ihres Speicherkontos. Dieser Prozess kann über das Azure-Portal, die Azure CLI oder das PowerShell-Befehlszeilentool durchgeführt werden.

Bei der Rotation eines Schlüssels wird der ursprüngliche Schlüsselwert sofort ungültig und jeder Person, die den Schlüssel unberechtigterweise erhalten hat, wird der Zugriff entzogen. Bei der Unterstützung von zwei Schlüsseln können Sie die Schlüsselrotation ohne Ausfallzeiten in den Anwendungen, die die Schlüssel verwenden, durchführen. Während ein Schlüssel neu generiert wird, kann Ihre App zur Verwendung des anderen Zugriffsschlüssels wechseln. Wenn mehrere Ihrer Apps dieses Speicherkonto nutzen, sollten sie alle denselben Schlüssel verwenden, um diese Technik zu unterstützen. Die grundlegende Idee lautet wie folgt:

1. Aktualisieren Sie die Verbindungszeichenfolgen im Anwendungscode, damit sie auf den sekundären Zugriffsschlüssel des Speicherkontos verweisen.
2. Generieren Sie den primären Zugriffsschlüssel für Ihr Speicherkonto neu, indem Sie das Azure-Portal oder ein Befehlszeilentool verwenden.
3. Aktualisieren Sie die Verbindungszeichenfolgen in Ihrem Code, um auf den neuen primären Zugriffsschlüssel zu verweisen.
4. Generieren Sie den sekundären Zugriffsschlüssel auf die gleiche Weise neu.

> [!TIP]
> Es wird dringend empfohlen, Ihre Zugriffsschlüssel regelmäßig zu rotieren, um sicherzustellen, dass sie privat bleiben (vergleichbar mit dem Ändern Ihrer Kennwörter). Wenn Sie den Schlüssel in einer Serveranwendung nutzen, können Sie einen **Azure Key Vault** verwenden, um den Zugriffsschlüssel zu speichern. Key Vaults (Schlüsseltresore) verfügen über Unterstützung für das direkte Synchronisieren mit dem Speicherkonto und das regelmäßige automatische Rotieren der Schlüssel. Die Verwendung eines Schlüsseltresors sorgt für eine zusätzliche Sicherheitsebene, da für die App niemals direkt ein Zugriffsschlüssel verwendet werden muss.

### <a name="shared-access-signatures-sas"></a>Shared Access Signatures (SAS)

Zugriffsschlüssel sind der einfachste Ansatz zum Authentifizieren des Zugriffs auf ein Speicherkonto, aber sie ermöglichen den vollständigen Zugriff auf alle Daten des Speicherkontos – wie beim Stammkennwort eines Computers. 

Für Speicherkonten ist der separate Authentifizierungsmechanismus _Shared Access Signatures_ verfügbar, mit dem der Ablauf und eingeschränkte Berechtigungen für Szenarios unterstützt werden, in denen Sie eingeschränkten Zugriff gewähren müssen. Sie sollten diesen Ansatz verwenden, wenn Sie anderen Benutzern für Ihr Speicherkonto das Lesen und Schreiben von Daten erlauben möchten. Am Ende des Moduls sind Links zu unserer Dokumentation zu diesem anspruchsvolleren Thema angegeben.
