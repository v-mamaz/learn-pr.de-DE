Stellen Sie sich vor, Sie müssen ein Tool zur Verwaltung der Azure-Ressourcen auswählen, die Sie zum Testen Ihres CRM-Systems (Customer Relationship Management) verwenden. Die wichtigsten Vorgänge, die Sie ausführen müssen, sind das Erstellen von Ressourcengruppen und das Bereitstellen von virtuellen Computern.

Sie benötigen ein Tool, das einerseits von Administratoren leicht erlernt werden kann, aber gleichzeitig leistungsstark genug ist, um die Installation und Einrichtung mehrerer virtueller Computer zu automatisieren oder eine komplette Anwendungsumgebung per Skript zu erstellen. Es gibt viele Tools auf dem Markt. Sie müssen das finden, das sich am besten für Ihre Mitarbeiter und Ihre Aufgaben eignet.

## <a name="what-tools-are-available"></a>Welche Tools sind verfügbar?
Azure bietet drei Verwaltungstools zur Auswahl: 

1. Das Azure-Portal 
2. Die Azure-CLI
3. Azure PowerShell

All diese Tools bieten in etwa das gleiche Maß an Steuerung: Jede Aufgabe, die Sie mit einem Tool ausführen können, können Sie wahrscheinlich auch mit den anderen beiden erledigen. Alle drei sind plattformübergreifend und können unter Windows, macOS und Linux ausgeführt werden. Sie unterscheiden sich in der Syntax und den Setupanforderungen sowie darin, ob sie die Automatisierung unterstützen.

Im Folgenden werden alle drei Optionen beschrieben, und Sie erhalten hilfreiche Informationen, damit Sie sich zwischen den Optionen entscheiden können. 

## <a name="what-is-the-azure-portal"></a>Was ist das Azure-Portal?
Das Azure-Portal ist eine Website, auf der Sie die Ressourcen in Ihrem Azure-Abonnement erstellen, konfigurieren und ändern können. Das Portal ist eine grafische Benutzeroberfläche, auf der Sie die benötigten Ressourcen ganz einfach finden und erforderliche Änderungen vornehmen können. Das Portal hilft Ihnen mit Assistenten und QuickInfos auch bei komplexen Verwaltungsaufgaben.

Das Portal bietet keine Möglichkeit, sich wiederholende Aufgaben zu automatisieren. Wenn Sie beispielsweise 15 virtuelle Computer einrichten möchten, müssen Sie jeden einzelnen mithilfe des Assistenten erstellen. Dies kann bei komplexen Aufgaben zeitaufwendig und fehleranfällig sein. 

## <a name="what-is-the-azure-cli"></a>Was ist die Azure CLI?
Die Azure CLI ist ein plattformübergreifendes Befehlszeilenprogramm, über das Sie eine Verbindung mit Azure herstellen und Verwaltungsbefehle für Azure-Ressourcen ausführen können. Zum Erstellen eines virtuellen Computers würden Sie beispielsweise einen Befehl wie den folgenden verwenden:

```bash
az vm create \
  --resource-group CrmTestingResourceGroup \
  --name CrmUnitTests \
  --image UbuntuLTS
  ...
```

Die Azure CLI ist auf zwei Arten verfügbar: über Azure Cloud Shell in einem Browser oder in einer lokalen Installation unter Linux, macOS oder Windows. In beiden Fällen kann sie interaktiv oder mit Skripts verwendet werden. Bei der interaktiven Nutzung starten Sie zunächst eine Shell wie z.B. „`cmd.exe`“ unter Windows oder Bash unter Linux oder macOS und geben dann den Befehl an der Eingabeaufforderung der Shell ein. Um sich wiederholende Aufgaben zu automatisieren, stellen Sie die Befehle unter Verwendung der Syntax Ihrer ausgewählten Shell in einem Shellskript zusammen und führen dieses Skript dann aus.

## <a name="what-is-azure-powershell"></a>Was ist Azure PowerShell?
Azure PowerShell ist ein Modul, das Sie zu Windows PowerShell oder PowerShell Core hinzufügen, um eine Verbindung mit Ihrem Azure-Abonnement herzustellen und Ihre Ressourcen zu verwalten. Azure PowerShell erfordert PowerShell. PowerShell bietet Dienste wie Shellfenster, Befehlsanalyse usw. Azure PowerShell fügt die Azure-spezifischen Befehle hinzu.

