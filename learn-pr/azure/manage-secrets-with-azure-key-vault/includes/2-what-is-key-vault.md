Azure Key Vault ist ein *Geheimnisspeicher*: ein zentraler Clouddienst zum Speichern von Anwendungsgeheimnissen. Key Vault hilft, die oben genannten Szenarios zu verhindern, indem Anwendungsgeheimnisse an einem zentralen Ort gespeichert werden und sicherer Zugriff, eine Berechtigungssteuerung und eine Zugriffsprotokollierung ermöglicht werden.

Folgende Hauptvorteile ergeben sich aus der Nutzung von Key Vault:

* geringeres Risiko für versehentliche Veröffentlichung von Geheimnissen durch sichere Speicherung außerhalb der Konfiguration und der Quellcodeverwaltung sowie durch Vermeiden von Szenarios, in denen Geheimnisse aus bzw. in Dateien kopiert werden oder in E-Mails oder Chats eingefügt werden
* eingeschränkter Zugriff auf Geheimnisse durch individuelle Zugriffsrichtlinien für Anwendungen und deren Benutzer
* zentrale Speicherung von Geheimnissen, wodurch mehrere Benutzer und Anwendungsinstanzen auf Geheimniswerte zugreifen können, die nur an einer Stelle aktualisiert werden müssen
* Zugriffsprotokollierung und -überwachung, mit der Sie nachvollziehen können, wie und wann auf Geheimnisse zugegriffen wurde

Geheimnisse werden in einzelnen *Tresoren* gespeichert. Hierbei handelt es sich um Azure-Ressourcen mit eigenen Konfigurations- und Sicherheitsrichtlinien, die Sie mit den Azure-Standardverwaltungstools wie dem Azure-Portal oder der Azure CLI erstellen können. Der Zugriff auf Geheimnisse und die Verwaltung des Tresors erfolgen über eine REST-API, die auch von allen Azure-Verwaltungstools und Clientbibliotheken für häufig verwendete Programmiersprachen unterstützt wird. Jeder Tresor verfügt über eine eindeutige URL, unter der seine API gehostet wird.

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
