Azure stellt zum Schutz von Azure-VM-Datenträgern Speicherdienstverschlüsselung (SSE) und Azure Disk Encryption (ADE) bereit. Diese Technologien arbeiten zusammen, um eine starke 256-Bit-Verschlüsselung im Rahmen eines mehrschichtigen Sicherheitsansatzes für den Schutz von Azure-VM-Datenträgern zu bieten. Es ist erforderlich, dass Sie die Einrichtung der notwendigen Komponenten für Azure Disk Encryption abschließen, um die Datenträgerverschlüsselung zu aktivieren. Dieser Vorgang kann mit dem Konfigurationsskript für die erforderlichen Azure Disk Encryption-Komponenten automatisiert werden. Wenn Sie die Verschlüsselung auf neuen VMs aktivieren, können Sie eine Azure Resource Manager-Vorlage verwenden. So wird sichergestellt, dass Ihre Daten zum Zeitpunkt der Bereitstellung verschlüsselt werden, sodass keine Sicherheitsrisiken entstehen.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Problembehandlung für die Verschlüsselung von Datenträgern von Azure-VMs](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-tsg)
- [Verschlüsseln eines virtuellen Linux-Computers in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/encrypt-disks)
- [Übersicht über Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-overview)
- [Welche Linux-Distributionen werden von Azure Disk Encryption unterstützt?](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-faq#bkmk_LinuxOSSupport)
- [Resource Manager-Vorlagen auf GitHub](https://github.com/Azure/azure-quickstart-templates)