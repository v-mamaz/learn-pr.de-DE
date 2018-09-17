Angenommen, Ihr Unternehmen stellt im Rahmen ihrer Cloudmigration mehrere Server bereit. VM-Datenträger müssen bei der Bereitstellung verschlüsselt werden, damit sie zu keinem Zeitpunkt angreifbar sind. Sie möchten diesen Prozess automatisieren und müssen die Azure Resource Manager-Vorlagen ändern, damit die Verschlüsselung automatisch aktiviert wird.

Im Folgenden verwenden Sie eine Azure Resource Manager-Vorlage, um die Verschlüsselung für neue virtuelle Windows-Computer automatisch zu aktivieren.

## <a name="what-are-azure-resource-manager-templates"></a>Was sind Azure Resource Manager-Vorlagen?

Bei diesen Vorlagen handelt es sich um JSON-Dateien zum Definieren einer Ressource, die in Azure bereitgestellt werden soll (beispielsweise ein virtueller Computer). Sie können von Grund auf neu erstellt werden. Bei einigen Ressourcen (unter anderem bei virtuellen Computern) besteht allerdings auch die Möglichkeit, sie über das Azure-Portal zu generieren. Sie geben die erforderlichen Informationen für die manuelle Bereitstellung eines virtuellen Computers an, stellen den virtuellen Computer aber nicht in Azure bereit, sondern speichern die Vorlage.

Beispielvorlagen finden Sie auf GitHub.

## <a name="using-github-templates"></a>Verwenden von GitHub-Vorlagen

Auf GitHub steht die Vorlage **Enable encryption on a running Windows VM ARM** (Aktivieren der Verschlüsselung für einen ausgeführten virtuellen Windows-Computer mithilfe von ARM) zum Aktivieren der Verschlüsselung zur Verfügung. Sie befindet sich im Repository [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) (Azure-Schnellstartvorlagen). Auf der Infoseite der Vorlage befindet sich die Schaltfläche **Deploy to Azure** (In Azure bereitstellen), mit der Sie die Vorlage im Azure-Portal öffnen können.

Die Vorlage ermöglicht die Bereitstellung eines virtuellen Windows Server-Computers mit bereits aktivierter Verschlüsselung. Vergewissern Sie sich vor der Verwendung der Vorlage, dass alle Voraussetzungen für die Verschlüsselung erfüllt sind. Darüber hinaus benötigen Sie die Konfigurationsinformationen, die durch das Skript zur Überprüfung der Voraussetzungen bereitgestellt werden (etwa die Azure Active Directory-Client-ID und das Azure Active Directory-Clientgeheimnis).

Sie erstellen einen neuen virtuellen Computer, indem Sie die erforderlichen Informationen in die Vorlage eingeben. Anschließend initiieren Sie die Bereitstellung, indem Sie auf **Kaufen** klicken. (Dabei fallen in der Regel die normalen Azure-Computegebühren an.)

## <a name="deploy-an-encrypted-vm-by-using-a-template"></a>Bereitstellen eines verschlüsselten virtuellen Computers mit einer Vorlage

Die Bereitstellung eines verschlüsselten virtuellen Computers mit einer Vorlage umfasst folgende Hauptschritte:

1. Greifen Sie auf die Vorlage **Enable encryption on a running Windows VM ARM** (Aktivieren der Verschlüsselung für einen ausgeführten virtuellen Windows-Computer (ARM)) von GitHub zu, und führen Sie sie aus.

1. Fügen Sie auf der Skriptkonfigurationsseite die erforderlichen Informationen hinzu.

1. Stellen Sie mithilfe des Skripts einen neuen virtuellen Computer bereit, indem Sie auf **Kaufen** klicken.

1. Überprüfen Sie den Status der Datenträgerverschlüsselung über das Azure-Portal.
