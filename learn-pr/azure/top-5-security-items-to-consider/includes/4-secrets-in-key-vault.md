Geheime Schlüssel sind Geheimnisse nicht, wenn sie mit allen Benutzern gemeinsam genutzt werden. Speichern vertrauliche, z.B. Verbindungszeichenfolgen, ist Security Token, Zertifikate und Kennwörter in Ihrem Code einfach einladen von Benutzern zu aufnehmen und für einen anderen Wert als für die gewünschten. Speichern diese Art von Daten auch in Ihrer Webkonfiguration ist keine gute Idee – Sie sind im Wesentlichen jede Person mit Zugriff auf den Quellcode oder Web Serverzugriff auf Ihre privaten Daten erlauben.

Stattdessen sollten Sie immer diese Geheimnisse in abgelegt **Azure Key Vault**.

## <a name="what-is-azure-key-vault"></a>Was ist Azure Key Vault
Azure Key Vault ist ein *Geheimnisspeicher*: ein zentraler Clouddienst zum Speichern von Anwendungsgeheimnissen. Key Vault sorgt für die Sicherheit Ihrer vertraulichen Daten geheime Schlüssel für Anwendungen in einem zentralen Ort speichern und Bereitstellen von sicheren Zugriff, Berechtigungen Kontrolle und Protokollierung für den Zugriff.

Vertraulichen Informationen befinden sich in einzelnen *Tresore*, jeweils ihre eigenen Konfigurations- und Richtlinien zum Steuern des Zugriffs. Sie erhalten dann mit Ihren Daten über eine REST-API oder über eine Client-SDK für die meisten Sprachen verfügbar.

> [!IMPORTANT]
> **Key Vault dient zum Speichern von Konfigurationsinformationen für Serveranwendungen.** Es dient nicht zum Speichern von Daten, die zu den Benutzern Ihrer App gehören, und sollte nicht im clientseitigen Teil einer App verwendet werden. Dies spiegelt sich in seinen Leistungsmerkmalen, seiner API und seinem Kostenmodell wieder.
>
> Benutzerdaten sollten an anderer Stelle gespeichert werden, z.B. in einer Azure SQL-Datenbank mit Transparent Data Encryption, oder auf einem Speicherkonto mit Speicherdienstverschlüsselung. Geheimnisse, die von Ihrer Anwendung verwendet werden, um auf diese Datenspeicher zuzugreifen, können in Key Vault gespeichert werden.

## <a name="why-use-a-key-vault-for-my-secrets"></a>Gründe für die Verwendung eines Schlüsseltresors für meine geheime Schlüssel

Verwalten von Schlüsseln und Geheimnissen speichern können kompliziert und fehleranfällig, wenn eine manuelle sein. Rotieren von Zertifikaten manuell bedeutet, dass potenziell ohne für einige Stunden oder Tage. Wie bereits erwähnt, bedeutet speichern Ihre Verbindungszeichenfolgen in Ihrer Konfiguration Datei oder Code-Repository, dass jemand Ihre Anmeldeinformationen stehlen könnten.

Key Vault ermöglicht Benutzern das Speichern von Verbindungszeichenfolgen, geheime Schlüssel, Kennwörter, Zertifikate, Zugriffsrichtlinien, Dateisperren (Elemente in Azure als schreibgeschützt markieren) und Automation-Skripts.  Zudem protokolliert Zugriff und der Aktivität können Sie die Zugriffssteuerung (IAM) in Ihrem Abonnement zu überwachen, sowie über Diagnose-, Metriken, Warnungen und Tools zur Problembehandlung, um sicherzustellen, dass Sie über die Zugriffsrechte, die Sie benötigen.

![Azure Key Vault](../media-draft/Key-Vault.png)

<!-- TODO: get link to TC module -->
<!--
You can learn more about using a Key Vault in the module [Manage secrets in your server apps with Azure Key Vault](learn/modules/manage-secrets-with-azure-key-vault).-->

## <a name="summary"></a>Zusammenfassung

Anmeldeinformationen Sie Identitätsdiebstahl, manuelle Schlüsselrotation und, dass die Verlängerung der Vergangenheit sein kann, wenn Sie Ihre Geheimnisse, verwalten und Verwenden von Azure Key Vault-Zertifikat für.
