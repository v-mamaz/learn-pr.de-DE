Jim verwaltet einen Satz von Azure Virtual Machines auf unsere firmeneigene Web-Infrastruktur, die mehrere Websites und Servern, die auf verschiedenen Plattformen mit umfasst ausgeführt wird. 

Während das Azure-Portal einfach zu verwenden ist, Jim gefunden, dass beim Navigieren durch die verschiedenen Blätter Zeit einige Aufgaben hinzugefügt. 

Beim Durchsuchen der alternativen, erkennt er das Tool für die Azure-Befehlszeilenschnittstelle (CLI).

Arbeiten mit der Azure CLI, kann Jim Skripts schreiben, um den Status von seinen Servern überprüfen, stellen Sie eine neue Konfiguration, einen Port öffnen oder Herstellen einer Verbindung eines virtuellen Computers auf eine Einstellung ändern, mit.

Sie können vielleicht Jim entsprechen und ein Tool zum Automatisieren von Aufgaben in Ihrer Cloudumgebung suchen. Wir werden die veranschaulicht, wie mit der Azure-Befehlszeilenschnittstelle erstellen und Verwalten von virtuellen Computern in Azure gehostet. 

## <a name="azure-cli"></a>Azure-Befehlszeilenschnittstelle

Der Azure-Befehlszeilenschnittstelle ist Microsofts plattformübergreifende Befehlszeilentool für die Verwaltung von Azure-Ressourcen. Es steht für MacOS, Linux und Windows, oder klicken Sie im Browser mit der [Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).

> [!IMPORTANT]
> Es stehen zwei Versionen des Azure-CLI-Tools noch heute: Azure CLI 1.0 und Azure CLI 2.0. Wir werden Azure CLI 2.0 verwenden, ist die neueste Version aus, und wird empfohlen, es sei denn, Sie legacy-Skripts, die für 1.0 ausführen. Azure CLI 1.0 gestartet wird, mithilfe der `azure` -Befehl, und die Azure CLI 2.0 wird gestartet, mit der `az` Befehl. 

Der Azure-Befehlszeilenschnittstelle können Sie die Azure-Ressourcen wie virtuellen Computern und Datenträgern über die Befehlszeile oder in Skripts verwalten. Wir beginnen, und sehen, was sie tun kann.