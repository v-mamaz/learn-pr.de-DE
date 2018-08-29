Azure Key Vault ist ein *Geheimnisspeicher*: ein zentraler Clouddienst zum Speichern von Anwendungsgeheimnissen. Key Vault hilft, die oben genannten Szenarien zu verhindern, indem Anwendungsgeheimnisse mit sicherem Zugriff, Berechtigungensteuerung und Zugriffsprotokollierung an einem zentralen Ort gespeichert werden.

Ein einzelner Tresor ist eine Azure-Ressource mit eigener Konfigurations- und Sicherheitsrichtlinie, die Sie mit den standardmäßigen Azure-Management-Tools wie Azure-Portal oder der Azure-Befehlszeilenschnittstelle erstellen können. Geheimniszugriff und Tresorverwaltung erfolgen über eine REST-API. Jeder Tresor verfügt über eine eindeutige URL, unter der seine API gehostet wird.

> [!IMPORTANT]
> **Key Vault dient zum Speichern von Konfigurationsinformationen für Serveranwendungen.** Es dient nicht zum Speichern von Daten, die zu den Benutzern Ihrer App gehören, und sollte nicht im clientseitigen Teil einer App verwendet werden. Dies spiegelt sich in seinen Leistungsmerkmalen, seiner API und seinem Kostenmodell wieder.
>
> Benutzerdaten sollten an anderer Stelle gespeichert werden, z.B. in einer Azure SQL-Datenbank mit Transparent Data Encryption, oder auf einem Speicherkonto mit Speicherdienstverschlüsselung. Geheimnisse, die von Ihrer Anwendung verwendet werden, um auf diese Datenspeicher zuzugreifen, können in Key Vault gespeichert werden.

## <a name="what-is-a-secret-in-key-vault"></a>Was ist ein Geheimnis in Key Vault?

In Key Vault ist ein Geheimnis ein Name/Wert-Paar von Zeichenfolgen. Geheimnisnamen müssen 1-127 Zeichen lang sein, dürfen nur alphanumerische Zeichen und Bindestriche enthalten und müssen in einem Tresor eindeutig sein. Ein geheimer Wert kann jede bis zu 25 KB große UTF-8-Zeichenfolge sein.

> [!TIP]
> Geheimnisnamen müssen nicht an sich als Geheimnis behandelt werden. Sie können sie in der Konfiguration Ihrer App speichern, wenn Ihre Implementierung dies erfordert. Dasselbe gilt für Tresornamen und URLs.

> [!NOTE]
> Key Vault unterstützt zwei weitere Arten von Geheimnissen außer Zeichenfolgen &mdash; *Schlüssel* und *Zertifikate* &mdash; und bietet nützliche Funktionen speziell für ihre Anwendungsfälle. Dieses Modul behandelt diese Funktionen nicht und konzentriert sich auf die geheimen Zeichenfolgen wie Kennwörter und Verbindungszeichenfolgen.
