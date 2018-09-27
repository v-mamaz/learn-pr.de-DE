Wir verfügen über einen Lastenausgleich, mit dem wir eingehenden Internetdatenverkehr weiterleiten. Nun benötigen wir einige Azure-VMs, zu denen der Datenverkehr geleitet werden soll. In diesem Beispiel wird Linux verwendet, allerdings funktioniert die exakt gleiche Vorgehensweise mit jedem beliebigen VM-Image.

## <a name="create-a-set-of-vms"></a>Erstellen einer Gruppe von virtuellen Computern

Im Folgenden erstellen Sie drei virtuelle Computer (VMs) und gruppieren diese über die Azure CLI in einer Verfügbarkeitsgruppe. Für diese Aufgabe hätte auch das Portal verwendet werden können, jedoch ist dieser Vorgang mit einem Tool zur Skripterstellung viel einfacher, da mehrere Ressourcen erstellt werden.

Wenn Sie die Verwendung des Azure-Portals _wirklich_ bevorzugen, können Sie alternativ eine _Vorlage_ verwenden. Dabei handelt es sich um JSON-Anweisungen, die zum Bereitstellen von Ressourcen verwendet werden können. Sie können eine Vorlage für die VM definieren und die Vorlage anschließend mehrmals im Azure-Portal bereitstellen.

### <a name="create-some-azure-cli-defaults"></a>Erstellen von Standardbefehlen für die Azure CLI

1. Legen Sie zunächst Standardbefehle in der Azure CLI fest. Für jeden Befehl ist eine _Ressourcengruppe_ und optional ein _Standort_ erforderlich. Anstatt diese jedes Mal einzugeben, können Sie Standardparameter festlegen. Verwenden Sie die vorab erstellte Azure-Sandboxressourcengruppe und den gleichen Standort, den Sie für Azure Load Balancer ausgewählt haben. Zur Erinnerung werden hier die verfügbaren Standorte aufgeführt:

    [!include[](../../../includes/azure-sandbox-regions-note.md)]

