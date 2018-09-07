Die Verwaltung der Infrastruktur einer beliebigen Workload umfasst Konfigurationsaufgaben. Die Konfiguration kann zwar manuell ausgeführt werden, aber manuell ausgeführte Vorgänge sind häufig aufwendig, fehleranfällig und nicht effizient. Und was geschieht, wenn Ihnen die Aufgabe zugeteilt wird, ein Projekt zu leiten, das die Bereitstellung von hunderten von Systemen in Azure umfasst? Wie sollen Sie diese Ressourcen dann erstellen und konfigurieren? Wie viel Zeit würde dies in Anspruch nehmen? Wäre es möglich sicherzustellen, dass alle Systeme fehlerfrei und ohne Abweichungen konfiguriert werden? Wenn Sie Ihre automatisierte Vorgänge in Ihre Architektur einbauen, können Sie all diese Herausforderungen meistern. Nachfolgend werden einige Möglichkeiten zur Automatisierung mit Azure vorgestellt.

## <a name="infrastructure-as-code"></a>Infrastruktur als Code

Sie können bei der Automatisierung der Bereitstellung von Diensten und Infrastruktur entweder auf imperative oder auf deklarative Weise vorgehen. Bei einem imperativen Ansatz werden genau die Befehle angegeben, die ausgeführt werden müssen, um das gewünschte Ergebnis zu erzielen. Bei einem deklarativen Ansatz wird das gewünschte Ergebnis angegeben, aber nicht vorgeben, wie dieses erzielt werden kann. Beide Ansätze eignen sich hervorragend. Sie können also nichts falsch machen. Im Folgenden wird erläutert, wie die einzelnen Ansätze in Azure funktionieren.

### <a name="imperative-automation"></a>Imperative Automatisierung

Zunächst wird die imperative Automatisierung erläutert. Bei der imperativen Automatisierung wird angegeben, _wie_ ein Ziel erreicht werden kann. Dies geschieht in der Regel programmgesteuert über eine Skriptsprache oder ein SDK. Für Azure-Ressourcen können z.B. eine Azure-Befehlszeilenschnittstelle oder Azure PowerShell verwendet werden. Im folgenden Beispiel wird eine Azure-Befehlszeilenschnittstelle verwendet, um ein Speicherkonto zu erstellen.

```azure-cli
az group create --name storage-resource-group --location westus
az storage account create --resource-group storage-resource-group --name mystorageaccount --kind BlobStorage --access-tier hot
```

Es wird gezeigt, wie Sie diese Ressourcen erstellen können. Erstellen Sie eine Ressourcengruppe über einen Befehl. Erstellen Sie über einen weiteren Befehl ein Speicherkonto. Azure erfährt explizit, welche Befehle ausgeführt werden müssen, um das gewünschte Ergebnis zu erzielen.

Dieser Ansatz hilft dabei, die Infrastruktur vollständig zu automatisieren. Es können Bereiche für Eingaben und Ausgaben bereitgestellt werden. Außerdem kann sichergestellt werden, dass jedes Mal die gleichen Befehle ausgeführt werden. Durch die Automatisierung der Ressourcen müssen keine manuellen Schritte mehr ausgeführt werden. Dadurch wird die Ressourcenverwaltung effizienter. Allerdings hat dieser Ansatz auch Nachteile. Skripts zum Erstellen von Ressourcen werden schnell immer komplexer, wenn auch die Architektur komplexer wird. Funktionen zur Fehlerbehandlung und Eingabeüberprüfung müssen möglicherweise hinzugefügt werden, damit alle Vorgänge vollständig ausgeführt werden können. Die Befehle können sich ändern, weshalb die Skripte stetig verwaltet werden müssen.

### <a name="declarative-automation"></a>Deklarative Automatisierung

Bei der deklarativen Automatisierung wird das gewünschte _Ergebnis_ angegeben und offengelassen, wie das verwendete System dieses erzielt. In Azure werden im Rahmen der deklarativen Automatisierung Azure Resource Manager-Vorlagen verwendet.

