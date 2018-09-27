Für den MEAN-Komponentenstapel wird ein Server benötigt. Sie können entweder einen Linux-Computer oder einen virtuellen Computer aus Ihrem eigenen Serverbestand verwenden, oder die Konfiguration erfolgt auf einem cloudbasierten virtuellen Computer. In diesem Modul richten wir den Stapel zur Ausführung auf einem virtuellen Ubuntu Linux-Computer ein, der in Azure ausgeführt wird.

In dieser Einheit erstellen Sie einen neuen virtuellen Ubuntu Linux-Computer, der in Azure gehostet wird. Sie könnten Ihre MEAN-Stapelkomponenten auch auf einer vorhandenen VM oder auf einem physischen Hostcomputer installieren. Durch das Erstellen eines neuen virtuellen Computers in dieser Übung können Sie alle Komponenten in einer Azure-Ressourcengruppe zusammenfassen. Dies vereinfacht die Verwaltung und die Bereinigung nach Abschluss der Übung.

## <a name="provision-an-ubuntu-linux-vm"></a>Bereitstellen eines virtuellen Ubuntu Linux-Computers

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="creating-a-resource-group"></a>Erstellen einer Ressourcengruppe

Wenn Sie neue Ressourcen erstellen, erstellen Sie in der Regel zuerst eine _Ressourcengruppe_, um alle Ressourcen zu besitzen. Dieser Schritt ist in der Azure-Sandbox überflüssig, aber wenn Sie in Ihrem eigenen Abonnement arbeiten, erstellen Sie mit dem folgenden Befehl eine Ressourcengruppe an einem Standort in Ihrer Nähe.

```azurecli
az group create --name <resource-group-name> --location <resource-group-location>
```

> [!IMPORTANT]
> In der Azure-Sandbox müssen Sie keine Ressourcengruppe erstellen. Verwenden Sie stattdessen die vorab erstellte Ressourcengruppe mit dem Namen **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.

1. Führen Sie in der Cloud Shell rechts den folgenden Befehl aus, um eine neue Ubuntu Linux-VM zu erstellen. Ersetzen Sie `<vm-admin-username>` und `<vm-admin-password>` durch Ihren bevorzugten Administratornamen sowie das zugehörige Kennwort.

    ```azurecli
    az vm create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
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
        "location": "<resource group location>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<rgn>[sandbox resource group name]</rgn>",
        "zones": ""
    }
    ```

    Sie sollten sich für die Verbindungsherstellung mit der VM auch die öffentliche IP-Adresse der neu erstellten VM notieren.

1. Versuchen Sie, eine Verbindung mit Ihrer neuen VM herzustellen.

    Führen Sie in der Cloud Shell den folgenden Befehl aus. Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der zuvor erwähnten VM.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    Bei der ersten Verbindungsherstellung mit dem Computer werden Sie gefragt, ob Sie den Remotecomputer als vertrauenswürdig einstufen. Wenn Sie `yes` eingeben, wird der ECDSA-Fingerabdruck lokal gespeichert, damit nachfolgende Verbindungen als vertrauenswürdig eingestuft werden. Sie werden dann zur Eingabe Ihres Kennworts aufgefordert. Diese Eingabeaufforderung wird jedes Mal angezeigt, wenn Sie eine Verbindung herstellen.

    Wenn alles gut aussieht, geben Sie `exit` ein, um die SSH-Sitzung zu schließen.

1. Öffnen Sie Port 80 auf der VM, um bei der neuen Webanwendung, die Sie erstellen werden, eingehenden HTTP-Datenverkehr zuzulassen.

    ```azurecli
    az vm open-port --port 80 --resource-group <rgn>[sandbox resource group name]</rgn> --name MeanDemo
    ```

    Durch diesen Befehl wird der HTTP-Port auf Ihrem virtuellen Computer geöffnet, der mit dem Namen „MeanDemo“ erstellt wurde.

## <a name="summary"></a>Zusammenfassung

Mit der neu erstellten Ubuntu Linux-VM ist es jetzt möglich, eine Verbindung herzustellen, um die verschiedenen Komponenten des MEAN-Stapels zu installieren.