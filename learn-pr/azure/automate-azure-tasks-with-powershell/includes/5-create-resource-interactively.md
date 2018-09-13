Mit Azure PowerShell können Sie Befehle schreiben und diese sofort ausführen. Wird als **interaktiver Modus** bezeichnet.

Denken Sie daran, dass das Ziel im CRM-Beispiel (Customer Relationship Management) darin besteht, drei Testumgebungen zu erstellen, die virtuelle Computer enthalten. Sie verwenden Ressourcengruppen, um sicherzustellen, dass die virtuellen Computer in separaten Umgebungen organisiert sind: einer für Komponententests, einer für Integrationstests und einer für Benutzerakzeptanztests. Sie müssen die Ressourcengruppen nur einmal erstellen, der interaktive Modus von PowerShell ist daher eine gute Wahl.

In diesem Abschnitt werden einige Beispiele dargestellt, wie PowerShell interaktiv verwendet wird, um sich bei einem Azure-Abonnement anzumelden und Ressourcengruppen zu erstellen.

## <a name="what-are-powershell-cmdlets"></a>Was sind PowerShell-Cmdlets?
Ein PowerShell-Befehl wird als **Cmdlet** (ausgesprochen: „Command-let“) bezeichnet. Ein Cmdlet ist ein Befehl, der ein einzelnes Feature bearbeitet. Der Begriff **Cmdlet** soll „kleiner Befehl“ heißen. Gemäß der Konvention wird Cmdlet-Autoren empfohlen, Cmdlets einfach zu halten und nur für einen einzigen Zweck zu erstellen.

Im PowerShell-Basisprodukt sind Cmdlets enthalten, die mit Features wie Sitzungen und Hintergrundaufträgen funktionieren. Fügen Sie Module zu Ihrer PowerShell-Installation hinzu, damit Cmdlets andere Features ändern können. Es gibt z.B. Drittanbietermodule für die Arbeit mit FTP, das Verwalten Ihres Betriebssystems oder das Zugreifen auf das Dateisystem.

Die Namenskonvention bei Cmdlets ist „Verb-Substantiv“, z.B. **Get-Process**, **Format-Table**, and **Start-Service**. Es gibt ebenfalls eine Konvention für die Auswahl des Verbs, z.B. „get“ zum Abrufen von Daten, „set“ zum Einfügen oder Aktualisieren von Daten, „format“ zum Formatieren von Daten oder „out“, um die Ausgabe einem Ziel zuzuweisen.

Cmdlet-Autoren wird empfohlen, eine Hilfedatei für jedes Cmdlet beizufügen. Das Cmdlet **Get-Help** zeigt die Hilfedatei für ein Cmdlet an:

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>Was ist AzureRM?
**AzureRM** ist der formelle Name des Azure PowerShell-Moduls, das die Cmdlets enthält, die mit den Azure-Features zusammenarbeiten sollen (das **RM** im Namen steht für **Resource Manager**). Es enthält hunderte Cmdlets, mit denen Sie nahezu jeden Aspekt jeder Azure-Ressource regulieren können. Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory, Containern, Machine Learning usw. arbeiten.

## <a name="how-to-create-a-resource-group"></a>Erstellen einer Ressourcengruppe
Als Nächstes erstellen Sie eine Ressourcengruppe mit einer lokalen Installation von Azure PowerShell. 

Dazu sind vier Schritte notwendig: 

1. Importieren Sie die Azure-Cmdlets.

1. Stellen Sie eine Verbindung mit Ihrem Azure-Abonnement her.

1. Erstellen Sie die Ressourcengruppe.

1. Stellen Sie sicher, dass das Erstellen erfolgreich war.

Die folgende Abbildung zeigt eine Übersicht dieser Schritte.

![Eine Abbildung, die die Schritte zum Erstellen einer Ressourcengruppe zeigt.](../media/5-create-resource-overview.png)

Jeder Schritt entspricht einem anderen Cmdlet.

### <a name="import"></a>Importieren
PowerShell lädt beim Start standardmäßig nur die wichtigsten Cmdlets. Das bedeutet, dass das Cmdlet, dass mit Azure arbeiten muss, nicht geladen wird. Die zuverlässigste Option zum Laden der benötigten Cmdlets besteht darin, diese manuell zu Beginn der PowerShell-Sitzung zu importieren.

Sie verwenden das Cmdlet **Import-Module** zum Laden von Modulen. Dieses Cmdlet verfügt über viele Parameter, die für unterschiedliche Situationen geeignet sind. Beispielsweise kann es mehrere Module, eine bestimmte Modulversion, Teile eines Moduls usw. laden. Die Syntax ist einfach, wenn Sie ein gesamtes Modul laden möchten:

```powershell
Import-Module <module-name>
```

> [!TIP]
> Wenn Sie häufig mit Azure PowerShell arbeiten, gibt es zwei Möglichkeiten, den Modulladeprozess zu automatisieren. Sie können Ihrem PowerShell-Profil einen Eintrag hinzufügen, um das Azure-Modul beim Start zu importieren, oder die aktuellste Versionen von PowerShell verwenden, die das enthaltende Modul automatisch lädt, wenn Sie das Cmdlet verwenden.

### <a name="connect"></a>Verbinden
Da Sie mit einer lokalen Installation von Azure PowerShell arbeiten, müssen Sie sich zunächst authentifizieren, um Azure-Befehle ausführen zu können. Das Cmdlet **Connect-AzureRmAccount** ruft Ihre Azure-Anmeldeinformationen ab und stellt dann eine Verbindung mit Ihrem Azure-Abonnement her. Es hat viele optionale Parameter. Wenn Sie jedoch nur eine interaktive Eingabeaufforderung benötigen, sind keine Parameter erforderlich:

```powershell
Connect-AzureRmAccount
```

### <a name="create"></a>Erstellen
Verwenden Sie das Cmdlet **New-AzureRmResourceGroup**, um eine Ressourcengruppe zu erstellen. Sie müssen einen Namen und einen Standort angeben. Der Name muss innerhalb Ihres Abonnements eindeutig sein. Der Standort bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden (was für Sie aus Konformitätsgründen wichtig sein kann). Verwenden Sie Zeichenfolgen wie „USA, Westen“, „Europa, Norden“ oder „Indien, Westen“, um den Standort anzugeben. Wie die meisten Azure-Cmdlets hat auch **New-AzureRmResourceGroup** viele optionale Parameter. Die grundlegende Syntax ist die folgende:

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

### <a name="verify"></a>Überprüfen
Das Cmdlet **Get-AzureRmResource** listet Ihre Azure-Ressourcen auf. So können wir hier überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde.

```powershell
Get-AzureRmResource
```

Senden Sie die Ausgabe des Cmdlets **Get-AzureRmResource** an das Cmdlet **Format-Table** mit dem senkrechten Strich „|“.

```powershell
Get-AzureRmResource | Format-Table
```

## <a name="summary"></a>Zusammenfassung
Der interaktive Modus von PowerShell eignet sich für einmalige Aufgaben. In unserem Beispiel verwenden wir die gleiche Ressourcengruppe für das gesamte Projekt, weshalb es sinnvoll ist, sie als interaktive Ressourcengruppe zu erstellen. Der interaktive Modus erweist sich für diesen Task oft als schneller und einfacher als das Schreiben eines Skripts, das Sie dann nur einmal ausführen.