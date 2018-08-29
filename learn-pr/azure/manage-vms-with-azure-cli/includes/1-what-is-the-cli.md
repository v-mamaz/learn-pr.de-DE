Jim verwaltet eine Reihe von virtuellen Azure-Computern, die in der Webinfrastruktur unseres Unternehmens ausgeführt werden, die zahlreiche Websites und Datenbankserver mit verschiedenen Plattformen umfasst. 

Das Azure-Portal lässt sich zwar sehr einfach bedienen, aber Jim hat festgestellt, dass die Navigation durch die zahlreichen Blätter bei einigen Aufgaben recht zeitaufwendig ist. 

Er sucht also nach Alternativen und stößt dabei auf die Azure CLI (Command Line Interface, Befehlszeilenschnittstelle).

Mit der Azure CLI kann Jim Skripts zum Überprüfen des Status seiner Server schreiben, eine neue Konfiguration bereitstellen, einen Port öffnen oder eine Verbindung mit einem virtuellen Computer herstellen, um eine Einstellung zu ändern.

Vielleicht geht es Ihnen wie Jim, und Sie suchen nach einem Tool, das Ihnen dabei hilft, Aufgaben in Ihrer Cloudumgebung zu automatisieren. Wir zeigen Ihnen jetzt, wie Sie die Azure CLI verwenden, um in Azure gehostete virtuelle Computer zu erstellen und zu verwalten. 

## <a name="azure-cli"></a>Azure-Befehlszeilenschnittstelle

Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen. Sie steht für macOS, Linux und Windows sowie unter Verwendung von [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) im Browser zur Verfügung.

> [!IMPORTANT]
> Es gibt heute zwei Versionen der Azure CLI: Azure CLI 1.0 und Azure CLI 2.0. Wir verwenden hier die neueste Version, Azure CLI 2.0, die empfohlen wird, außer wenn Sie ältere Skripts ausführen, die für 1.0 geschrieben wurden. Azure CLI 1.0 wird mit dem Befehl „`azure`“ gestartet, Azure CLI 2.0 mit dem Befehl „`az`“. 

Die Azure CLI kann Sie dabei unterstützen, Azure-Ressourcen wie z.B. virtuelle Computer und Datenträger über die Befehlszeile oder mithilfe von Skripts zu verwalten. Fangen wir einfach an und finden heraus, was Sie mit dem Tool tun können.

## <a name="learning-objectives"></a>Lernziele
> [!div class="checklist"]
> * Erstellen eines virtuellen Azure-Computers mit der CLI
> * Ändern der Größe von virtuellen Computern mit der CLI
> * Verwalten und Abfragen eines virtuellen Computers über die Befehlszeile
> * Installieren von Software auf einem virtuellen Computer