1. Geben Sie diesen Befehl rechts in Cloud Shell ein, und ersetzen Sie den Platzhalter `<location>` durch den Standort, den Sie für Azure Load Balancer verwendet haben.

    ```azurecli
    az configure --defaults group=<rgn>[sandbox Resource Group</rgn> location=<location>
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

### <a name="create-an-availability-set"></a>Erstellen einer Verfügbarkeitsgruppe

Beginnen Sie zunächst mit dem Erstellen einer _Verfügbarkeitsgruppe_.

Eine Verfügbarkeitsgruppe muss festgelegt sein, damit die VMs in ihr gruppiert werden können. Mit dem Befehl `vm availability-set` können Sie sie erstellen. Sie benötigt lediglich einen Namen. Für diese Vorgehensweise wird **woodgrove-avail-set** verwendet.

```azurecli
az vm availability-set create --name woodgrove-avail-set
```

### <a name="create-a-configuration-script"></a>Erstellen eines Konfigurationsskripts

Für alle VMs soll die gleiche grundlegende Konfiguration verwendet werden.

    - Ubuntu Linux
    - nginx-Webserver
    - Node.js
    - Allgemeine Website mit einer einzigen Seite für Testzwecke

Die Auswahl des Betriebssystem basiert auf dem ausgewählten Image, für andere Konfigurationselemente ist jedoch ein gewisses Maß an Skripterstellung erforderlich. Erstellen Sie eine lokale Datei in Cloud Shell, um einen Webserver zu installieren, und konfigurieren Sie diesen mit einer allgemeinen Website.

1. Öffnen Sie den Cloud Shell-Editor, indem Sie `code` im Terminal eingeben.

    ```bash
    code
    ```

    Dies ist ein integrierter Editor, den Sie zum Erstellen und Bearbeiten von Dateien direkt in der Cloud Shell-Umgebung verwenden können. Die Dateien werden in einem Speicherkonto in Azure gespeichert, das erstellt wurde, als Sie die Cloud Shell-Umgebung gestartet haben.

1. Kopieren Sie das folgende Skript, und fügen Sie es in das Editorfenster ein.

    ```script
    #cloud-config
    package_upgrade: true
    packages:
      - nginx
      - nodejs
      - npm
    write_files:
      - owner: www-data:www-data
      - path: /etc/nginx/sites-available/default
        content: |
          server {
            listen 80;
            location / {
              proxy_pass http://localhost:3000;
              proxy_http_version 1.1;
              proxy_set_header Upgrade $http_upgrade;
              proxy_set_header Connection keep-alive;
              proxy_set_header Host $host;
              proxy_cache_bypass $http_upgrade;
            }
          }
      - owner: azureuser:azureuser
      - path: /home/azureuser/myapp/index.js
        content: |
          var express = require('express')
          var app = express()
          var os = require('os');
          app.get('/', function (req, res) {
            res.send('Hello World from host ' + os.hostname() + '!')
          })
          app.listen(3000, function () {
            console.log('Hello world app listening on port 3000!')
          })
    runcmd:
      - service nginx restart
      - cd "/home/azureuser/myapp"
      - npm init
      - npm install express -y
      - nodejs index.js
    ```

1. Speichern Sie die Datei, und nennen Sie sie **cloud-init.txt**. Hierzu können Sie das Kontextmenü „...“ in der oberen rechten Ecke des Editors, <kbd>STRG+S</kbd> unter Windows und Linux oder <kbd>CMD+S</kbd> unter macOS verwenden.

1. Beenden Sie den Editor. Hierzu können Sie erneut das Kontextmenü „...“ oder eine Tastenkombination (<kbd>STRG+Q</kbd>) verwenden.

1. Die Datei sollte sich im Dateisystem befinden. Versuchen Sie, den Befehl `ls` zum Auflisten der Ordnerinhalte zu verwenden. Sie können auch `cat` für die Datei verwenden, um die Inhalte zu überprüfen.

### <a name="create-the-virtual-machines"></a>Erstellen der virtuellen Computer

Als Nächstes erstellen Sie drei Ubuntu Linux-VMs mithilfe der Azure CLI. Die Optionen werden hier nicht erläutert. Sollten Sie jedoch daran interessiert sein, mehr über die Verwaltung von VMs mit der CLI zu lernen, finden Sie weitere Informationen im Modul **Verwalten von virtuellen Computern mit der Azure CLI**.

Außerdem müssen Sie eine virtuelle Netzwerkschnittstelle für jede VM erstellen. Sie können eine Schleife nutzen, um sie zusammen zu erstellen.

1. Verwenden Sie den Befehl `vm-create`, um drei VMs in einer Schleife zu erstellen. Sie können den folgenden Code für Folgendes verwenden:
    - Erstellen Sie eine NIC namens _woodgrove_NicX_, wobei X für [1,2,3] steht.
    - Erstellen Sie eine VM namens _woodgrove-VMX_, wobei X für [1,2,3] steht.
    - Ordnen Sie jede NIC dem erstellten virtuellen Netzwerk zu.
    - Ordnen Sie jede VM der NIC und der Verfügbarkeitsgruppe zu.

    ```azurecli
    for i in `seq 1 3`; do

        az network nic create --name woodgrove-Nic$i \
            --vnet-name woodgrove-VNET \
            --subnet backendSubnet

        az vm create --name woodgrove-VM$i \
            --availability-set woodgrove-avail-set \
            --nics woodgrove-Nic$i \
            --image UbuntuLTS \
            --admin-username azureuser \
            --generate-ssh-keys \
            --custom-data cloud-init.txt \
            --no-wait
    done
    ```
    > [!TIP]
    > Hier legt der Befehl den Namen des Administrators auf „azureuser“ fest, dies können Sie beliebig ändern. Außerdem können Sie ein Kennwort angeben, wenn Sie Benutzernamen mit Kennwort SSH-Schlüsseln vorziehen.

1. Die Ausführung dauert eine Weile, und nach Abschluss der Schleife werden die VMs noch nicht verfügbar sein. Sie können zum Azure-Portal wechseln und auf **Alle Ressourcen** klicken, um die erstellten Ressourcen anzuzeigen.

1. Sie können auf den Befehl `vm list` verwenden, um anzuzeigen, wie viele VMs bereitgestellt wurden.

    ```azurecli
    az vm list -o table
    ```

Als Nächstes wird das Konfigurieren des Lastenausgleichs erläutert.