Als Softwareentwickler in Ihrem Unternehmen haben Sie die Möglichkeit, Ihre Fähigkeiten weiter auszubauen und Teil des internen KI-Teams zu werden. Während Sie sich auf diese spannende neue Rolle vorbereiten, müssen Sie allerdings auch noch Ihre sonstigen Aufgaben erledigen. Angenommen, der hauptverantwortliche AI-Engineer in Ihrem Team hat Ihnen von Jupyter Notebooks erzählt. Diese Anwendung umfasst PyTorch-basierte Aufgaben zum Trainieren eines Bildklassifizierungsmodells. Dies ist zwar eine interessante Anwendung, aber es wird nicht empfohlen, mehrere Frameworks auf einem Computer zu installieren. Stattdessen sollten Sie einen virtuellen Computer erstellen, der auf dem Data Science Virtual Machine-Image (DSVM) basiert. 

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-the-azure-cli"></a>Was ist die Azure CLI?

Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen. Sie steht für macOS, Linux und Windows sowie unter Verwendung von [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) im Browser zur Verfügung. In dem Modul **Kontrollieren von Azure-Diensten mit der CLI** werden die Funktionen des Tools detailliert erläutert.

## <a name="managing-deployments"></a>Verwalten von Bereitstellungen

Die Azure CLI umfasst den `az group deployment`-Befehl zum Verwalten von Azure Resource Manager-Bereitstellungen. Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen. Folgende werden am häufigsten verwendeten:

| Unterbefehl | Beschreibung |
|-------------|-------------|
| `create` | Startet eine Bereitstellung. |
| `list` | Listet alle Bereitstellungen einer Ressourcengruppe auf. |
| `export` | Exportiert die für die Bereitstellung verwendete Vorlage. |

Eine vollständige Liste der verfügbaren Bereitstellungsbefehle finden Sie in der [Referenz zu Azure-Befehlen für Gruppenbereitstellungen](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create).

In diesem Beispiel wird `az group deployment create` zum Bereitstellen des virtuellen Computers verwendet.

## <a name="create-a-json-deployment-parameters-file"></a>Erstellen einer JSON-Datei mit Bereitstellungsparametern

In diesem Beispiel wird die VM mithilfe einer Azure Resource Manager-Vorlage erstellt. Die Vorlage definiert das DSVM-Image für Linux, das bereitgestellt werden soll. Sie müssen für die Vorlage einige Parameter angeben, z.B. die Größe der VM, die verwendet werden soll, den Namen des Administratorbenutzers und das zugehörige Kennwort sowie den Hostnamen. 

1. Führen Sie in Azure Cloud Shell für diese Einheit den folgenden Befehl aus:

    ```bash
    code parameter_file.json
    ```
    <!-- TODO add a link to official doc that explains the built-in editor when it becomes available --> Dieser Befehl öffnet im integrierten Editor eine leere Datei mit dem Namen `parameter_file.json`. 

1. Fügen Sie den folgenden JSON-Ausschnitt in die leere Datei im Code-Editor ein.

    ```json
    { 
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
         "adminUsername": { "value" : "<USERNAME>"},
         "adminPassword": { "value" : "<PASSWORD>"},
         "vmName": { "value" : "<HOSTNAME>"},
         "vmSize": { "value" : "Standard_DS2_v2"},
      }
    }
    ```

1. Aktualisieren Sie die folgenden Parameter in der JSON-Datei, die Sie in den Editor eingefügt haben:

    |Parameter  |Aktueller Wert  |Ihr Wert  |
    |---------|---------|---------|
    |adminUsername     |  `<USERNAME>`       |    Wählen Sie einen Namen für den Administratorbenutzer dieses neuen Computers aus, z.B. *azuser*.     |
    |adminPassword     |  `<PASSWORD>`       |   Wählen Sie ein Kennwort für dieses Administratorbenutzerkonto aus. Weitere Informationen über Kennwortanforderungen finden Sie unter [Häufig gestellte Fragen zu virtuellen Linux-Computern](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true).     |
    |vmName     |   `<HOSTNAME>`      |  Geben Sie einen Namen für den neuen virtuellen Computer ein. Der Name muss mit einem Buchstaben beginnen und darf nur Kleinbuchstaben und Zahlen enthalten. Versuchen Sie, einen eindeutigen Namen zu finden, der z.B. Ihre Initialen und Ihr Geburtsjahr enthält. |
    |vmSize     |  Standard_DS2_v2       |  Die VM-Größe eignet sich gut für diese Übung. Sie können sie aber auch ändern. Eine Liste mit verfügbaren VM-Größen finden Sie unter [Größen für virtuelle Linux-Computer in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true).       |

