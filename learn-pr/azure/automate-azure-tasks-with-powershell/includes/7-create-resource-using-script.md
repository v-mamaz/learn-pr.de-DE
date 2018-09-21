Komplexe oder wiederkehrende Aufgaben erfordern häufig viel Zeit für die Verwaltung. Organisationen bevorzugen, diese Aufgaben zu automatisieren, um Kosten zu senken und Fehler zu vermeiden.

Dies ist im Customer Relationship Management-Unternehmensbeispiel wichtig. Dort testen Sie Ihre Software auf mehreren virtuellen Linux-Computern, die Sie kontinuierlich löschen und neu erstellen müssen. Sie sollten ein PowerShell-Skript zum Automatisieren der Erstellung von VMs verwenden, anstatt sie jedes Mal auf die gleiche Weise wie eben manuell zu erstellen.

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

### <a name="variables"></a>Variablen
Wie Sie bereits in der vorherigen Einheit erfahren haben, unterstützt PowerShell die Verwendung von Variablen. Verwenden Sie **$** zum Deklarieren einer Variablen, und verwenden Sie **=** zum Zuweisen eines Werts. Beispiel:

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

Im Skript verlassen Sie sich auf die Position beim Abgleich, wenn die Parameter nicht benannt sind:

```powershell
param([int]$size, [string]$location)
```

Sie können diese Parameter als Eingabe nutzen, und eine Schleife verwenden, um mehrere VMs anhand der angegebenen Parameter zu erstellen. Das sehen Sie sich als Nächstes an.

Durch die Kombination von PowerShell und Azure PowerShell können Sie alle Tools nutzen, die Sie für die Automatisierung von Azure benötigen. In unserem CRM-Beispiel können wir mehrere virtuelle Linux-Computer mithilfe eines Parameters erstellen, damit das Skript generisch bleibt. Außerdem kann eine Schleife erstellt werden, um wiederholten Code zu vermeiden. Das bedeutet, dass ein zuvor komplexer Vorgang nun in einem einzigen Schritt ausgeführt werden kann.