## <a name="motivation"></a>Motivation
Komplexe und wiederkehrende Aufgaben nutzen häufig viel Zeit bei der Verwaltung. Organisationen bevorzugen zur Automatisierung dieser Aufgaben aus, um Kosten zu senken und Fehler zu vermeiden.

Dies ist wichtig, im Beispiel Unternehmen (Customer Relationship Management, CRM). Testen Sie Ihre Software auf mehrere virtuelle Linux-Computer (VMs), die Sie kontinuierlich löschen und neu erstellen müssen. Möchten ein PowerShell-Skript zu verwenden, um die Erstellung der virtuellen Computer zu automatisieren.

Über den Basisbetrieb Erstellen eines virtuellen Computers müssen Sie einige zusätzliche Anforderungen für das Skript aus. 
- Mehrere virtuelle Computer, erstellen Sie daher die Erstellung in einer Schleife aufgenommen werden soll
- Sie müssen in drei verschiedenen Ressourcengruppen, VMs erstellen, damit der Name der Ressourcengruppe an das Skript als Parameter übergeben werden sollen

In diesem Abschnitt sehen Sie, wie Sie schreiben, und führen Sie ein Azure PowerShell-Skript, das diese Anforderungen erfüllt.

## <a name="what-is-a-powershell-script"></a>Was ist ein PowerShell-Skript?
Ein PowerShell-Skript ist eine Textdatei mit Befehlen und Steuerelement erstellt. Die Befehle sind die Aufrufe der Cmdlets. Die Steuerelementkonstrukte sind Funktionen wie Schleifen, Variablen, Parameter, Kommentare, usw., die vom PowerShell Programmierung.

PowerShell-Skriptdateien haben ein **ps1** Dateierweiterung. Sie können zu erstellen und speichern diese Dateien mit einem beliebigen Texteditor. 

> [!TIP] Wenn Sie in Windows PowerShell-Skripts schreiben, können Sie die Windows PowerShell Integrated Scripting Environment (ISE) verwenden. Dieser Editor bietet es sich um Features wie farbliche syntaxkennzeichnung und eine Liste der verfügbaren Cmdlets.
>
>![Der Windows PowerShell ISE](../images/7-windows-powershell-ise-screenshot.png)

Nachdem Sie das Skript geschrieben haben, führen Sie es über die PowerShell-Befehlszeile durch Übergeben des Namens der Datei, einem Punkt und ein umgekehrter Schrägstrich vorangestellt:

    ```powershell
    .\myScript.ps1
    ```

## <a name="powershell-techniques"></a>PowerShell-Verfahren
PowerShell umfasst viele Features, die in typischen Programmiersprachen gefunden. Sie können definieren Sie Variablen, Verzweigungen und Schleifen, erfassen Befehlszeilenparameter, Schreiben von Funktionen, Hinzufügen von Kommentaren usw. Wir benötigen drei Funktionen für unser Skript: Variablen, Schleifen und Parameter.

### <a name="variables"></a>Variables
PowerShell unterstützt Variablen. Verwendung **$** zum Deklarieren einer Variablen und **=** , einen Wert zuzuweisen. Beispiel:

    ```powershell
    $loc = "East US"
    $iterations = 3
    ```

Variablen können Objekte enthalten. Die folgende Definition legt z. B. die **AdminCredential** -Variable auf das von zurückgegebene Objekt der **Get-Credential** Cmdlet.

    ```powershell
    $adminCredential = Get-Credential
    ```

Verwenden Sie zum Abrufen des in einer Variablen gespeicherten Wertes dem **$** Präfix und den Namen, wie unten dargestellt: 

    ```powershell
    $loc = "East US"
    New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
    ```

### <a name="loops"></a>Schleifen
PowerShell verfügt über mehrere Schleifen: **für**, **tun... Während**, **für... Jede**usw. Die **für** Schleife ist die beste Übereinstimmung für unsere Anforderungen, da wir ein Cmdlet eine feste Anzahl von ausgeführt wird.

Die Core-Syntax ist unten dargestellt; In diesem Beispiel wird für zwei Iterationen ausgeführt und den Wert des **ich** jedes Mal. Die Vergleichsoperatoren werden geschrieben, **- Lt** für "kleiner als" **-le** für "kleiner als oder gleich" **Eq** für "gleich" **Ne** für "nicht gleich", usw.

    ```powershell
    For ($i = 1; $i -lt 3; $i++)
    {
        $i
    }
    ```

### <a name="parameters"></a>Parameter
Wenn Sie ein Skript ausführen, können Sie Argumente in der Befehlszeile übergeben. Sie können Namen für jeden Parameter können Sie das Skript die Werte zu extrahieren, bereitstellen. Beispiel:

    ```powershell
    .\setupEnvironment.ps1 -size 5 -location "East US"
    ```

Innerhalb des Skripts erfassen Sie die Werte in Variablen an. In diesem Beispiel werden die Parameter nach Namen abgeglichen:

    ```powershell
    param([string]$location, [int]$size)
    ```

Sie können die Namen über die Befehlszeile weglassen. Beispiel:

    ```powershell
    .\setupEnvironment.ps1 5 "East US"
    ```

Verwenden Sie innerhalb des Skripts Position für den Abgleich, wenn der Parameter unbenannt sind:

    ```powershell
    param([int]$size, [string]$location)
    ```

## <a name="how-to-create-a-linux-virtual-machine"></a>Vorgehensweise: Erstellen einer Linux-VM
Azure PowerShell bietet die **New-AzureRmVm** -Cmdlet zum Erstellen eines virtuellen Computers. Das Cmdlet verfügt über viele Parameter, damit es die große Anzahl von VM-Konfigurationseinstellungen verarbeiten kann. Die meisten Parameter haben sinnvolle Standardwerte, daher wir nur fünf Dinge anzugeben müssen:
- **ResourceGroupName**: die Ressourcengruppe, in dem der neue virtuelle Computer platziert werden.
- **Namen**: der Name des virtuellen Computers in Azure.
- **Speicherort**: geografischen Standort, in dem der virtuelle Computer bereitgestellt werden.
- **Anmeldeinformationen**: ein Objekt mit dem Benutzernamen und Kennwort für das Administratorkonto des virtuellen Computers. Wir verwenden die **Get-Credential** Cmdlet zur Eingabe eines Benutzernamens und Kennworts auffordert. **Get-Credential** Pakete des Benutzernamens und Kennworts in ein Objekt mit Anmeldeinformationen der als Ergebnis zurückgegeben.
- **Image**: Identität des Betriebssystems für den virtuellen Computer verwendet werden soll. Wir verwenden "UbuntuLTS".

Die Syntax für das Cmdlet ist unten dargestellt:

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a>Zusammenfassung
Die Kombination von PowerShell und Azure PowerShell bietet Ihnen die Tools, die für die Sie benötigen, Automatisieren von Azure. In unserem Beispiel CRM werden wir erstellen mehrere Linux-VMs, die mit einem Parameter, um das Skript generische zu halten und einer Schleife, um wiederholte Code zu vermeiden. Dies bedeutet, dass ein ehemals komplexer Vorgang jetzt in einem einzigen Schritt ausgeführt werden kann.