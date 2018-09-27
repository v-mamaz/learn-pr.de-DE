Bevor einige der grundlegenden Methoden zum Ausführen, Auflisten und Löschen von Containern erläutert werden, sehen Sie sich eine einfache nginx-Konfiguration an, die auf einem Docker-Container ausgeführt wird, der auf einem virtuellen Ubuntu-Computer (VM) gehostet wird.

In dieser Einheit lernen Sie Folgendes:

1. Erstellen einer Linux-VM, die zum Installieren von Docker beim ersten Start der VM konfiguriert ist.
1. Herstellen einer Verbindung zur VM und Starten eines Docker-Containers, auf dem nginx ausgeführt wird.
1. Verwenden der Portbindung, um den Webserver außerhalb der VM zur Verfügung zu stellen.

## <a name="what-are-containers"></a>Was sind Container?

Ein Container ist eine Virtualisierungsumgebung, die im Gegensatz zu einer VM nicht immer ein vollständiges Betriebssystem enthält. Stattdessen verweist sie auf das Betriebssystem der Hostumgebung, die den Container ausführt. Wenn Sie beispielsweise fünf Container auf einem Server mit einem spezifischen Linux-Kernel ausführen, werden alle fünf Container auf demselben Kernel ausgeführt.

Mit Containern können Sie Ihre Anwendung und alle zur Ausführung erforderlichen Elemente in ein sogenanntes _Containerimage_ packen. Container sind isoliert, d.h., sie beeinflussen keine anderen Container auf dem gleichen System. Containerimages sind außerdem portierbar. Sie können Ihre Images in eine Containerregistrierung hochladen, z.B. Docker Hub oder Azure Container Registry. Anschließend können Sie Ihre Container in der Cloud ausführen und davon ausgehen, dass sie sich auf die gleiche Weise wie in Ihrer Entwicklungsumgebung verhalten.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

Container ermöglichen schnelle Iterationen. Da Container kein Betriebssystem enthalten müssen, sind sie in der Regel deutlich kleiner als vollständige VMs. Dadurch können Sie Container schnell starten und beenden, oft innerhalb von Sekunden.

## <a name="understand-the-setup"></a>Grundlegende Informationen zum Aufbau

Ihnen wird eine Sandboxumgebung zu Lernzwecken bereitgestellt. Diese Umgebung enthält Azure Cloud Shell, ein browserbasierter Dienst zum Verwalten und Entwickeln von Azure-Ressourcen über die Befehlszeile.

Über Cloud Shell erstellen Sie eine Linux-VM, die Docker enthält. Sie verbinden Ihre Linux-VM per SSH, sodass Sie Docker-Container interaktiv erstellen und verwenden können.

Stellen Sie sich diese Linux-VM als Ihre Entwicklungsumgebung zum Kennenlernen von Containern vor. In der Praxis würden Sie Docker auf dem Computer installieren, den Sie zum Entwickeln Ihrer Apps verwenden. Docker kann unter Windows, macOS und Linux ausgeführt werden.

Am Ende dieses Moduls werden Ihnen Ressourcen bereitgestellt, mit denen Sie mehr über das Ausführen von Docker in Ihrer lokalen Entwicklungsumgebung erfahren können.

## <a name="what-is-nginx"></a>Was ist nginx?

nginx (ausgesprochen „Engine-x“) ist ein beliebter, kostenloser Open-Source-Webserver, der unter Unix, Linux, macOS und Windows ausgeführt werden kann. Das Konfigurieren eines Webservers stellt eine gute Möglichkeit dar, Container in Aktion zu sehen. Hier verwenden Sie nginx, um eine einfache Webseite bereitzustellen.

## <a name="what-is-cloud-init"></a>Was ist cloud-init?

Mit cloud-init können Sie eine Linux-VM während des ersten Starts anpassen. Sie können mit cloud-init Pakete installieren und Dateien schreiben oder Benutzer und Sicherheit konfigurieren. Hier verwenden Sie ein cloud-init-Skript, um Docker auf Ihrer VM zu installieren.

