Angenommen, Ihr Unternehmen hat sich entschieden, Azure Disk Encryption (ADE) auf allen VMs zu implementieren. In diesem Fall müssen Sie evaluieren, wie Sie den Rollout für die Verschlüsselung auf allen vorhandenen VM-Volumes durchführen.

Hier werden die Anforderungen für ADE und die Schritte zum Verschlüsseln von Datenträgern auf vorhandenen Windows-VMs beschrieben.

## <a name="azure-disk-encryption-prerequisites"></a>Azure Disk Encryption – Voraussetzungen

Bevor Sie Ihren ersten VM-Datenträger verschlüsseln können, müssen Sie Folgendes durchführen:

1. Erstellen eines Schlüsseltresors
1. Einrichten einer Azure AD-Anwendung und eines Dienstprinzipals
1. Festlegen der Zugriffsrichtlinie für den Schlüsseltresor für die Azure AD-App
1. Festlegen der erweiterten Zugriffsrichtlinien für den Schlüsseltresor

### <a name="azure-key-vault"></a>Azure Key Vault

Die von ADE verwendeten Verschlüsselungsschlüssel können auf einer Azure Key Vault-Instanz gespeichert werden. Azure Key Vault ist ein Tool zum sicheren Speichern und Zugreifen auf Geheimnisse. Als Geheimnis wird alles bezeichnet, für das Sie den Zugriff streng kontrollieren möchten, z.B. API-Schlüssel, Kennwörter oder Zertifikate. Hiermit wird die hoch verfügbare und skalierbare sichere Speicherung in Hardwaresicherheitsmodulen (HSMs) mit Überprüfung gemäß Federal Information Processing Standards (FIPS) 140-2 Level 2 ermöglicht. Mit Key Vault erhalten Sie die vollständige Kontrolle über die Schlüssel, die zum Verschlüsseln Ihrer Daten verwendet werden, und Sie können Ihre Schlüsselnutzung verwalten und überwachen. Sie können Ihren Schlüsseltresor über das Azure-Portal, Azure PowerShell und Azure CLI konfigurieren und verwalten.

>[!NOTE]
> Für Azure Disk Encryption ist es erforderlich, dass sich Ihre Key Vault-Instanz und Ihre VMs in derselben Azure-Region befinden. So wird sichergestellt, dass Verschlüsselungsgeheimnisse nicht über Grenzen von Regionen hinweg verwendet werden.

### <a name="azure-ad-application-and-service-principal"></a>Azure AD-Anwendung und -Dienstprinzipal

Zum Zugreifen auf oder Ändern von Ressourcen, z.B. die Verschlüsselungskonfiguration für eine VM mit Skripts oder Code, müssen Sie zuerst eine **Azure Active Directory-Anwendung** einrichten. Azure Active Directory (Azure AD) ist ein mehrinstanzenfähiger, cloudbasierter Verzeichnis- und Identitätsverwaltungsdienst, in dem Kernverzeichnisdienste, Anwendungszugriffsverwaltung und Identitätsschutz in nur einer Lösung vereint sind.

Außerdem benötigen Sie einen Azure-**Dienstprinzipal**. Dienstprinzipale sind die Dienstkonten, die Sie zum Ausführen des Skripts oder Codes verwenden. Sie ermöglichen Ihnen das Zuweisen der spezifischen Berechtigungen und des Bereichs, die zum Ausführen der Aufgabe für eine bestimmte Azure-Ressource erforderlich sind.

In Azure AD sind zwei Elemente vorhanden: Das Anwendungsobjekt steht für die **_Definition_** der Anwendung (Zweck der Anwendung), und der Dienstprinzipal steht für die **_spezifische Instanz_** der Anwendung.

Dieser Ansatz beruht auf dem Prinzip der **geringsten Rechte**. Hierbei werden die Berechtigungen, die der App zugewiesen werden, auf das Minimum beschränkt, das die App zum Durchführen ihrer jeweiligen Aufgaben benötigt.

Sie können Azure AD-Anwendungen und -Dienstprinzipale mit dem Azure-Portal, Azure PowerShell und Azure CLI konfigurieren und verwalten.

### <a name="key-vault-access-policies"></a>Key Vault-Zugriffsrichtlinien

Bevor Sie Verschlüsselungsschlüssel in einer Key Vault-Instanz speichern können, benötigt ADE die Details zur **Client-ID** und zum **Clientgeheimnis** der Azure Active Directory-Anwendung, die über die Berechtigung zum Schreiben in die Key Vault-Instanz verfügt.

Außerdem müssen Sie den Azure-Zugriff auf die Verschlüsselungsschlüssel in Ihrem Schlüsseltresor angeben, damit sie für die VM zum Starten und Entschlüsseln der Volumes bereitgestellt werden.

## <a name="set-key-vault-advanced-access-policies"></a>Festlegen der erweiterten Zugriffsrichtlinien für den Schlüsseltresor

Mit **erweiterten Zugriffsrichtlinien** wird die Datenträgerverschlüsselung im Schlüsseltresor ermöglicht. Für die Verschlüsselungsbereitstellungen tritt ein Fehler auf, wenn sie nicht vorhanden sind. 

Es gibt drei Richtlinien, die aktiviert werden müssen:

- **Key Vault für die Datenträgerverschlüsselung** Ist für die Azure Disk-Verschlüsselung erforderlich.
- **Key Vault für die Bereitstellung** Ermöglicht dem Microsoft.Compute-Ressourcenanbieter das Abrufen von Geheimnissen aus dem Schlüsseltresor. Diese Richtlinie wird beim Erstellen einer VM benötigt.
- **Key Vault für die Vorlagenbereitstellung (falls erforderlich)** Ermöglicht Azure Resource Manager das Abrufen von Geheimnissen aus dem Schlüsseltresor. Diese Richtlinie ist erforderlich, wenn ARM-Vorlagen für die VM-Bereitstellung verwendet werden.

Zugriffsrichtlinien für den Schlüsseltresor können mit dem Azure-Portal, Azure PowerShell oder der Azure CLI konfiguriert und verwaltet werden.

### <a name="what-is-the-azure-disk-encryption-prerequisites-configuration-script"></a>Was ist das Konfigurationsskript für die Azure Disk Encryption-Voraussetzungen?

Mit dem **Konfigurationsskript für die Azure Disk Encryption-Voraussetzungen** werden alle Verschlüsselungsvoraussetzungen (bzw. so viele wie gewünscht) eingerichtet. Mit dem Skript wird auch sichergestellt, dass sich Ihre Key Vault-Instanz in derselben Region wie die zu verschlüsselnde VM befindet. Es erstellt eine Ressourcengruppe und einen Schlüsseltresor und legt die Zugriffsrichtlinie für den Schlüsseltresor fest. Das Skript erstellt darüber hinaus eine Ressourcensperre für den Schlüsseltresor, um zu verhindern, dass er versehentlich gelöscht wird.

## <a name="encrypting-an-existing-vm-disk"></a>Verschlüsseln eines vorhandenen VM-Datenträgers

Die Verschlüsselung eines vorhandenen VM-Datenträgers umfasst zwei Schritte, wenn das **Konfigurationsskript für die Azure Disk Encryption-Voraussetzungen** verwendet wird:

1. Führen Sie das Konfigurationsskript für die Azure Disk Encryption-Voraussetzungen aus.
1. Verschlüsseln des virtuellen Azure-Computers in PowerShell
