In dieser Einheit machen Sie mit dem Beispiel einer Firma weiter, die Linux-Verwaltungstools herstellt. Wie bereits besprochen planen Sie, Linux-VMs zu verwenden, um potenzielle Kunden Ihre Software testen zu lassen. Eine Ressourcengruppe steht bereit, und nun ist es an der Zeit, die VMs zu erstellen.

Ihr Unternehmen hat einen Stand auf einer großen Linux-Messe gebucht. Sie planen einen Demobereich mit drei Terminals, die jeweils an eine separate Linux-VM angeschlossen sind. Am Ende jedes Tages möchten Sie die VMs löschen und neu erstellen, damit sie jeden Morgen neu starten können. Das manuelle Erstellen der VMs nach der Arbeit, wenn Sie erschöpft sind, wäre zu fehleranfällig. Sie möchten ein PowerShell-Skript schreiben, um die Erstellung der VMs zu automatisieren.

## <a name="write-a-script-that-creates-virtual-machines"></a>Schreiben eines Skripts zum Erstellen virtueller Computer

Gehen Sie in Cloud Shell auf der rechten Seite wie folgt vor, um das Skript zu schreiben:

1. Wechseln Sie in Cloud Shell zu Ihrem Stammordner.

    ```powershell
    cd $HOME\clouddrive
    ```

1. Erstellen Sie eine neue Textdatei namens **ConferenceDailyReset.ps1**.

    ```powershell
    touch "./ConferenceDailyReset.ps1"
    ```

1. Öffnen Sie den integrierten Editor, und wählen Sie die Datei **ConferenceDailyReset.ps1** aus.

    ```powershell
    code "./ConferenceDailyReset.ps1"
    ```
    > [!TIP]
    > Die integrierte Cloud Shell-Instanz unterstützt auch Vim, Nano und Emacs, falls Sie lieber einen dieser Editoren verwenden möchten.

1. Erfassen Sie zunächst die Eingabeparameter in einer Variablen. Fügen Sie Ihrem Skript die folgende Zeile hinzu:

    ```powershell
    param([string]$resourceGroup)
    ```

    > [!NOTE]
    > Normalerweise müssen Sie sich bei Azure unter Verwendung von `Connect-AzureRmAccount` mit Ihren Anmeldeinformationen authentifizieren, was über das Skript erfolgen kann. Da Sie in der Cloud Shell-Umgebung allerdings bereits authentifiziert sind, ist dieser Schritt nicht erforderlich.

1. Fordern Sie zur Eingabe eines Benutzernamens und Kennworts für das Administratorkonto des virtuellen Computers auf, und erfassen Sie das Ergebnis in einer Variablen:

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. Erstellen Sie eine Schleife, die dreimal ausgeführt wird:

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

1. Erstellen Sie im Schleifentext einen Namen für jeden virtuellen Computer, speichern Sie ihn in einer Variablen, und geben Sie ihn in der Konsole aus:

    ```powershell
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    ```

1. Erstellen Sie als Nächstes einen virtuellen Computer unter Verwendung der Variablen `$vmName`:

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
   ```

1. Speichern Sie die Datei. Dazu können Sie das Menü „...“ rechts oben im Editor verwenden. Zum Speichern können aber auch die gängigen Zugriffstasten verwendet werden.

Das fertige Skript sollte wie folgt aussehen:

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>Ausführen des Skripts

Schließen Sie den Editor über das Kontextmenü „...“.

1. Führen Sie das Skript aus.

    ```powershell
    .\ConferenceDailyReset.ps1 <rgn>[Sandbox resource group name]</rgn>
    ```
    
Die Skriptausführung dauert ein paar Minuten. Vergewissern Sie sich anschließend, dass es erfolgreich ausgeführt wurde. Sehen Sie sich dazu die Ressourcen an, die nun in Ihrer Ressourcengruppe zur Verfügung stehen:

```powershell
Get-AzureRmResource -ResourceType Microsoft.Compute/virtualMachines
```

Es sollten drei virtuelle Computer mit jeweils eindeutigem Namen angezeigt werden.

Sie haben ein Skript geschrieben, das die Erstellung dreier virtueller Computer in der durch einen Skriptparameter angegebenen Ressourcengruppe automatisiert. Das Skript ist kurz und einfach, automatisiert aber einen Prozess, der im Portal viel Zeit in Anspruch nehmen würde.