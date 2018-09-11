Komplexe oder wiederkehrende Aufgaben erfordern häufig viel Zeit für die Verwaltung. Organisationen bevorzugen, diese Aufgaben zu automatisieren, um Kosten zu senken und Fehler zu vermeiden.

Dies ist im Customer Relationship Management-Unternehmensbeispiel wichtig. Dort testen Sie Ihre Software auf mehreren virtuellen Linux-Computern, die Sie kontinuierlich löschen und neu erstellen müssen. Angenommen, Sie möchten ein PowerShell-Skript verwenden, um die Erstellung der virtuellen Computer zu automatisieren.

Bevor Sie einen virtuellen Computer erstellen, müssen einige zusätzliche Voraussetzungen für das Skript erfüllt sein. 
- Sie erstellen mehrere virtuelle Computer, deshalb sollte die Erstellung in einer Schleife stattfinden.
- Sie müssen virtuelle Computer in drei verschiedenen Ressourcengruppen erstellen, der Name der Ressourcengruppe sollte dem Skript also als Parameter übergeben werden.

In diesem Abschnitt sehen Sie, wie Sie ein Azure PowerShell-Skript schreiben und ausführen, das diese Anforderungen erfüllt.

## <a name="what-is-a-powershell-script"></a>Was ist ein PowerShell-Skript?
Ein PowerShell-Skript ist eine Textdatei, die Befehle und Steuerelementkonstrukte enthält. Bei diesen Befehlen handelt es sich um Aufrufe von Cmdlets. Die Steuerelementkonstrukte sind beispielsweise Schleifen, Variablen, Parameter, Kommentare, die von PowerShell bereitgestellt werden.

PowerShell-Skriptdateien haben die Erweiterung **PS1**. Sie können diese Dateien mit jedem Text-Editor erstellen und speichern. 

> [!TIP]
> Wenn Sie PowerShell-Skripts unter Windows schreiben, können Sie PowerShell ISE (Integrated Scripting Environment) verwenden. Dieser Editor stellt Features wie die Syntaxkennzeichnung und eine Liste der verfügbaren Cmdlets bereit.
>
Der folgende Screenshot zeigt die Windows PowerShell Integrated Scripting Environment (ISE) mit einem Beispielskript zum Verbinden mit Azure und Erstellen eines virtuellen Computers in Azure.

>![Screenshot der im Bearbeitungsfenster geöffneten Windows PowerShell Integrated Scripting Environment mit einem Skript zum Erstellen eines virtuellen Computers](../media/7-windows-powershell-ise-screenshot.png)

Sobald Sie dieses Skript geschrieben haben, führen Sie dieses über die PowerShell-Befehlszeile aus, indem Sie den Namen der Datei mit einem vorangestellten Punkt und Schrägstrich übergeben:

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a>PowerShell-Verfahren
PowerShell hat viele Features, die auch in typischen Programmiersprachen vorhanden sind. Sie können Variablen definieren, Branches und Schleifen verwenden, Befehlszeilenparameter erfassen, Funktionen schreiben, Kommentare hinzufügen und vieles mehr. Für unser Skript sind drei Features erforderlich: Variablen, Schleifen und Parameter.

### <a name="variables"></a>Variables
PowerShell unterstützt Variablen. Verwenden Sie **$**, um eine Variable zu deklarieren und **=**, um einen Wert zuzuweisen. Beispiel:

```powershell
$loc = "East US"
$iterations = 3
```

Variablen können Objekte enthalten. Die folgende Definition legt die Variable **adminCredential** beispielsweise auf das Objekt fest, das vom Cmdlet **Get-Credential** zurückgegeben wird.

```powershell
$adminCredential = Get-Credential
```

Verwenden Sie das Präfix **$** und seinen Namen wie im Folgenden dargestellt, um den Wert abzurufen, der in einer Variable gespeichert ist: 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a>Schleifen
PowerShell verfügt über mehrere Schleifen, z.B. **For**, **Do...While** und **For...Each**. Die **For**-Schleife ist für unsere Anforderungen am besten geeignet, da wir ein Cmdlet mit einer festgelegten Häufigkeit ausführen.

Die Hauptsyntax wird im Folgenden dargestellt. Das Beispiel wird für zwei Iterationen ausgeführt und gibt jedes Mal den Wert von **i** aus. Die Vergleichsoperatoren lauten z.B. **-lt** (kleiner als), **-le** (kleiner als oder gleich), **eq** (gleich) oder **ne** (nicht gleich).

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a>Parameter
Wenn Sie ein Skript ausführen, können Sie Argumente über die Befehlszeile übergeben. Sie können ebenfalls Namen für jeden Parameter bereitstellen, damit das Skript die Werte extrahieren kann. Beispiel: 

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

Innerhalb des Skripts erfassen Sie die Werte in Variablen. In diesem Beispiel werden die Parameter nach Namen abgeglichen:

```powershell
param([string]$location, [int]$size)
```

Sie können die Namen weglassen, wenn Sie die Befehlszeile verwenden. Beispiel: 

```powershell
.\setupEnvironment.ps1 5 "East US"
```

Verwenden Sie innerhalb des Skripts Position für den Abgleich, wenn die Parameter unbenannt sind:

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a>Erstellen eines benutzerdefinierten virtuellen Linux-Computers
Azure PowerShell stellt das Cmdlet **New-AzureRmVm** bereit, um einen virtuellen Computer zu erstellen. Das Cmdlet hat viele Parameter, um die große Anzahl von Konfigurationseinstellungen für virtuelle Computer zu verarbeiten. Die meisten Parameter haben sinnvolle Standardwerte, deshalb müssen Sie nur fünf Werte angeben:

- **ResourceGroupName:** Die Ressourcengruppe, in der der neue virtuelle Computer platziert wird.
- **Name:** Der Name des virtuellen Computers in Azure.
- **Location:** Der geografische Standort, in dem der virtuelle Computer bereitgestellt wird.
- **Credential:** Ein Objekt, das den Benutzernamen und das Kennwort für das Administratorkonto des virtuellen Computers enthält. Wir verwenden das Cmdlet **Get-Credential**, um den Benutzer zur Eingabe eines Benutzernamens und eines Kennworts aufzufordern. **Get-Credential** packt den Benutzernamen und das Kennwort in ein Credential-Objekt, das diese als Ergebnis zurückgibt.
- **Image:** Identität des Betriebssystems, das für den virtuellen Computer verwendet werden soll. Wir verwenden „UbuntuLTS“.

Die Syntax für das Cmdlet wird im Folgenden dargestellt:

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a>Zusammenfassung
Durch die Kombination von PowerShell und Azure PowerShell können Sie alle Tools nutzen, die Sie für die Automatisierung von Azure benötigen. In unserem CRM-Beispiel können wir mehrere virtuelle Linux-Computer mithilfe eines Parameters erstellen, damit das Skript generisch bleibt. Außerdem kann eine Schleife erstellt werden, um wiederholten Code zu vermeiden. Das bedeutet, dass ein zuvor komplexer Vorgang nun in einem einzigen Schritt ausgeführt werden kann.