1. Speichern Sie Ihre Änderungen in `parameter_file.json`, und schließen Sie den Text-Editor.

    > [!IMPORTANT]
    > Merken Sie sich die Werte, die Sie für adminUsername, adminPassword und vmName angegeben haben. Sie werden Sie im Laufe dieser Übung noch einmal brauchen.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe 

> [!IMPORTANT]
> In der Regel können Sie Ressourcengruppen in einer Region Ihrer Wahl erstellen. Sie erhalten allerdings über die aktuelle Sandbox-Sitzung eine Ressourcengruppe, die Sie verwenden können. Die Ressourcengruppe für diese Sitzung lautet **<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>**.

## <a name="deploy-the-dsvm-to-your-resource-group"></a>Bereitstellen der DSVM für Ihre Ressourcengruppe

Sie verfügen jetzt über eine Ressourcengruppe und über definierte Parameter für die DSVM-Vorlage für den Resource Manager in einer Datei mit dem Namen `parameter_file.json`. In diesem Beispiel wird als nächstes `az group deployment create` zum Bereitstellen unseres virtuellen Computers ausgeführt.

1. Führen Sie in Azure Cloud Shell folgenden Befehl aus:

    ```azurecli
    az group deployment create \
    --resource-group  <rgn>[Sandbox resource group name]</rgn> \
    --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json \
    --parameters parameter_file.json
    ```

    Der Befehl verwendet die Resource Manager-Vorlage und unsere Parameter, um den virtuellen Computer in der Ressourcengruppe zu erstellen. 

2. Die Bereitstellung des virtuellen Computers dauert einige Minuten. Die Konsole zeigt beinahe ausschließlich ` - Running ..` an, bis der Vorgang abgeschlossen ist. Wenn der Vorgang abgeschlossen ist, wird eine JSON-Antwortdatei an den Bildschirm ausgegeben. Scrollen Sie in der JSON-Datei nach unten, und prüfen Sie, ob das Feld **provisioningState** den Wert *Erfolgreich* aufweist.

    > [!TIP]
    > Wenn ein Fehler zurückgegeben wird, weil ein DNS-Datensatz bereits von einer weiteren öffentlichen IP verwendet wird, können Sie versuchen, **vmName** in `parameter_file.json` in einen anderen eindeutigen Namen zu ändern.

3. Führen Sie den folgenden Befehl aus, um Informationen zu der VM abzurufen. Dabei wird `<HOSTNAME>` durch den Hostnamen ersetzt, den Sie für Ihre VM definiert haben.

    ```azurecli
    az vm get-instance-view \
    --name <HOSTNAME> \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --query instanceView.statuses[1] \
    --output table
    ```

    Dieser Befehl zeigt den Status der VM an. Dieser sollte *Virtueller Computer wird ausgeführt* lauten.

Herzlichen Glückwunsch! Sie haben jetzt einen virtuellen Linux-Computer erstellt und bereitgestellt, der auf dem DSVM-Image basiert.

## <a name="open-the-vm-to-ssh-traffic-on-port-22"></a>Öffnen der VM für SSH-Datenverkehr auf Port 22

Standardmäßig ist kein Port der VM geöffnet. Ziel ist es, eine Remoteverbindung herzustellen, einen Jupyter Notebook-Server zu starten und andere lokale Befehle auf dem Computer auszuführen. Damit über das Secure Shell-Protokoll (SSH) eine Remoteverbindung mit der VM hergestellt werden kann, muss ein Port geöffnet werden. Der Standardport für SSH lautet 22.  

1. Führen Sie den folgenden Befehl in Azure Cloud Shell aus. Dabei wird `<HOSTNAME>` durch den Namen ersetzt, den Sie Ihrem virtuellen Computer unter DSVM beim Einrichten gegeben haben. 

    ```azurecli
    az vm open-port \
    -g <rgn>[Sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 22 \
    --priority 900
    ```

Die Ausführung dieses Befehls kann einige Minuten dauern. Wenn der letzte Befehl abgeschlossen wird, gibt er eine JSON-Antwort an die Befehlszeile zurück. Prüfen Sie, ob das Feld **provisioningState** den Wert *Erfolgreich* aufweist. Sie werden in Kürze erfahren, wie Sie testen können, ob SSH funktioniert. Zunächst sollten Sie jedoch noch einen weiteren Port öffnen.

