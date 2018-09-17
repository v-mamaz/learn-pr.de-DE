Für den MEAN-Komponentenstapel wird ein Server benötigt. Sie können entweder einen Linux-Computer oder einen virtuellen Computer aus Ihrem eigenen Serverbestand verwenden, oder die Konfiguration erfolgt auf einem cloudbasierten virtuellen Computer. In diesem Modul richten wir den Stapel zur Ausführung auf einem virtuellen Ubuntu Linux-Computer ein, der in Azure ausgeführt wird.

In dieser Einheit erstellen Sie einen neuen virtuellen Ubuntu Linux-Computer, der in Azure gehostet wird. Sie könnten Ihre MEAN-Stapelkomponenten auch auf einer vorhandenen VM oder auf einem physischen Hostcomputer installieren. Durch das Erstellen eines neuen virtuellen Computers in dieser Übung können Sie alle Komponenten in einer Azure-Ressourcengruppe zusammenfassen. Dies vereinfacht die Verwaltung und die Bereinigung nach Abschluss der Übung.

Wir verwenden die im Azure-Portal integrierte Cloud Shell-Befehlszeile, um die Linux-VM zu erstellen.

## <a name="provision-an-ubuntu-linux-vm"></a>Bereitstellen eines virtuellen Ubuntu Linux-Computers

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com?azure-portal=true).
1. Öffnen Sie Cloud Shell über das Symbol „>_“ in der Symbolleiste des Azure-Portals.
1. Führen Sie in Cloud Shell den Befehl zum Erstellen einer Azure-Ressourcengruppe aus, was unseren virtuellen Computer einschließt. Ersetzen Sie `<resource-group-name>` durch den Namen Ihrer eigenen Ressourcengruppe und `<resource-group-location>` durch den gewünschten Azure-Standort (z.B. `westus`).


    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    Merken Sie sich den Namen Ihrer Ressourcengruppe, weil wir diesen in weiteren Befehlen verwenden werden.

1. Führen Sie in Cloud Shell den folgenden Befehl aus, um einen neuen virtuellen Ubuntu Linux-Computer zu erstellen. Ersetzen Sie `<resource-group-name>` durch den Namen Ihrer eigenen Ressourcengruppe und `<vm-admin-username>` und `<vm-admin-password>` durch den bevorzugten Administratornamen sowie das zugehörige Kennwort.

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    Notieren Sie sich Ihren Administratornamen und das zugehörige Kennwort, um später eine Verbindung mit diesem virtuellen Computer herstellen zu können.

    Die Ausführung dieses Befehls dauert ungefähr zwei Minuten. Nach Abschluss der Befehlsausführung sieht die resultierende Ausgabe in etwa so aus:

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    Sie sollten sich für die Verbindungsherstellung mit der VM auch die öffentliche IP-Adresse der neu erstellten VM notieren.

1. Versuchen Sie, eine Verbindung mit Ihrer neuen VM herzustellen.

    Öffnen Sie eine Eingabeaufforderung/ein Terminalfenster, und führen Sie den folgenden Befehl aus. Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der VM von oben.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    Bei der ersten Verbindungsherstellung mit dem Computer werden Sie gefragt, ob Sie den Remotecomputer als vertrauenswürdig einstufen. Wenn Sie `yes` eingeben, wird der ECDSA-Fingerabdruck lokal gespeichert, damit nachfolgende Verbindungen als vertrauenswürdig eingestuft werden.

    Wenn alles gut aussieht, geben Sie `exit` ein, um die SSH-Sitzung zu schließen.

1. Öffnen Sie Port 80, um eingehenden HTTP-Datenverkehr an die neue Webanwendung zuzulassen, die Sie erstellen werden.

    Gehen Sie im Azure-Portal zurück zu Cloud Shell. Geben Sie den folgenden Befehl ein, indem Sie Ihren ursprünglichen Ressourcengruppenname für `<resource-group-name>` verwenden.

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    Durch diesen Befehl wird der HTTP-Port auf Ihrem virtuellen Computer geöffnet, der mit dem Namen „MeanDemo“ erstellt wurde.

## <a name="summary"></a>Zusammenfassung

Mit der neu erstellten Ubuntu Linux-VM ist es jetzt möglich, eine Verbindung herzustellen, um die verschiedenen Komponenten des MEAN-Stapels zu installieren.