Das Erstellen von Verwaltungsskripts ist eine leistungsstarke Möglichkeit, Ihren Workflow zu optimieren. Sie können die gängiger, sich wiederholender Aufgaben automatisieren. Nachdem ein Skript überprüft wurde, wird sie konsistent und ausgeführt, wahrscheinlich wird der Fehler reduzieren. In der vorherigen Übung haben wir eine virtuelle Maschine erstellt, einen Datenträger für Daten hinzugefügt und cacheeinstellungen, über das Azure-Portal geändert. Was geschieht, wenn es erforderlich, wiederholen diese Aufgaben auf vielen VMs in vielen Regionen? Azure PowerShell verwenden, lassen Sie uns!

## <a name="what-is-azure-powershell"></a>Was ist Azure PowerShell?

Azure PowerShell ist ein Modul, das Sie Windows PowerShell können Sie eine Verbindung mit Ihrem Azure-Abonnement herstellen und Verwalten von Ressourcen hinzufügen. Azure PowerShell müssen Sie Windows PowerShell-Funktion. Windows PowerShell bietet Dienste wie die Shell-Fenster, Befehl zu analysieren und So weiter. Azure PowerShell fügt die Azure-spezifischen Befehle hinzu.

Beispielsweise bietet der Azure PowerShell die **New-AzureRmVM** -Befehl, der einen virtuellen Computer in Ihrem Azure-Abonnement für Sie erstellt. Um es zu verwenden, Sie starten Sie die PowerShell-Anwendung und geben Sie dann einen Befehl wie im folgenden Beispiel:

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell ist, zwei verschiedene Arten verfügbar: in einem Browser über Azure Cloud Shell oder mit einer lokalen Installation unter Linux, Mac oder Windows.

## <a name="what-are-powershell-cmdlets"></a>Was sind PowerShell-Cmdlets?

Ein PowerShell-Befehl wird als **Cmdlet** (ausgesprochen: „Command-let“) bezeichnet. Ein Cmdlet ist ein Befehl, der ein einzelnes Feature bearbeitet. Der Begriff **Cmdlet** richtet sich an "kleine Command". Gemäß der Konvention wird Cmdlet-Autoren empfohlen, Cmdlets einfach zu halten und nur für einen einzigen Zweck zu erstellen.

Im PowerShell-Basisprodukt sind Cmdlets enthalten, die mit Features wie Sitzungen und Hintergrundaufträgen funktionieren. Fügen Sie Module zu Ihrer PowerShell-Installation hinzu, damit Cmdlets andere Features ändern können. Es gibt z.B. Drittanbietermodule für die Arbeit mit FTP, das Verwalten Ihres Betriebssystems oder das Zugreifen auf das Dateisystem.

Die Namenskonvention bei Cmdlets ist „Verb-Substantiv“, z.B. **Get-Process**, **Format-Table**, and **Start-Service**. Es gibt auch eine Konvention für das Verb Wahl: "get" zum Abrufen von Daten, die "set" zum Einfügen oder Aktualisieren von Daten, die "format" zum Formatieren von Daten, "out" für die direkte Ausgabe an ein Ziel aus, und So weiter.

Cmdlet-Autoren wird empfohlen, eine Hilfedatei für jedes Cmdlet beizufügen. Das Cmdlet **Get-Help** zeigt die Hilfedatei für ein Cmdlet an:

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>Was ist AzureRM?

**AzureRM** ist der formelle Name für das Azure PowerShell-Modul, die einen Satz von Cmdlets arbeiten mit Azure-Features (die **RM** im Namen steht für **Resource Manager**). Es enthält hunderte Cmdlets, mit denen Sie nahezu jeden Aspekt jeder Azure-Ressource regulieren können. Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory, Containern, Machine Learning usw. arbeiten.

## <a name="powershell-cmdlets-for-managing-azure-disk-caching"></a>PowerShell-Cmdlets zum Verwalten von Azure-Datenträger Zwischenspeichern

Azure PowerShell verfügt über bestimmte Cmdlets zum Verwalten von VMs und Datenträger.

Die folgende Tabelle enthält einige der-Cmdlets, die in der nächsten Übung wir verwenden:

|Get-Help  |Beschreibung  |
|---------|---------|
|`Get-AzureRmVM`     |  Ruft die Eigenschaften eines virtuellen Computers ab.       |
|`Update-AzureRmVM`     |  Aktualisiert den Status des virtuellen Azure-Computer.       |
|`New-AzureRmDiskConfig`     |  Erstellt ein konfigurierbares Disk-Objekt.       |
|`Add-AzureRmVMDataDisk`     |  Fügt einen Datenträger an einen virtuellen Computer an.   |

Wir verwenden diese Cmdlets in der nächsten Übung Verwaltung der Zwischenspeicherung auf dem virtuellen Computer ein.