## <a name="what-is-port-binding"></a>Was ist Portbindung?

Mit Portbindung können Sie Netzwerkdatenverkehr vom Host an einen Container weiterleiten.

Ein Docker-Container wird auf einem lokalen Netzwerk des Hostsystems des Containers ausgeführt. In diesem Fall befindet sich das Netzwerk des Containers auf Ihrer Linux-VM.

Wie Sie bereits wissen, werden Webanforderungen in der Regel über Port 80 (HTTP) ausgeführt. Da der Container auf einem lokalen Netzwerk in der VM ausgeführt wird, ist der Container für die Außenwelt nicht zugänglich.

Mit Docker können Sie einen Port außerhalb der VM veröffentlichen oder zur Verfügung stellen. Hier konfigurieren Sie Ihren Container so, dass der Netzwerkdatenverkehr an Port 8080 Ihrer VM an Port 80 Ihres Containers weitergeleitet wird.

## <a name="create-a-virtual-machine-to-host-docker"></a>Erstellen eines virtuellen Computers zum Hosten von Docker

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="create-the-cloud-init-script"></a>Erstellen des cloud-init-Skripts

1. Navigieren Sie zum Ordner **clouddrive**.

    ```azurecli
    cd clouddrive
    ```

1. Erstellen Sie einen neuen Ordner mit dem Namen **vm-config**.

    ```azurecli
    mkdir vm-config
    ```

1. Navigieren Sie zum neuen Ordner.

    ```azurecli
    cd vm-config
    ```

1. Erstellen Sie eine neue Datei mit dem in Cloud Shell integrierten Editor.

    ```azurecli
    code .
    ```

1. Fügen Sie das cloud-init-Skript in den Editor ein.

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```yaml
    #cloud-config
    package_upgrade: true
    write_files:
      - path: /etc/systemd/system/docker.service.d/docker.conf
        content: |
          [Service]
          ExecStart=
          ExecStart=/usr/bin/dockerd
      - path: /etc/docker/daemon.json
        content: |
          {
            "hosts": ["fd://","tcp://127.0.0.1:2375"]
          }
    runcmd:
      - curl -sSL https://get.docker.com/ | sh
      - usermod -aG docker azureuser
    ```

1. Speichern Sie die Datei als **docker-vm-config.txt** (drücken Sie hierzu <kbd>STRG+S</kbd>, oder klicken Sie mit der rechten Maustaste, und wählen Sie dann **Speichern** aus).

1. Schließen Sie den Editor (drücken Sie hierzu <kbd>STRG+Q</kbd>, oder klicken Sie mit der rechten Maustaste, und wählen Sie **Beenden** aus).

### <a name="create-the-vm"></a>Erstellen des virtuellen Computers

> [!IMPORTANT]
> Normalerweise würden Sie mit dem Befehl `az group create` eine Ressourcengruppe für alle Ihre verwandten Azure-Ressourcen erstellen. Für diese Übungen wurde aber bereits eine Ressourcengruppe für Sie erstellt. Verwenden Sie in allen Schritten die Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.

1. Führen Sie den folgenden `az vm create`-Befehl aus, um die Linux-VM zu erstellen.

    ```azurecli
    az vm create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --image UbuntuLTS \
      --admin-username azureuser \
      --generate-ssh-keys \
      --custom-data docker-vm-config.txt
    ```

Das Argument `--custom-data` gibt das cloud-init-Skript an, das Docker beim ersten Start der VM installiert. Dieser Prozess dauert ein paar Minuten.

## <a name="connect-to-the-vm"></a>Herstellen der Verbindung mit der VM

Hier erstellen Sie eine SSH-Verbindung mit der VM, damit Sie sie konfigurieren können.

1. Führen Sie den folgenden `az vm show`-Befehl aus, um die IP-Adresse Ihrer VM abzurufen.

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

