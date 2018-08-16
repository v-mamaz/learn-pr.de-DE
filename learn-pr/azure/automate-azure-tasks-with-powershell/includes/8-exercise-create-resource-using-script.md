
In dieser Übung wird das Beispiel für ein Unternehmen fortgesetzt werden, mit der Linux-Verwaltungstools. Denken Sie daran, dass Sie virtuelle Linux-Computer zu verwenden, um potenzielle Kunden das Testen Ihrer Software ermöglichen möchten. Sie haben eine Ressourcengruppe bereit, und nun ist es Zeit, um die virtuellen Computer zu erstellen.

Ihr Unternehmen hat für einen Stand auf einer großen Linux Messe bezahlt. Einen Demo-Bereich, enthält jede drei Terminals mit einer separaten Linux-VM verbunden werden sollen. Am Ende des Tages möchten Sie die virtuellen Computer löschen und neu erstellen, sodass sie neue jeden Morgen beginnen. Erstellen die virtuellen Computer manuell aus, nachdem die Arbeit, wenn Sie es vielleicht leid, sind unter Umständen Fehler unterlaufen würde. Ein PowerShell-Skript zur Automatisierung des Erstellungsprozesses des virtuellen Computers schreiben möchten.

## <a name="write-a-script-that-creates-virtual-machines"></a>Schreiben Sie ein Skript, virtuelle Computer erstellt.

Um das Skript zu erstellen, gehen Sie wie folgt vor:

1. Erstellen Sie eine neue Textdatei mit dem Namen **ConferenceDailyReset.ps1**.

1. Erfassen Sie den Parameter in einer Variablen:

    ```powershell
    param([string]$resourceGroup)
    ```

1. Authentifizieren Sie bei Azure, die mit Ihren Anmeldeinformationen:

    ```powershell
    Connect-AzureRmAccount
    ```

1. Zum Angeben eines Benutzernamens und Kennworts für die VM Administratorkonto aufgefordert, und das Ergebnis in einer Variablen zu erfassen:

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. Erstellen Sie eine Schleife, die drei Mal ausgeführt wird:

    ```powershell
    For ($i = 1; $i -le 3; $i++) {
    ```

1. Erstellen Sie einen Namen für jeden virtuellen Computer aus, und speichern Sie es in einer Variablen:

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

1. Erstellen eines virtuellen Computers:

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

1. Schließen Sie den Text der Schleife:

    ```powershell
    }
    ```

1. Speichern Sie die Datei .

Das fertiggestellte Skript sollte wie folgt aussehen:

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

## <a name="execute-the-script"></a>Führen Sie das Skript

Starten Sie PowerShell, und wechseln Sie zum Verzeichnis, in dem Sie die Skriptdatei gespeichert. Um das Skript auszuführen, führen Sie den folgenden Befehl aus:

    ```powershell
    .\ConferenceDailyReset.ps1 TrialsResourceGroup
    ```

Das Skript kann einige Minuten dauern. Wenn sie abgeschlossen ist, stellen Sie sicher, dass es erfolgreich ausgeführt wurde:

1. Melden Sie sich im Azure-Portal, in einem Browser.
1. Klicken Sie im Navigationsbereich auf der linken Seite auf **Ressourcengruppen**.
1. In der Liste der Ressourcengruppen anzuzeigen, klicken Sie auf **TrialsResourceGroup**. In der Liste der Ressourcen sollte die neu erstellten virtuellen Computer und den zugehörigen Ressourcen angezeigt werden.

## <a name="summary"></a>Zusammenfassung
Sie schrieb ein Skript, das die Erstellung von drei virtuellen Computer in der Ressourcengruppe, die durch ein Script-Parameter angegebenen automatisiert. Das Skript ist kurz und einfach aber automatisiert den Prozess, der eine lange manuell über das Portal akzeptieren würde.