## <a name="open-the-vm-to-access-the-jupyter-notebook-server-remotely"></a>Öffnen der VM, um über eine Remoteverbindung auf den Jupyter Notebook-Server zuzugreifen

Wie zuvor bereits erwähnt ist das DSVM-Image bei Software, Tools und Beispielen bereits vorinstalliert. Es soll Sie bei Projekten zu Data Science, Machine Learning und Deep Learning unterstützen. Jupyter ist zusammen mit mehreren Beispielnotebooks im Image installiert. Nun soll erst ein Jupyter Notebook-Server auf der VM gestartet und dann über Ihren lokalen Computer eine Remoteverbindung mit dem Notebook-Server hergestellt werden. Standardmäßig wird der Notebook-Server auf Port 8888 ausgeführt. Wenn Sie über eine Remoteverbindung auf den Server zugreifen möchten, müssen Sie diesen Port auf Ihrem virtuellen Computer öffnen. 

1. Führen Sie den folgenden Befehl in Azure Cloud Shell aus. Dabei wird `<HOSTNAME>` durch den Namen ersetzt, den Sie Ihrem virtuellen Computer unter DSVM beim Einrichten gegeben haben.

    ```azurecli
    az vm open-port \
    -g <rgn>[Sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 8888 \
    --priority 901
    ```

Die Ausführung dieses Befehls kann wieder einige Minuten dauern. Wenn der letzte Befehl abgeschlossen wird, gibt er eine JSON-Antwort an die Befehlszeile zurück. Prüfen Sie, ob das Feld **provisioningState** den Wert *Erfolgreich* aufweist.  

## <a name="connect-to-the-vm-with-secure-shell-ssh"></a>Herstellen einer Verbindung mit dem virtuellen Computer mit Secure Shell (SSH)

1. Führen Sie den folgenden Befehl in Azure Cloud Shell aus, um die öffentliche IP-Adresse der VM zu finden. Ersetzen Sie `<HOSTNAME>` durch den Namen, den Sie Ihrem virtuellen Computer unter DSVM beim Einrichten gegeben haben.

    ```azurecli
    az vm list-ip-addresses \
    -g <rgn>[Sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --output table
    ```

1. Führen Sie in Cloud Shell den folgenden Befehl aus, um sich bei der VM anzumelden. Ersetzen Sie `<USERNAME>` durch den Benutzernamen, den Sie zu Beginn dieser Übung ausgewählt haben. Ersetzen Sie `<IP>` durch den Wert aus der **PublicIPAddresses**-Spalte, den Sie im Schritt zuvor erhalten haben.

    Wenn Sie z.B. den Benutzernamen *azuser* ausgewählt haben und in der Spalte PublicIPAddresses der Wert 33.165.103.23 eingetragen war, würde der Befehl wie folgt aussehen:
    
    `ssh azuser@33.165.103.23`
    
    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 

1. Geben Sie das Kennwort des Administratorbenutzers ein, das Sie zu Beginn dieser Übung ausgewählt haben, wenn Sie dazu aufgefordert werden. Wenn Sie sich erfolgreich angemeldet haben, sollte Ihre Aufforderung in das Format `username@hostname` wechseln, z.B. `azuser@js1982`.

Starten Sie in einem nächsten Schritt den Jupyter Notebook-Server auf Ihrer VM, und öffnen Sie ein Notebook über eine Remoteverbindung.

## <a name="start-the-jupyter-notebook-server-on-the-vm"></a>Starten des Jupyter Notebook-Servers auf der VM

Sie finden im `~/notebooks`-Ordner Ihrer VM eine Reihe von Notebooks. Angenommen, Sie sind noch über eine SSH-Sitzung angemeldet. Starten Sie den Notebook-Server, und öffnen Sie eins dieser Notebooks, um zu prüfen, ob alles einwandfrei funktioniert.


1. Führen Sie über die Eingabeaufforderung Ihrer VM den folgenden Befehl aus:

    ```bash
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root
    ```

> [!CAUTION]
> In dieser Übung wird über `http://` auf den Notebook-Server zugegriffen. Wenn Sie einen Notebook-Server öffentlich ausführen möchten, sollten Sie ihn sichern. Weitere Informationen zum Sichern eines Notebook-Servers finden Sie in der offiziellen Onlinedokumentation zu Jupyter. 

