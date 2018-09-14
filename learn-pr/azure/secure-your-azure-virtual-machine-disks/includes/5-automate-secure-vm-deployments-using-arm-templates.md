Angenommen, Ihr Unternehmen stellt im Rahmen ihrer Cloudmigration mehrere Server bereit. VM-Datenträger müssen bei der Bereitstellung verschlüsselt werden, damit sie zu keinem Zeitpunkt angreifbar sind. Sie möchten, diesen Prozess zu automatisieren, und ändern die Azure Resource Manager-Vorlagen, um die Verschlüsselung automatisch zu aktivieren.

Hier suchen wir an, wie eine Azure Resource Manager-Vorlage zu verwenden, um die Verschlüsselung für neue Windows-VMs automatisch zu aktivieren.

## <a name="what-are-azure-resource-manager-templates"></a>Was sind Azure Resource Manager-Vorlagen?

Diese Vorlagen sind JSON-Dateien verwendet, um eine Ressource in Azure bereitstellen, z.B. eine VM zu definieren. Sie können von Grund auf neu erstellt werden. Bei einigen Ressourcen (unter anderem bei virtuellen Computern) besteht allerdings auch die Möglichkeit, sie über das Azure-Portal zu generieren. Sie geben die erforderlichen Informationen für die manuelle Bereitstellung eines virtuellen Computers an, stellen den virtuellen Computer aber nicht in Azure bereit, sondern speichern die Vorlage.

Beispielvorlagen finden Sie auf GitHub.

## <a name="using-github-templates"></a>Verwenden von GitHub-Vorlagen

GitHub bietet eine Vorlage aus, für das Aktivieren der Verschlüsselung wird aufgerufen, die **Aktivieren der Verschlüsselung auf einer ausgeführten Windows-VM-ARM**. Sie befindet sich im Repository [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) (Azure-Schnellstartvorlagen). Die Seite mit der Infodatei für die Vorlage stellt eine **in Azure bereitstellen** Schaltfläche, klicken Sie dann die Vorlage im Azure-Portal geöffnet wird.

Die Vorlage ermöglicht die Bereitstellung eines virtuellen Windows Server-Computers mit bereits aktivierter Verschlüsselung. Bevor Sie mit der Vorlage, müssen Sie sicherstellen, dass alle Verschlüsselung Voraussetzungen erfüllt sind. Sie benötigen auch die Konfigurationsinformationen, die durch das Skript erforderliche Komponenten wie Azure Active Directory-Client-ID und Azure Active Directory-Clientschlüssel bereitgestellt wird.

Sie erstellen einen neuen virtuellen Computer, indem Sie die erforderlichen Informationen in die Vorlage eingeben. Anschließend initiieren Sie die Bereitstellung, indem Sie auf **Kaufen** klicken. (Dabei fallen in der Regel die normalen Azure-Computegebühren an.)

## <a name="deploy-an-encrypted-vm-by-using-a-template"></a>Bereitstellen eines verschlüsselten virtuellen Computers mit einer Vorlage

Die Bereitstellung eines verschlüsselten virtuellen Computers mit einer Vorlage umfasst folgende Hauptschritte:

1. Greifen Sie auf die Vorlage **Enable encryption on a running Windows VM ARM** (Aktivieren der Verschlüsselung für einen ausgeführten virtuellen Windows-Computer (ARM)) von GitHub zu, und führen Sie sie aus.

1. Fügen Sie auf der Skriptkonfigurationsseite die erforderlichen Informationen hinzu.

1. Stellen Sie mithilfe des Skripts einen neuen virtuellen Computer bereit, indem Sie auf **Kaufen** klicken.

1. Überprüfen Sie den Status der Datenträgerverschlüsselung über das Azure-Portal.
