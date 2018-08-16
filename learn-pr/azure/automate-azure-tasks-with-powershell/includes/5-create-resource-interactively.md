## <a name="motivation"></a>Motivation
Azure PowerShell können Sie die Befehle schreiben, und führen Sie sie. Dies bezeichnet man als **im interaktiven Modus**.

Denken Sie daran, dass das Ziel im Beispiel (Customer Relationship Management, CRM) besteht darin, drei Test-Umgebungen mit virtuellen Computern zu erstellen. Sie können Ressourcengruppen, um sicherzustellen, dass die virtuellen Computer werden in separaten Umgebungen organisiert: eins für Komponententests bereit, eine für Integrationstests und für Tests der Benutzerakzeptanz. Sie müssen nur einmal für die Ressourcengruppen zu erstellen, d. h., die im interaktiven Modus von PowerShell eine gute Wahl ist.

In diesem Abschnitt erfahren Sie, wie Sie mithilfe von PowerShell interaktiv anmelden beim Azure-Abonnement, und erstellen Sie Ressourcengruppen.

## <a name="what-are-powershell-cmdlets"></a>Welche PowerShell-Cmdlets sind?
Ein PowerShell-Befehl aufgerufen wird eine **Cmdlet** (ausgesprochen "Command-Let"). Ein Cmdlet ist ein Befehl, der eine einzelne Funktion bearbeitet. Der Begriff **Cmdlet** richtet sich an "kleine Befehl" impliziert. Gemäß der Konvention werden Cmdlet-Autoren wird empfohlen, die Cmdlets auf einfache und einzelnen Zweck zu halten.

Das PowerShell-Basisprodukt Lieferumfang von Cmdlets, die Arbeit mit Funktionen wie Sitzungen und Hintergrundaufträge ab. Die PowerShell-Installation um Cmdlets zu erhalten, die andere Funktionen ändern hinzugefügt Module. Es gibt z. B. Drittanbieter-Module zum Arbeiten mit ftp, verwalten Ihr Betriebssystem, das Zugriff auf das Dateisystem usw.

Cmdlets folgen eine Verb-Substantiv-Namenskonvention gilt. z. B. **Get-Process**, **Format-Table**, und **Start-Service**. Es gibt auch eine Konvention für das Verb Wahl: "get", um Daten abzurufen, "set" zum Einfügen oder Aktualisieren von Daten, "formatieren" für die direkte Ausgabe an ein Ziel usw. zum Formatieren von Daten "out".

Cmdlet-Autoren werden empfohlen, eine Hilfedatei für die einzelnen Cmdlets enthalten. Die **Get-Help** Cmdlet zeigt an, der die Hilfedatei für ein Cmdlet:

```
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>Was ist AzureRM?
**AzureRM** der formelle Name für das Azure PowerShell-Modul enthält Cmdlets zum Arbeiten mit Azure-Features (die **RM** im Namen steht für **Resource Manager**). Es enthält Hunderte von Cmdlets, mit denen Sie fast jeden Aspekt aller Azure-Ressourcen zu steuern. Arbeiten mit Ressourcengruppen, Speicher, virtuelle Computer können Sie Azure Active Directory, Container, Machine Learning.

## <a name="how-to-create-a-resource-group"></a>Gewusst wie: Erstellen einer Ressourcengruppe
Als Nächstes erstellen wir eine Ressourcengruppe mit einer lokalen Installation von Azure PowerShell. 

Es sind vier Schritte notwendig: 
1. Importieren der Azure-cmdlets
1. Verbinden mit Ihrem Azure-Abonnement
1. Ressourcengruppe erstellen
1. Stellen Sie sicher, dass die Erstellung erfolgreich (siehe unten) wurde.

![Schritte zum Erstellen einer Ressource in Azure mithilfe von Azure PowerShell](../images/5-MOCKUP-create-resource-overview.png)

Jeder Schritt entspricht einem anderen Cmdlet.

### <a name="import"></a>Importieren
Beim Start lädt PowerShell nur die Kern-Cmdlets in der Standardeinstellung an. Dies bedeutet, dass die Cmdlets müssen Sie für die Arbeit mit Azure wird nicht geladen werden. Die zuverlässigste Möglichkeit, um die Cmdlets zu laden, die Sie benötigen, ist am Anfang der PowerShell-Sitzung manuell importieren.

Sie verwenden die **Import-Module** Cmdlet-Module laden. Dieses Cmdlet verfügt über viele Parameter, um eine Vielzahl von Situationen zu behandeln. Beispielsweise können sie laden mehrere Module, ein bestimmtes Modulversion, die Teil eines Moduls usw. Um ein Modul während des gesamten Entwicklungsprozesses zu laden, ist einfach die Syntax auf:

```powershell
Import-Module <module-name>
```

> [!TIP] Wenn Sie feststellen, dass Sie häufig mit Azure PowerShell arbeiten, gibt es zwei Möglichkeiten, die Sie das Laden von Modulen automatisieren können. Sie können einen Eintrag hinzufügen, um das PowerShell-Profil importieren das Azure-Modul beim Start aus, oder verwenden die neuesten Versionen von PowerShell das enthaltende Modul automatisch geladen, wenn Sie ein Cmdlet verwenden.

### <a name="connect"></a>Verbinden
Da Sie mit einer lokalen Installation von Azure PowerShell arbeiten, müssen Sie sich authentifizieren, bevor Sie Azure-Befehle ausführen können. Die **Connect-AzureRmAccount** -Cmdlet für Ihre Azure-Anmeldeinformationen aufgefordert werden, und klicken Sie dann eine Verbindung mit Ihrem Azure-Abonnement her. Es weist viele optionale Parameter, jedoch ist alles, was Sie benötigen eine interaktive Eingabeaufforderung, klicken Sie dann keine Parameter benötigt werden:

```powershell
Connect-AzureRmAccount
```

### <a name="create"></a>Erstellen
Die **New-AzureRmResourceGroup** -Cmdlet erstellt eine Ressourcengruppe aus. Sie müssen einen Namen und Speicherort angeben. Der Name muss innerhalb Ihres Abonnements eindeutig sein. Die Position bestimmt, die Metadaten für Ihre Ressourcengruppe gespeichert wird (der Compliance-Gründen wichtig sein kann). Sie verwenden Zeichenfolgen wie "USA, Westen", "Europa, Norden" und "Indien (Westen)", um den Speicherort anzugeben. Wie bei den meisten Azure-Cmdlets, **New-AzureRmResourceGroup** weist viele optionale Parameter ist jedoch der grundlegenden Syntax:

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

### <a name="verify"></a>Überprüfen
Die **Get-AzureRmResource** Listet Ihre Azure-Ressourcen. Dies ist hier nützlich zu überprüfen, ob die Erstellung der Ressourcengruppe erfolgreich war.

```powershell
Get-AzureRmResource
```

Um eine präzisere Ansicht zu erhalten, können Sie die Ausgabe senden die **Get-AzureRmResource** auf die **Format-Table** Cmdlet mithilfe einer Pipe "|".

```powershell
Get-AzureRmResource | Format-Table
```

## <a name="summary"></a>Zusammenfassung
PowerShell interaktive Modus ist für einmalige Aufgaben geeignet. In unserem Beispiel verwenden wir die gleiche Ressourcengruppe für die Lebensdauer des Projekts Dies bedeutet, dass es interaktiven erstellen angemessen ist. Im interaktiver Modus ist häufig schneller und einfacher für diese Aufgabe als ein Skript zu schreiben und das Skript genau einmal ausgeführt.