1. Stellen Sie eine SSH-Verbindung zur VM her. Ersetzen Sie **ip-adress** durch Ihre IP-Adresse.

    ```bash
    ssh azureuser@ip-address
    ```

1. Überprüfen Sie die Version von Docker.

    ```bash
    docker version
    ```

    > [!NOTE]
    > Wenn der Befehl fehlschlägt, oder eine Fehlermeldung zum Herstellen einer Verbindung mit dem Docker-Daemonsocket angezeigt wird, bedeutet das, dass das cloud-init-Skript noch nicht abgeschlossen wurde. Obwohl es Möglichkeiten gibt, auf den Abschluss des Skripts zu warten, führen Sie fürs Erste `exit` aus, um Ihre SSH-Sitzung zu verlassen und die Verbindung in ein paar Minuten wiederherzustellen.

## <a name="start-nginx"></a>Starten von nginx

Hier starten Sie einen Docker-Container, auf dem nginx ausgeführt wird.

1. Führen Sie den folgenden `docker run`-Befehl aus, um einen Docker-Container zu starten, auf dem nginx ausgeführt wird.

    ```bash
    docker run -d -p 8080:80 --name nginx nginx
    ```

    Durch diesen Befehl wird ein Docker-Image heruntergeladen, das vom [Docker Hub](https://hub.docker.com/_/nginx?azure-portal=true) mit nginx vorkonfiguriert ist.

    Das Argument `--name` weist dem Docker-Container den Namen „nginx“ zu, damit Sie ihn später verwenden können.

    Das Argument `-p` leitet Netzwerkdatenverkehr an Port 8080 Ihrer VM an Port 80 Ihres Containers weiter.

1. Führen Sie den Befehl `curl` aus, um zu überprüfen, ob nginx ausgeführt wird und zugänglich ist.

    ```bash
    curl http://localhost:8080
    ```

1. Beenden Sie Ihre SSH-Sitzung.

    ```bash
    exit
    ```

## <a name="access-your-web-server-from-a-web-browser"></a>Zugriff auf Ihren Webserver über einen Webbrowser

Denken Sie daran, dass Sie Ihren Container so konfiguriert haben, dass der Netzwerkdatenverkehr an Port 8080 an Port 80 Ihres Containers weitergeleitet wird.

Im Folgenden öffnen Sie Port 8080 Ihrer VM über Azure Firewall, um die Portzuordnung in Aktion zu sehen. Anschließend greifen Sie über einen Browser auf Ihren Webserver zu.

1. Führen Sie den folgenden `az vm open-port`-Befehl aus, um Port 8080 durch die Firewall Ihrer VM zu öffnen.

    ```azurecli
    az vm open-port \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --port 8080 \
      --priority 1001
    ```

1. Navigieren Sie in einem Webbrowser zur IP-Adresse der VM. Stellen Sie sicher, dass Sie Port 8080 in die Adresse einfügen, z.B. **http://40.121.106.164:8080**.

    Die Standardstartseite wird angezeigt.

    ![Die Website im Browser](../media/2-nginx-browser.png)

## <a name="stop-the-container"></a>Beenden des Containers

Nun beenden Sie den Container.

1. Melden Sie sich zunächst wieder bei Ihrer VM an. Hier ist eine kleine Erinnerung.

    Rufen Sie die IP-Adresse ab.

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

    Stellen Sie eine SSH-Verbindung zur VM her. Ersetzen Sie **ip-adress** durch Ihre IP-Adresse.

    ```bash
    ssh azureuser@ip-address
    ```

1. Führen Sie den Befehl `docker stop nginx` aus, um den Container namens „nginx“ zu beenden.

    ```bash
    docker stop nginx
    ```

Lassen Sie die SSH-Verbindung für die nächste Einheit geöffnet.

Herzlichen Glückwunsch! Sie haben erfolgreich einen virtuellen Computer erstellt und diesen zum Hosten eines nginx-Webservers in einem Container verwendet.
