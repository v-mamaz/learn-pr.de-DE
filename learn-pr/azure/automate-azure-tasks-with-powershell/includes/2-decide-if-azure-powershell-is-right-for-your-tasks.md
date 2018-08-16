## <a name="motivation"></a>Motivation
Angenommen Sie, Sie müssen ein Tool zum Verwalten der Azure-Ressourcen verwendet, um Ihr System (Customer Relationship Management, CRM) testen auswählen. Sind die wichtigsten Vorgänge, die Sie tun müssen: Erstellen von Ressourcengruppen und Bereitstellen von virtuellen Computern (VMs).

Sie möchten etwas, das einfach für Administratoren, aber leistungsfähige Informationen aus, um die Installation und Einrichtung von mehreren virtuellen Computern automatisieren. Mitglieder Ihres Teams verfügt über Erfahrung mit PowerShell von der vorherigen Windows-Verwaltung-Arbeit. Es sind mehrere Tools zur Verfügung. Sie müssen die beste Option für Ihre Mitarbeiter und Ihre Aufgaben zu finden.

## <a name="what-tools-are-available"></a>Welche Tools sind verfügbar?
Azure bietet drei Verwaltungstools zur Auswahl: das Azure-Portal, Azure PowerShell und der Azure-Befehlszeilenschnittstelle. 

Alle angebotenen ungefähr die gleiche Menge an Steuerelement; Jede Aufgabe, die Sie mit einem der Tools ausführen können, können Sie mit den anderen wahrscheinlich tun. Sie sind alle unter Linux, Mac und Windows verfügbar. Sie unterscheiden sich in der Syntax-setupanforderungen und gibt an, ob sie Automation unterstützen.

Hier wird beschrieben der drei Optionen und weisen Sie hilfreiche Informationen wie Sie zwischen ihnen zu entscheiden. 

## <a name="what-is-the-azure-portal"></a>Was ist Azure-Portal?
Das Azure-Portal ist eine Website, mit dem Sie das Erstellen, konfigurieren und ändern die Ressourcen in Ihrem Azure-Abonnement. Das Portal ist eine Grafische Benutzeroberfläche (GUI), das ist hilfreich, die die Ressource zu suchen, die Sie benötigen, und führen Sie die erforderlichen Änderungen vor. Es beschrieben, wie Sie komplexe Verwaltungsaufgaben durch die Bereitstellung von Assistenten und QuickInfos.

Das Portal bietet keine Möglichkeit, sich wiederholende Aufgaben zu automatisieren. Beispielsweise würde um 15 virtuelle Computer einzurichten, müssen sie einzeln nacheinander durch Abschließen des Assistenten für jeden virtuellen Computer erstellen. Dies kann zeitaufwändig und fehleranfällig für komplexe Aufgaben sein. 

## <a name="what-is-azure-powershell"></a>Was ist Azure PowerShell?
Azure PowerShell ist ein Modul, das Sie von PowerShell können Sie eine Verbindung mit Ihrem Azure-Abonnement herstellen und Verwalten von Ressourcen hinzufügen. Azure PowerShell müssen Sie PowerShell-Funktion. PowerShell bietet Dienste wie die Shell-Fenster, Befehl zu analysieren, usw. an. Die Azure-spezifischen Befehle wird von Azure PowerShell hinzugefügt.

Beispielsweise bietet der Azure PowerShell die **New-AzureRmVM** -Befehl, der einen virtuellen Computer in Ihrem Azure-Abonnement für Sie erstellt. Um es zu verwenden, Sie starten Sie die PowerShell-Anwendung und geben Sie dann einen Befehl wie folgt:
```
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell ist, zwei verschiedene Arten verfügbar: in einem Browser über Azure Cloud Shell oder mit einer lokalen Installation unter Linux, Mac oder Windows. In beiden Fällen haben Sie zwei Modi zur Auswahl. Sie können es verwenden, im interaktiven Modus, in dem Sie ihn manuell einen Befehl zu einem Zeitpunkt oder in den Skriptmodus, in dem Sie ein Skript ausführen, die aus mehreren Befehlen besteht.

## <a name="what-is-the-azure-cli"></a>Was ist der Azure-Befehlszeilenschnittstelle?
Der Azure-Befehlszeilenschnittstelle ist ein Befehlszeilenprogramm zum Verbinden mit Azure und das Ausführen administrativer Befehle für Azure-Ressourcen. Um einen virtuellen Computer zu erstellen, würden Sie beispielsweise einen Befehl wie den folgenden verwenden:

```
az vm create \
  --resource-group CrmTestingResourceGroup \
  --name CrmUnitTests \
  --image UbuntuLTS
  ...