Azure PowerShell stellt z.B. den Befehl **New-AzureRmVM** bereit, der einen virtuellen Computer in Ihrem Azure-Abonnement erstellt. Um diesen Befehl zu verwenden, starten Sie die PowerShell-Anwendung und geben einen Befehl wie den folgenden ein:

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell ist ebenfalls auf zwei Arten verfügbar: über Azure Cloud Shell in einem Browser oder in einer lokalen Installation unter Linux, macOS oder Windows. In beiden Fällen können Sie aus zwei Modi auswählen. Sie können Azure PowerShell im interaktiven Modus verwenden, in dem Sie manuell einen Befehl nach dem anderen eingeben, oder im Skriptmodus, in dem Sie ein aus mehreren Befehlen bestehendes Skript ausführen.

## <a name="how-to-choose-an-administrative-tool"></a>So wählen Sie das geeignete Verwaltungstool aus
In Bezug auf die Azure-Objekte, die verwaltet, und die Konfigurationen, die erstellt werden können, sind das Portal, die Azure CLI und Azure PowerShell in etwa gleich. Alle drei Tools funktionieren auch plattformübergreifend. Das bedeutet, dass Sie andere Faktoren berücksichtigen müssen, wenn Sie das zu verwendende Tool auswählen:

- **Automatisierung**: Müssen Sie eine Reihe von komplexen oder sich wiederholenden Aufgaben automatisieren? Azure PowerShell und die Azure CLI unterstützen diese Anforderung, das Portal nicht.

- **Lernkurve**: Müssen Sie schnell eine Aufgabe ausführen und haben keine Zeit, neue Befehle oder eine neue Syntax zu lernen? Für das Azure-Portal müssen Sie keine Syntax lernen oder sich Befehle merken. In Azure PowerShell und der Azure CLI müssen Sie die genaue Syntax jedes von Ihnen verwendeten Befehls kennen.

- **Kenntnisse im Team**: Besitzen Mitglieder Ihres Teams bereits Erfahrung? Hat Ihr Team möglicherweise PowerShell schon zum Verwalten von Windows verwendet? In diesem Fall wird Ihr Team sehr schnell mit Azure PowerShell zurechtkommen.

## <a name="example"></a>Beispiel
Denken Sie daran, dass Sie ein Verwaltungstool auswählen, mit dem Sie die Testumgebungen für Ihre CRM-Anwendung erstellen möchten. Ihre Administratoren müssen zwei spezifische Azure-Aufgaben ausführen:

1. Sie müssen eine Ressourcengruppe für jede Testkategorie (Einheit, Integration und Akzeptanz) erstellen.
2. Sie müssen vor jeder Testrunde mehrere virtuelle Computer in jeder Ressourcengruppe erstellen.

Zum Erstellen der Ressourcengruppen ist das Azure-Portal eine vernünftige Wahl. Das sind Aufgaben, die nur einmal ausgeführt werden müssen, daher sind dafür keine Skripts nötig.

Das Ermitteln des richtigen Tools zum Erstellen der virtuellen Computer ist da schon kniffliger. Sie müssen mehrere Computer erstellen und zwar immer wieder, wahrscheinlich mehrmals pro Woche. Diese Aufgabe sollten Sie also automatisieren, daher ist das Azure-Portal dafür keine gute Wahl. In diesem Fall erfüllen entweder Azure PowerShell oder die Azure CLI Ihre Anforderungen. Wenn Ihre Teammitglieder bereits über PowerShell-Kenntnisse verfügen, ist Azure PowerShell wahrscheinlich am besten geeignet. Azure PowerShell ist in dem Betriebssystem verfügbar, das von Ihrem Administratorteam verwendet wird, unterstützt die Automatisierung und ist für Ihr Team leicht zu lernen.

## <a name="summary"></a>Zusammenfassung
Die meisten Administratoren gehen die ersten Schritte mit Azure im Portal. Das Portal ist ein ausgezeichneter Einstiegspunkt, weil es eine klare, gut strukturierte grafische Oberfläche aufweist. Allerdings bietet es nur sehr eingeschränkte Optionen für die Automatisierung. Wenn Sie Automatisierungsfunktionen benötigen, bietet Azure Ihnen zwei Optionen: Azure PowerShell für Administratoren mit PowerShell-Erfahrung und die Azure CLI für alle anderen.

In der Praxis fallen bei den meisten Unternehmen sowohl einmalige als auch sich wiederholende Aufgaben an. Das bedeutet, dass sowohl das Portal als auch eine Skriptlösung zum Einsatz kommen. In unserem CRM-Beispiel ist es eine gute Lösung, die Ressourcengruppen über das Portal zu erstellen und die Erstellung der virtuellen Computer mit PowerShell zu automatisieren.

Der Rest dieses Moduls dreht sich um die Installation und Verwendung von Azure PowerShell.