Das Erstellen von Verwaltungsskripts ist eine leistungsstarke Möglichkeit, Ihren Workflow zu optimieren. Sie können gängige, sich wiederholende Aufgaben automatisieren. Nachdem ein Skript überprüft wurde, wird es konsistent ausgeführt, was wahrscheinlich das Auftreten von Fehler reduziert. In der vorherigen Übung haben wir über das Azure-Portal eine VM erstellt, einen Datenträger für Daten hinzugefügt und Cacheeinstellungen geändert. Was wäre, wenn wir diese Aufgaben auf vielen VMs in vielen Regionen wiederholen müssten? Dazu würden wir auf Azure PowerShell zurückgreifen.

> [!TIP]
> Azure PowerShell wird im Modul **Automatisieren von Microsoft Azure-Aufgaben mit PowerShell** ausführlich behandelt. In diesem Modul finden Sie weitere Details zur Installation, Konfiguration und Verwendung von PowerShell.

## <a name="what-is-azure-powershell"></a>Was ist Azure PowerShell?

Azure PowerShell ist ein plattformübergreifendes Befehlszeilentool, mit dem Sie eine Verbindung mit Ihrem Azure-Abonnement herstellen und Ressourcen verwalten. Es ist die Kombination zweier Elemente: **PowerShell**, das Befehlszeilentool-Unterstützung bietet, und **AzureRM**, das die (als „Cmdlets“ bezeichneten) Befehle für das Arbeiten mit Azure bereitstellt. 

Azure PowerShell bietet Cmdlets, mit denen Sie die meisten Aspekte von Azure-Ressourcen bearbeiten können. Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory, Containern, maschinellem Lernen usw. arbeiten. Alle diese Details werden in anderen Schulungsmodulen behandelt.

### <a name="powershell-cmdlets-for-managing-azure-disk-caching"></a>PowerShell-Cmdlets zum Verwalten der Azure-Datenträgerzwischenspeicherung

Azure PowerShell verfügt über spezifische Cmdlets zum Verwalten von VMs und Datenträgern.

|Befehl  | Beschreibung |
|---------|-------------|
| `Get-AzureRmVM`         | Dient zum Abrufen der Eigenschaften eines virtuellen Computers.       |
| `Update-AzureRmVM`      | Aktualisiert den Status des virtuellen Azure-Computers.  |
| `New-AzureRmDiskConfig` | Erstellt ein konfigurierbares Datenträgerobjekt.             |
| `Add-AzureRmVMDataDisk` | Fügt einen Datenträger einem virtuellen Computer hinzu.          |

Hiermit können wir alle Aufgaben ausführen, die wir im Azure-Portal ausgeführt haben. Lassen Sie es uns auf unserem virtuellen Computer ausprobieren.
