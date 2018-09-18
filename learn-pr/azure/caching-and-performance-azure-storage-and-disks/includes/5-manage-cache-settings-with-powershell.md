Das Erstellen von Verwaltungsskripts ist eine leistungsstarke Möglichkeit, Ihren Workflow zu optimieren. Sie können gängige, sich wiederholende Aufgaben automatisieren. Nachdem ein Skript überprüft wurde, wird es konsistent ausgeführt, was wahrscheinlich das Auftreten von Fehler reduziert. In der vorherigen Übung haben wir über das Azure-Portal eine VM erstellt, einen Datenträger für Daten hinzugefügt und Cacheeinstellungen geändert. Was wäre, wenn wir diese Aufgaben auf vielen VMs in vielen Regionen wiederholen müssten? Wir verwenden Azure PowerShell!

## <a name="what-is-azure-powershell"></a>Was ist Azure PowerShell?
Azure PowerShell ist ein Modul, das Sie zu PowerShell hinzufügen, um eine Verbindung mit Ihrem Azure-Abonnement herzustellen und Ihre Ressourcen zu verwalten. Die Funktion von Azure PowerShell erfordert PowerShell. PowerShell bietet Dienste wie Shellfenster, Befehlsanalyse usw. Azure PowerShell fügt die Azure-spezifischen Befehle hinzu.

Azure PowerShell stellt z.B. den Befehl **New-AzureRmVM** bereit, der einen virtuellen Computer in Ihrem Azure-Abonnement erstellt. Um diesen Befehl zu verwenden, starten Sie die PowerShell-Anwendung und geben einen Befehl wie im Beispiel ein:

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell ist auf zwei Arten verfügbar: über Azure Cloud Shell in einem Browser oder in einer lokalen Installation unter Linux, macOS oder Windows.

## <a name="what-are-powershell-cmdlets"></a>Was sind PowerShell-Cmdlets?

Ein PowerShell-Befehl wird als **Cmdlet** (ausgesprochen: „Command-let“) bezeichnet. Ein Cmdlet ist ein Befehl, der ein einzelnes Feature bearbeitet. Der Begriff **Cmdlet** soll „kleiner Befehl“ heißen. Gemäß der Konvention wird Cmdlet-Autoren empfohlen, Cmdlets einfach zu halten und nur für einen einzigen Zweck zu erstellen.

Im PowerShell-Basisprodukt sind Cmdlets enthalten, die mit Features wie Sitzungen und Hintergrundaufträgen funktionieren. Fügen Sie Module zu Ihrer PowerShell-Installation hinzu, damit Cmdlets andere Features ändern können. Es gibt z.B. Drittanbietermodule für die Arbeit mit FTP, das Verwalten Ihres Betriebssystems oder das Zugreifen auf das Dateisystem.

Die Namenskonvention bei Cmdlets ist „Verb-Substantiv“, z.B. **Get-Process**, **Format-Table** und **Start-Service**. Es gibt ebenfalls eine Konvention für die Auswahl des Verbs, z.B. „get“ zum Abrufen von Daten, „set“ zum Einfügen oder Aktualisieren von Daten, „format“ zum Formatieren von Daten oder „out“, um die Ausgabe einem Ziel zuzuweisen.

Cmdlet-Autoren wird empfohlen, eine Hilfedatei für jedes Cmdlet beizufügen. Das Cmdlet **Get-Help** zeigt die Hilfedatei für ein Cmdlet an:

```
Get-Help <cmdlet-name> -detailed
```
## <a name="what-is-azurerm"></a>Was ist AzureRM?

**AzureRM** ist der formelle Name des Azure PowerShell-Moduls, das einen Satz von Cmdlets enthält, die mit den Azure-Features zusammenarbeiten sollen (das **RM** im Namen steht für **Resource Manager**). Es enthält hunderte Cmdlets, mit denen Sie nahezu jeden Aspekt jeder Azure-Ressource regulieren können. Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory, Containern, Machine Learning usw. arbeiten.

## <a name="powershell-cmdlets-for-managing-azure-disk-caching"></a>PowerShell-Cmdlets zum Verwalten von Azure-Datenträgerzwischenspeichern

Azure PowerShell verfügt über bestimmte Cmdlets zum Verwalten von VMs und Datenträgern. 

Die folgende Tabelle enthält einige der Cmdlets, die wir in der nächsten Übung verwenden.

|Befehl  |Beschreibung  |
|---------|---------|
|`Get-AzureRmVM`     |  Dient zum Abrufen der Eigenschaften eines virtuellen Computers.       |        $myVM
|`Update-AzureRmVM`     |  Aktualisiert den Status des virtuellen Azure-Computers.       |        
|`New-AzureRmDiskConfig`     |  Erstellt ein konfigurierbares Datenträgerobjekt.       |        
|`Add-AzureRmVMDataDisk`     |  Fügt einen Datenträger einem virtuellen Computer hinzu.   |      


Wir verwenden diese Cmdlets in der nächsten Übung zum Verwalten des Zwischenspeicherns auf dem virtuellen Computer.