Im folgenden Befehl wird der Jupyter Notebook-Server mit dem Befehl `jupyter notebook` gestartet. Es werden drei wichtige Befehlszeilenargumente bereitgestellt. Bedenken Sie, dass Sie über eine Remoteverbindung mit einer Konsole bei diesem Computer angemeldet sind. Notebooks werden über einen Browser bereitgestellt. 

 - `--ip=0.0.0.0` Standardmäßig werden Notebook-Server lokal über 127.0.0.1:8888 ausgeführt und sind nur über den Localhost verfügbar. Sie können den Notebook-Server lokal mithilfe von http://127.0.0.1:8888 über den Browser ausführen. Wenn die IP-Adresse auf 0.0.0.0 festgelegt ist, überwacht der Server den Datenverkehr auf allen IPs. Wenn der Notebook-Server 0.0.0.0 überwacht, kann über die IP-Adresse des Hostcomputers auf ihn zugegriffen werden.  
 - `--no-browser` Da Sie über einen anderen Computer über das Internet eine Verbindung zu dem Notebook-Server herstellen möchten, wird der Server so konfiguriert, dass er nicht den Browser öffnet. Dies wäre das Standardverhalten. 
 - `--allow-root` In dieser Übung gibt es nur ein Administratorkonto für die VM. Daher kann kein Notebooks als Stamm verwendet werden.

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a>Herstellen einer Verbindung mit dem Jupyter Notebook-Server über einen Remotebrowser

Wenn der obenstehende Befehl auf der VM ausgeführt wird, startet der Notebook-Server, und die Konsole zeigt eine URL an, die Sie in einem Browser verwenden können. 

![Screenshot: Meldung, die ein Notebook-Server, der gerade ausgeführt wird, in der Konsole anzeigt, inklusive der URL, über die über einen Hostcomputer auf den Server zugegriffen werden kann](../media/notebook-url.png)

1. Kopieren Sie die URL, die der Notebook-Server in der Adressleiste des von Ihnen bevorzugten Browsers anzeigt. Sie können auch auf die URL klicken. Dann wird der Server in Ihrem Standardbrowser geöffnet. 

    Sie erhalten dann die Meldung "Site can't be reached" (Website nicht erreichbar.), da die bereitgestellte URL die Verbindung mit dem Notebook-Server über den Hostcomputer darstellt.

1. Damit Sie über eine Remoteverbindung auf den Server zugreifen können, ersetzen Sie den Hostnamen in der URL durch die IP-Adresse der zuvor gespeicherten VM. 

    Nachfolgend sehen Sie eine Beispiel-URL eines Notebook-Servers.

    "http://**ab-dsvm-4**:8888/?token={beliebiges Token}"

    In diesem Fall muss **ab-dsvm-4** durch die IP-Adresse des Computers ersetzt werden. Wenn die IP-Adresse `52.175.199.43` lautet, lautet die URL wie folgt:

    "http://**52.175.199.43**:8888/?token={beliebiges Token}"

    Vergewissern Sie sich, dass `:8888`, die Portadresse, in der URL bleibt.

    > [!TIP]
    > Wenn Sie nicht die IP-Adresse verwenden möchten, können Sie auch den vollqualifizierten Namen des Servers verwenden, der das Format `<HOST NAME>.<REGION>.cloudapp.azure.com` aufweist.

    Auf dem folgenden Screenshot sehen Sie, wie das Jupyter-Dashboard in Ihrem Browser aussieht.

    ![Screenshot des Jupyter Notebook-Dashboards ](../media/jupyter-in-browser.png)

1. Navigieren Sie zu **notebooks/IntroToJupyterPython.ipynb**, und klicken Sie darauf. Testen Sie dieses Notebook, um zu prüfen, ob alles einwandfrei funktioniert.

    Herzlichen Glückwunsch! Sie verfügen jetzt über einen virtuellen Computer, der auf DSVM basiert, und können über eine Remoteverbindung mit Jupyter arbeiten. In dieser Übung wird die Software ausgeführt, die auf der VM installiert wurde. In der nächsten Übung wird die Software in einem Container auf der VM isoliert, sodass Sie ohne Sorge experimentieren können.

4. Wenn Sie das Notebook nicht mehr benötigen, können Sie den Jupyter-Server mit `Control-C` in der Cloud Shell anhalten.
