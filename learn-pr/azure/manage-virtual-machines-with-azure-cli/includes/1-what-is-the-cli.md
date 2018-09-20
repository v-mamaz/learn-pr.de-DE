Es kommt relativ häufig vor, dass IT-Abteilungen eine große Gruppe von Azure-Ressourcen verwalten – von Azure Virtual Machines bis zu verwalteten Websites.

Die Verwendung des Azure-Portals für einmalige Aufgaben ist einfach, aber das Navigieren durch die unterschiedlichen Blätter kostet zusätzliche Zeit, wenn Sie mehrere Dinge erstellen, ändern oder löschen müssen. Hier zeigt sich die Nützlichkeit der Befehlszeile: Sie können Befehle schnell und effizient ausführen und sogar Skripts verwenden, um sich häufig wiederholende Aufgaben durchzuführen. In Azure verfügen Sie über zwei unterschiedliche Befehlszeilentools, die Sie nutzen können: Azure PowerShell und die Azure CLI.

Mit beiden Tools können Sie Skripts schreiben, um den Status von Cloudservern zu prüfen, neue Konfigurationen bereitzustellen, Ports in der Firewall zu öffnen oder zum Ändern einer Einstellung eine Verbindung mit einem virtuellen Computer herzustellen. Windows-Administratoren neigen zur Verwendung von Azure PowerShell, während Entwickler und Linux-Administratoren häufig die Azure CLI nutzen.

In diesem Modul verwenden wir die Azure CLI, um in Azure gehostete virtuelle Computer zu erstellen und zu verwalten. Wenn Sie eine Übersicht über die Azure CLI, ihre Installation und die Arbeit mit Ihren Azure-Abonnements erhalten möchten, hilft Ihnen das Schulungsmodul **Steuern von Azure-Diensten mit der CLI** weiter.

## <a name="what-is-the-azure-cli"></a>Was ist die Azure CLI?

Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen. Sie steht für macOS, Linux und Windows sowie über [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) im Browser zur Verfügung.

Die Azure CLI kann Sie dabei unterstützen, Azure-Ressourcen, z.B. virtuelle Computer und Datenträger, über die Befehlszeile oder mithilfe von Skripts zu verwalten. Im Folgenden wird beschrieben, welche Möglichkeiten es hiermit in Bezug auf Azure Virtual Machines gibt.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Erstellen einer VM mit der Azure CLI
- Ändern der Größe von VMs mit der Azure CLI
- Ausführen grundlegender Verwaltungsaufgaben mit der Azure CLI
- Herstellen einer Verbindung mit einer aktiven VM über SSH und die Azure CLI

## <a name="prerequsites"></a>Voraussetzungen

- Grundkenntnisse zum Azure CLI-Tool aus dem Modul **Steuern von Azure-Diensten mit der CLI**.