Bei Resource Manager-Vorlagen handelt es sich um mit JSON strukturierte Dateien, in denen angegeben wird, was erstellt werden soll. Im nachfolgenden Beispiel wird Azure aufgefordert, ein Speicherkonto mit von uns angegebenen Namen und Eigenschaften zu erstellen. Es wird Azure überlassen, geeignete Schritte auszuführen, um dieses Speicherkonto zu erstellen. Vorlagen bestehen aus vier Bereichen: Parametern, Variablen, Ressourcen und Ausgaben. Parameter verarbeiten Eingaben, die in der Vorlage verwendet werden sollen. Mithilfe von Variablen können Werte gespeichert werden, die in der Vorlage verwendet werden sollen. Bei den Ressourcen handelt es sich um das, was erstellt wird, und über Ausgaben erfahren Benutzer, was erstellt wurde.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "name": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "accountType": {
            "type": "string",
            "defaultValue": "Standard_RAGRS"
        },
        "kind": {
            "type": "string"
        },
        "accessTier": {
            "type": "string"
        },
        "httpsTrafficOnlyEnabled": {
            "type": "bool",
            "defaultValue": true
        }
    },
    "variables": {
    },
    "resources": [
        {
            "apiVersion": "2018-02-01",
            "name": "[parameters('name')]",
            "location": "[parameters('location')]",
            "type": "Microsoft.Storage/storageAccounts",
            "sku": {
                "name": "[parameters('accountType')]"
            },
            "kind": "[parameters('kind')]",
            "properties": {
                "supportsHttpsTrafficOnly": "[parameters('httpsTrafficOnlyEnabled')]",
                "accessTier": "[parameters('accessTier')]",
                "encryption": {
                    "services": {
                        "blob": {
                            "enabled": true
                        },
                        "file": {
                            "enabled": true
                        }
                    },
                    "keySource": "Microsoft.Storage"
                }
            },
            "dependsOn": []
        }
    ],
    "outputs": {
        "storageAccountName": {
            "type": "string",
            "value": "[parameters('name')]"
        }
    }
}
```

Sie können Vorlagen verwenden, um Dienste in Azure zu erstellen und zu bearbeiten. Sie können in Coderepositorys gespeichert, von der Quelle verwaltet und für mehrere Umgebungen freigegeben werden, um sicherzustellen, dass die Infrastruktur, die entwickelt wird, den Ansprüchen der Produktion entspricht. Sie stellen eine gute Möglichkeit zum Automatisieren von Bereitstellungen dar, wahren die Konsistenz, vermeiden falsche Konfigurationen von Bereitstellungen und erhöhen die Geschwindigkeit von Vorgängen.

Die Automatisierung Ihrer Infrastrukturbereitstellung stellt zwar einen hilfreichen ersten Schritt dar, aber die Bereitstellung von virtuellen Computern stellt immer noch eine aufwendige Herausforderung dar. Im Folgenden werden einige Ansätze zum Automatisieren der Konfiguration nach der Bereitstellung beschrieben.

## <a name="vm-customization-images-vs-post-deployment-configuration"></a>VM-Anpassung: Images im Gegensatz zur Konfiguration nach der Bereitstellung

Häufig reicht es nicht, wenn der Computer ausgeführt wird. Für die Bereitstellung von virtuellen Computern sind weitere Maßnahmen erforderlich. Es ist wahrscheinlich, dass zusätzliche Konfigurationen durchgeführt werden müssen, bevor die VM wie vorgesehen verwendet werden kann. Außerdem müssen möglicherweise die Datenträger formatiert, die VM mit einer Domäne verknüpft, ein Agent für eine Verwaltungssoftware installiert oder (und das ist am wahrscheinlichsten) die tatsächliche Workload ebenfalls installiert und konfiguriert werden.

Es werden in der Regel zwei Konfigurationsstrategien angewendet, die als Bestandteil der eigentlichen Konfiguration der VM selbst angesehen werden. Beide haben sowohl Vor- als auch Nachteile:

- Benutzerdefinierte Images
- Skripterstellung nach der Bereitstellung

Benutzerdefinierte Images werden erstellt, indem erst ein virtueller Computer bereitgestellt und dann eine Software auf der ausgeführten Instanz konfiguriert oder installiert wird. Wenn die Konfigurationen ohne Fehler durchgeführt wurde, kann der Computer heruntergefahren werden, und es wird über die VM ein Image erstellt. Das Image kann als Basis für andere neue virtuelle Computer verwendet werden. Wenn Sie mit benutzerdefinierten Images arbeiten, kann die Bereitstellung schneller abgeschlossen werden. Dies liegt daran, dass keine zusätzliche Konfiguration mehr nötig ist, sobald ein virtueller Computer einmal bereitgestellt wurde und ausgeführt wird. Wenn es Ihnen wichtig ist, dass Bereitstellungen schnell abgeschlossen werden, sollten Sie sich näher mit benutzerdefinierten Images auseinandersetzen.

Bei der Skripterstellung nach der Bereitstellung wird in der Regel zunächst ein Basisimage verwendet. Anschließend wird eine Skripterstellung- oder Konfigurationsverwaltungsplattform benötigt, die die Konfiguration ausführt, nachdem die VM bereitgestellt wurde. Führen Sie für die Skripterstellung nach der Bereitstellung mithilfe von Azure Script Extension ein Skript auf der VM aus, oder verwenden Sie eine stabilere Lösung wie Azure Automation Desired State Configuration (DSC).

Bei beiden Ansätze gibt es einiges zu beachten. Wenn Sie Images verwenden, müssen Sie sicherstellen, dass ein Prozess vorhanden ist, um Imageupdates, Sicherheitspatches und die Bestandsverwaltung der eigentlichen Images zu verarbeiten. Bei der Skripterstellung nach der Bereitstellung können Buildzeiten verlängert werden, da die VM erst zu Liveworkloads hinzugefügt werden kann, wenn der Buildvorgang abgeschlossen ist. Bei eigenständigen Systemen ist dieses Problem zwar von geringerer Bedeutung, aber wenn Dienste für die automatische Skalierung verwendet werden (z.B. bei VM-Skalierungsgruppen) hat diese verlängerte Buildzeit Auswirkungen auf die Dauer der Skalierung. Bei beiden Ansätzen sollten Sie darauf achten, Konfigurationsabweichungen anzugehen. Wenn eine neue Konfiguration veröffentlicht wird, sollten Sie sicherstellen, dass bereits vorhandene Systeme entsprechend angepasst werden.

Das Automatisieren der Bereitstellung von Ressourcen kann einen großen Vorteil für Ihre Umgebung darstellen. Sie sparen dadurch viel Zeit, und es treten weniger Fehler auf, sodass die Vorgänge effizienter ausgeführt werden können.

## <a name="automation-of-operational-tasks"></a>Automatisieren von Vorgängen

Auch wenn Ihre Lösungen einmal funktionieren und ausgeführt werden, gibt es trotzdem noch weitere Vorgänge, die automatisiert werden können. Wenn Sie diese mit Azure Automation ausführen, gibt es weniger manuelle Workloads und Konfigurationen und Updates für Computeressourcen können verwaltet werden. Freigegebene Ressourcen wie Zeitpläne, Anmeldeinformationen und Zertifikate werden zentralisiert, und es wird ein Framework zum Ausführen jeder beliebigen Azure-Aufgabe bereitgestellt.

Für Ihre Arbeit mit Lamna Healthcare umfasst dies möglicherweise Folgendes:

- Regelmäßiges Suchen nach Datenträgern für Datenträger, die nicht mehr verwendet werden
- Installieren der neusten Sicherheitspatches auf VMs
- Suchen nach und Herunterfahren von virtuellen Computern außerhalb der offiziellen Geschäftszeiten
- Tägliches Ausführen von Berichten und Erstellen eines Dashboards für die Geschäftsleitung

Nehmen Sie beispielsweise an, Sie möchten einen virtuellen Computer nur während der Geschäftszeiten ausführen. Sie können ein Skript schreiben, das den virtuellen Computer am Morgen startet und am Abend wieder herunterfährt. Sie können Azure Automation so konfigurieren, dass das Skript zu bestimmten Zeiten ausgeführt wird. Die folgende Abbildung zeigt die Rolle von Azure Automation in diesem Prozess.

![Abbildung, die die Rolle von Azure Automation bei der Verwaltung eines sich wiederholenden Geschäftsprozesses zeigt.](../media/automation-vm-power-state.png)

## <a name="automating-development-environments"></a>Automatisieren von Entwicklungsumgebungen

Ihrer Cloudinfrastruktur stehen die Computer gegenüber, die von Entwicklern verwendet werden, um Anwendungen und Dienste zu schreiben, die für das Unternehmen von Bedeutung sind. Sie können Azure DevTest Labs verwenden, um VMs mit den richtigen Tools und Repositorys auszustatten, die benötigt werden. Entwickler, die an mehreren Diensten arbeiten, können zwischen den einzelnen Entwicklungsumgebungen wechseln, ohne selbst einen neuen Computer bereitzustellen. Diese Entwicklungsumgebungen können heruntergefahren werden, wenn niemand sie verwendet, und anschließend wieder hochgefahren werden, wenn sie benötigt werden.

## <a name="automation-at-lamna-healthcare"></a>Automatisierung bei Lamna Healthcare

Im Folgenden wird erläutert, welche Verbesserungen Lamna Healthcare mithilfe von Automatisierung verzeichnet hat. Vor der Automatisierung wurden die Infrastrukturbereitstellung und Buildvorgänge für Server vollständig manuell durchgeführt. Entwicklungen wurden ausschließlich über das Portal bereitgestellt. Dadurch entstanden Abweichungen und Fehler im Zusammenhang mit Test- und Produktionsumgebungen. Außerdem war es aufgrund der Unterschiede schwierig, Probleme zu ermitteln, bevor der Code in Produktion ging.

Jetzt wird die gesamte Infrastruktur über Resource Manager-Vorlagen bereitgestellt. Diese Vorlagen werden in ein GitHub-Repository eingecheckt, und der Code wird überprüft, bevor diese bereitgestellt werden. Außerdem kann für die Entwicklung, das Testen und die Produktion eine gemeinsame Infrastruktur erstellt werden, um so sicherzustellen, dass die Konfigurationen für sämtliche Umgebungen überprüft wurden.

Für die meisten Dienste, die virtuelle Computer verwenden, werden Standardbasisimages und DSC verwendet, um die Systeme nach der Bereitstellung zu konfigurieren. Für Webfarmen, für die die Skalierbarkeit von VM-Skalierungsgruppen von Bedeutung ist, wird ein vollständig automatisierter Prozess angewandt, um Code einzuchecken und ein neues Image mit allen erforderlichen Konfigurationen zu erstellen, bevor es in den Skalierungsgruppen zur Verfügung gestellt wird.

Bestimmte VMs werden automatisch außerhalb der offiziellen Geschäftszeiten heruntergefahren, um deren Kosten zu reduzieren. Zudem wurde das VM-Patching automatisiert.

Außerdem verfügen Entwickler jetzt über eine Umgebung in DevTest Labs, die sich selbst verwaltet. In dieser können sie die Entwicklung an die neuesten Images und Konfigurationen anpassen und somit sicherstellen, dass dies den Konfigurationen in der Produktion entspricht.

All diese Änderungen haben zwar viel Mühe gekostet, aber sie zahlen sich langfristig aus. Die Anzahl von Fehlern wurde deutlich reduziert und die Entwicklerteams müssen weniger Zeit in die Verwaltung ihrer Umgebungen investieren. Die Entwickler sind begeistert, dass sie ganz einfach Ressourcen für die Entwicklung bereitstellen können und das Erstellen von Umgebungen so stark vereinfacht wurde.

## <a name="summary"></a>Zusammenfassung

Es wurden einige Möglichkeiten beschrieben, wie Automatisierungsfunktionen zu Ihrer Architektur hinzugefügt werden können. Angefangen bei der Bereitstellung von Infrastruktur als Code, bis hin zur Verbesserung der Produktivität von Entwicklern mithilfe von Laborumgebungen, stellt das Automatisieren von Umgebungen viele Vorteile dar. Wenn Sie Fehler und Abweichungen sowie Betriebskosten reduzieren, kann Ihre Organisation davon profitieren und Ihre Cloudumgebung kann deutlich verbessert werden.