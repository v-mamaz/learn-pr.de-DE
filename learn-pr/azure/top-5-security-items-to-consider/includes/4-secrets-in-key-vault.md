Geheimnisse, die mit allen geteilt werden, sind keine Geheimnisse. Wenn Sie vertrauliche Informationen wie Verbindungszeichenfolgen, Sicherheitstoken, Zertifikate und Kennwörter in Ihrem Code speichern, lädt das geradezu zum Missbrauch ein. Es empfiehlt sich auch nicht, solche Daten in Ihrer Webkonfiguration zu speichern, da dadurch quasi jeder, der Zugriff auf den Quellcode oder Webserver hat, auf Ihre privaten Daten zugreifen kann.

Geheimnisse sollten daher immer in **Azure Key Vault** platziert werden.

## <a name="what-is-azure-key-vault"></a>Was ist Azure Key Vault?
Azure Key Vault ist ein *Geheimnisspeicher* – ein zentraler Clouddienst zum Speichern von Anwendungsgeheimnissen. Zum Schutz Ihrer vertraulichen Daten speichert Key Vault Anwendungsgeheimnisse an einem zentralen Ort und bietet sicheren Zugriff, eine Berechtigungssteuerung und eine Zugriffsprotokollierung.

Geheimnisse werden in einzelnen *Tresoren* mit jeweils eigenen Konfigurations- und Sicherheitsrichtlinien für die Zugriffssteuerung gespeichert. Der Zugriff auf die Daten kann über eine REST-API oder über ein für die meisten Sprachen verfügbares Client-SDK erfolgen.

> [!IMPORTANT]
> **Key Vault dient zum Speichern von Konfigurationsgeheimnissen für Serveranwendungen.** Es dient nicht zum Speichern von Daten, die zu den Benutzern Ihrer App gehören, und sollte nicht im clientseitigen Teil einer App verwendet werden. Dies spiegelt sich in seinen Leistungsmerkmalen, seiner API und seinem Kostenmodell wieder.
>
> Benutzerdaten sollten an anderer Stelle gespeichert werden, z.B. in einer Azure SQL-Datenbank mit Transparent Data Encryption, oder auf einem Speicherkonto mit Speicherdienstverschlüsselung. Geheimnisse, die von Ihrer Anwendung verwendet werden, um auf diese Datenspeicher zuzugreifen, können in Key Vault gespeichert werden.

## <a name="why-use-a-key-vault-for-my-secrets"></a>Argumente für die Speicherung von Geheimnissen in Key Vault

Manuelle Verfahren für die Schlüsselverwaltung und das Speichern von Geheimnissen sind potenziell kompliziert und fehleranfällig. Beim manuellen Rotieren von Zertifikaten stehen diese wahrscheinlich für einige Stunden (oder Tage) nicht zur Verfügung. Wie eingangs bereits erwähnt: Wenn Sie Ihre Verbindungszeichenfolgen in Ihrer Konfigurationsdatei oder in einem Coderepository speichern, besteht die Gefahr, dass Dritte an Ihre Anmeldeinformationen gelangen.

Mit Key Vault können Benutzer Verbindungszeichenfolgen, Geheimnisse, Kennwörter, Zertifikate, Zugriffsrichtlinien, Dateisperren (zur Aktivierung des Schreibschutzes für Elemente in Azure) und Automatisierungsskripts speichern.  Zudem protokolliert Key Vault Zugriffe und Aktivitäten, ermöglicht die Überwachung der Zugriffssteuerung (IAM) in Ihrem Abonnement und bietet Diagnose-, Metrik-, Warnungs- und Problembehandlungstools, damit Sie über den Zugriff verfügen, den Sie benötigen.

![Azure Key Vault](../media-draft/Key-Vault.png)

<!-- TODO: get link to TC module --> Weitere Informationen zur Verwendung von Schlüsseltresoren finden Sie im Modul **Managing secrets with Azure Key Vault** (Verwalten von Geheimnissen mit Azure Key Vault).

## <a name="summary"></a>Zusammenfassung

Mit Azure Key Vault und einer angemessenen Geheimnisverwaltung gehören der Diebstahl von Anmeldeinformationen sowie manuelle Schlüsselrotationen und Zertifikatverlängerungen der Vergangenheit an.