```

Die Azure CLI ist zwei verschiedene Arten verfügbar: in einem Browser über Azure Cloud Shell oder mit einer lokalen Installation unter Linux, Mac oder Windows. In beiden Fällen können sie interaktiv verwendet oder ein Skript erstellt werden. Für die interaktive Verwendung, wenn Sie eine Shell, wie z. B. cmd.exe unter Windows oder Bash unter Linux oder MacOS zum ersten Mal aufrufen und geben Sie den Befehl an der shelleingabeaufforderung. Um sich wiederholende Aufgaben zu automatisieren, müssen Sie die CLI-Befehle in ein Shell-Skript, das mithilfe der Syntax von Ressourcenskriptdateien Ihrer ausgewählten Shell zusammenstellen und führen Sie das Skript.

## <a name="how-to-choose-an-administrative-tool"></a>Gewusst wie: Wählen Sie ein Verwaltungstool
Es ist ungefähre Parität zwischen dem Portal, Azure PowerShell und der Azure-Befehlszeilenschnittstelle in Bezug auf die Azure-Objekte, die sie verwalten können und die Konfigurationen, die sie erstellen können. Sie sind auch in Linux, Mac und Windows verfügbar. Dies bedeutet, dass bei Ihrer Wahl in der Regel einige andere Faktoren berücksichtigt werden:

- **Automation**: Sie müssen eine Reihe von komplexe und wiederkehrende Aufgaben zu automatisieren? Azure PowerShell und der Azure-Befehlszeilenschnittstelle unterstützen dies hingegen nicht im Portal.

- **Lernkurve**: müssen Sie eine Aufgabe schnell abgeschlossen werden, ohne neue Befehle oder die Syntax? Das Azure-Portal erfordert keine Syntax zu untersuchen oder Befehle zu merken. In Azure PowerShell und der Azure-Befehlszeilenschnittstelle müssen Sie die ausführliche Syntax für jeden Befehl kennen, die Sie verwenden.

- **Team-Fähigkeiten**: weist Ihr Team bisherige Erfahrung? Angenommen, kann Ihr Team PowerShell verwendet haben zum Verwalten von Windows. Wenn dies der Fall ist, werden sie schnell mithilfe von Azure PowerShell vertraut sind.

## <a name="example"></a>Beispiel
Denken Sie daran, dass Sie ein Verwaltungstool zum Erstellen von testumgebungen für Ihre CRM-Anwendung auswählen. Administratoren haben zwei bestimmte Azure-Aufgaben, die sie benötigen:
- Erstellen Sie eine Ressourcengruppe für jede Kategorie von Tests (Einheit, Integration und akzeptieren).
- Erstellen Sie mehrere virtuelle Computer in jeder Ressourcengruppe vor jeder testrunde.

Um die Ressourcengruppen zu erstellen, ist das Azure-Portal eine vernünftige Wahl. Dies sind einmalige Aufgaben erforderlich, Skripts, die sie ausgeführt werden.

Suchen das beste Tool zur Erstellung der virtuellen Computer ist eine anspruchsvollere Entscheidung. Müssen Sie mehrere zu erstellen, und Sie ihn wiederholt wahrscheinlich mehrmals pro Woche werden müssen. Dies bedeutet, dass die Automatisierung, sollten Sie daher im Azure-Portal keine gute Wahl. Azure PowerShell oder der Azure-Befehlszeilenschnittstelle wird Ihre Anforderungen zu erfüllen. Angesichts der Tatsache, dass Mitgliedern Ihres Teams über vorhandene PowerShell-Kenntnisse verfügen, werden Sie Azure PowerShell wahrscheinlich die beste Übereinstimmung. Azure PowerShell ist verfügbar, auf die Betriebssysteme über das Admin-Team verwendet, er unterstützt die Automatisierung, muss für Ihr Team sich schnell.

## <a name="summary"></a>Zusammenfassung
Die meisten Administratoren noch keine Erfahrung mit Azure ist im Portal. Es eignet sich hervorragend zum Starten, da es sich um eine grafische Benutzeroberfläche für saubere, gut strukturierte bietet aber eingeschränkte Optionen für Automatition bereitgestellt. Wenn Sie die Automatisierung benötigen, Azure bietet Ihnen zwei Optionen: Azure PowerShell für Administratoren mit Erfahrung mit PowerShell und der Azure-Befehlszeilenschnittstelle für alle anderen.

In der Praxis gibt es für Unternehmen in der Regel eine Kombination von den einmaligen und sich wiederholende Aufgaben. Dies bedeutet, dass es üblich, das Portal und eine skriptlösung zu verwenden ist. In unserem Beispiel CRM ist es die Erstellung von Ressourcengruppen über das Portal, und die VM-Erstellung mit PowerShell automatisieren.

Der Rest dieses Moduls konzentriert sich auf die Installation und Verwendung von Azure PowerShell.