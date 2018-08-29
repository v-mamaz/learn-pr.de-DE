In dieser Übung fahren Sie mit dem Beispiel einer Firma fort, die Linux-Verwaltungstools herstellt. Rufen Sie sich in Erinnerung, dass Sie planen, Linux-VMs zu verwenden, um potenzielle Kunden Ihre Software testen zu lassen. Eine Ressourcengruppe steht bereit, und nun ist es an der Zeit, die VMs zu erstellen.

Ihr Unternehmen hat einen Stand auf einer großen Linux-Messe gebucht. Sie planen einen Demobereich mit drei Terminals, die jeweils an eine separate Linux-VM angeschlossen sind. Am Ende jedes Tages möchten Sie die VMs löschen und neu erstellen, damit sie jeden Morgen neu starten können. Das manuelle Erstellen der VMs nach der Arbeit, wenn Sie erschöpft sind, wäre zu fehleranfällig. Sie möchten ein PowerShell-Skript schreiben, um die Erstellung der VMs zu automatisieren.

## <a name="write-a-script-that-creates-virtual-machines"></a>Schreiben eines Skripts zum Erstellen virtueller Computer

Gehen Sie folgendermaßen vor, um das Skript zu schreiben:

1. Erstellen Sie eine neue Textdatei mit dem Namen **ConferenceDailyReset.ps1**.

2. Erfassen Sie den Parameter in einer Variablen:

    ```powershell
    param([string]$resourceGroup)
    ```

3. Authentifizieren Sie sich bei Azure mit Ihren Anmeldeinformationen:

    ```powershell
    Connect-AzureRmAccount
    ```

4. Fordern Sie einen Benutzernamen und ein Kennwort für das Administratorkonto der VM an, und erfassen Sie das Ergebnis in einer Variablen:

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. Erstellen Sie eine Schleife, die dreimal ausgeführt wird:

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. Erstellen Sie im Schleifentext einen Namen für jede VM, und speichern Sie ihn in einer Variablen:

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. Erstellen Sie als Nächstes eine VM mithilfe der Variablen `$vmName`:

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. Speichern Sie die Datei.

Die fertige Skript sollte wie folgt aussehen:

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>Ausführen des Skripts

Starten Sie PowerShell, und wechseln Sie zum Verzeichnis, in dem Sie die Skriptdatei gespeichert haben. Geben Sie den folgenden Befehl ein, um das Skript auszuführen:

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

Die Ausführung des Skripts kann einige Minuten dauern. Wenn sie abgeschlossen ist, stellen Sie sicher, dass es erfolgreich ausgeführt wurde:

1. Melden Sie sich in einem Browser beim Azure-Portal an.
2. Klicken Sie im linken Navigationsbereich auf **Ressourcengruppen**.
3. Klicken Sie in der Liste der Ressourcengruppen auf **TrialsResourceGroup**. In der Liste der Ressourcen sollten Sie die neu erstellten VMs und die zugehörigen Ressourcen vorfinden.

## <a name="summary"></a>Zusammenfassung
Sie haben ein Skript geschrieben, das die Erstellung dreier VMs in der von einem Skriptparameter angegebenen Ressourcengruppe automatisiert. Das Skript ist kurz und einfach, automatisiert aber einen Prozess, der im Portal viel Zeit in Anspruch nehmen würde.