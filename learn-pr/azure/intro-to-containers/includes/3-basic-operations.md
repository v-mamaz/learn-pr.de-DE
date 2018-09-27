Da Sie jetzt über eine funktionierende Umgebung für die Containerentwicklung verfügen, können wir uns einige häufig verwendete Möglichkeiten zum Ausführen, Auflisten und Löschen von Containern ansehen.

In dieser Einheit lernen Sie Folgendes:

* Ausführen von Standardcontainern
* Herunterladen von Containerimages
* Löschen von Containern und den zugehörigen Images

## <a name="whats-a-container-image"></a>Was ist ein Containerimage?

Ein _Containerimage_ umfasst das Basisbetriebssystem und alle zusätzlichen Prozesse, Anwendungen und Konfigurationen. Ein _Container_ führt ähnlich wie ein virtueller Computer (VM) eine Instanz eines Images aus.

## <a name="connect-to-your-linux-vm"></a>Herstellen einer Verbindung mit der Linux-VM

Wenn Sie die Verbindung zur SSH-Sitzung, die Sie im vorherigen Teil erstellt haben, getrennt haben, müssen Sie sich anmelden. Hier ist eine kleine Erinnerung.

1. Rufen Sie die IP-Adresse ab.

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

## <a name="create-and-run-a-basic-container"></a>Erstellen und Ausführen eines einfachen Containers

Im Folgenden führen Sie einen Container aus, der auf Alpine Linux basiert. Alpine Linux ist aufgrund der Größe beliebt. Containerimages können bis zu 5 MB klein sein.

Führen Sie diesen `docker run`-Befehl aus, um einen Container zu erstellen, der auf Alpine Linux basiert.

```bash
docker run alpine echo "Hello World"
```

Ihnen sollte eine Ausgabe angezeigt werden, die wie folgt aussieht:

```output
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
8e3ba11ec2a2: Pull complete
Digest: sha256:7043076348bf5040220df6ad703798fd8593a0918d06d3ce30c6c93be117e430
Status: Downloaded newer image for alpine:latest
Hello World
```

Mit dem `docker run`-Befehl wird ein Container erstellt, der angegebene Befehl ausgeführt und der Container anschließend gelöscht.

Hier lädt Docker das [alpine](https://hub.docker.com/_/alpine?azure-portal=true)-Image vom Docker Hub herunter, startet den Container und gibt dann „Hello World“ über die Konsole aus.

In diesem Fall wird der Befehl `echo` vorübergehend ausgeführt und dann beendet. Im vorherigen Teil wurde nginx im Vordergrund ausgeführt, wodurch Ihre Container aktiv blieben, bis Sie den Container oder den nginx-Dienst beendet haben.

## <a name="get-container-images"></a>Abrufen von Containerimages

Containerimages werden in einer Containerimageregistrierung gespeichert. Im vorherigen Beispiel hat Docker das **alpine**-Image vom Docker Hub per Pull abgerufen. Docker Hub ist die öffentliche Containerregistrierung von Docker.

Führen Sie den Befehl `docker images` aus, um eine Liste von Images anzuzeigen, die heruntergeladen und auf Ihrem System gespeichert wurden.

```bash
docker images
```

Ihnen werden zwei Images angezeigt: **alpine** und **nginx**.

```output
REPOSITORY          TAG                 IMAGE ID            CREATEDSIZE
alpine              latest              196d12cf6ab1        8 days ago4.41MB
nginx               latest              06144b287844        2 weeks ago109MB
```

Verwenden Sie den Befehl `docker search`, um nach einem Containerimage zu suchen. Beispielsweise können Sie den folgenden Befehl ausführen, um alle Containerimages aufzulisten, die `nginx` im Namen enthalten.

```bash
docker search nginx --limit 5
```

In diesem Beispiel schränkt das Argument `--limit` den Suchvorgang auf die ersten fünf Ergebnisse ein.

Die Ausgabe sollte wie folgt aussehen.

```output
NAME                                     DESCRIPTION         STARS               OFFICIAL            AUTOMATED
nginx                                    Official build of Nginx.         9672                [OK]
jwilder/nginx-proxy                      Automated Nginx reverse proxy for docker con…   1415                                    [OK]
richarvey/nginx-php-fpm                  Container running Nginx + PHP-FPM capable of…   615                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion   LetsEncrypt container to use with nginx as p…   411                                     [OK]
bitnami/nginx                            Bitnami nginx Docker Image         58                                      [OK]
```

Befehle wie `docker run` rufen das Image für Sie ab, wenn es nicht lokal vorhanden ist. Es ist jedoch üblich, ein Image herunterzuladen, bevor Sie es verwenden. Damit wird sichergestellt, dass Sie über die neueste Version verfügen.

Verwenden Sie hierzu den `docker pull`-Befehl. Führen Sie Folgendes aus, um das neueste **nginx**-Image vom Docker Hub zu abzurufen.

```bash
docker pull nginx
```

In diesem Beispiel wird gezeigt, dass Sie über die neuste Version des **nginx**-Images verfügen.

```output
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:24a0c4b4a4c0eb97a1aabb8e29f18e917d05abfe1b7a7c07857230879ce7d3d3
Status: Image is up to date for nginx:latest
```

## <a name="run-and-list-a-container"></a>Ausführen und Auflisten eines Containers

Im vorherigen Teil haben Sie den `docker run`-Befehl verwendet, um nginx aufzurufen. Führen Sie den Befehl ein zweites Mal aus, und sehen Sie sich genauer an, was passiert.

1. Führen Sie diesen Befehl über Ihre SSH-Verbindung aus, um einen Container aufzurufen, der nginx ausführt.

    ```bash
    docker run -d -p 8080:80 nginx
    ```

    * Das `-d`-Argument gibt an, dass der Container im Modus „Getrennt“ ausgeführt wird, d.h., der Container wird im Hintergrund ausgeführt. Wenn der nginx-Prozess beendet wird oder abstürzt, wird auch der Container beendet.
    * Das `-p`-Argument gibt an, dass Netzwerkdatenverkehr, den der Port 8080 des Containerhosts empfängt (in diesem Fall Ihre Linux-VM), an Port 80 des Containers weitergeleitet wird. Sie haben dieses Argument im vorherigen Teil verwendet, um über Ihren Browser auf den Webserver zuzugreifen.
    * Beim `nginx`-Argument handelt es sich um den Namen des Containerimages, das ausgeführt werden soll.

    Eine vollständige Liste der `docker run`-Optionen finden Sie in der [Referenz zu „docker run“](https://docs.docker.com/engine/reference/run?azure-portal=true).

    Der Befehl `docker run` zeigt einen eindeutigen Bezeichner für den Container an. Zum Beispiel:

    ```output
    9d7327e3121200cfe2dccb627544db1442a4e02ed3151f30681db4e538ef9466
    ```

1. Führen Sie den Befehl `docker ps` aus, um die Container aufzulisten, die auf Ihrem System ausgeführt werden.

    ```bash
    docker ps
    ```

    Der soeben gestartete nginx-Container sollte angezeigt werden. Beachten Sie, dass der Container sowohl über eine ID als auch über einen Namen verfügt. Sie können einen dieser Werte zum Verwalten des Containers verwenden. Notieren Sie sich die Container-ID. Sie werden sie später benötigen.

    ```output
    CONTAINER ID        IMAGE               COMMAND                  CREATED     STATUS              PORTS                  NAMES
    9d7327e31212        nginx               "nginx -g 'daemon of…"   4 minutes ago     Up 4 minutes        0.0.0.0:8080->80/tcp   compassionate_allen
    ```

1. Sie können den ausgeführten Webserver wie zuvor mit der IP-Adresse der VM im Browser anzeigen. Vergessen Sie nicht, Port 8080 als Teil der URL anzugeben.

    ![Die Website im Browser](../media/2-nginx-browser.png)

## <a name="delete-containers"></a>Löschen von Containern

Mit dem Befehl `docker rm` können Sie einen Container löschen. Sie können den zu löschenden Container anhand seines Namens oder seiner ID angeben.

1. Versuchen Sie, den Befehl `docker rm` auszuführen, um den Container zu löschen, der nginx ausführt. Führen Sie den Befehl `docker ps` aus, wenn Sie die ID abrufen müssen. Hier sehen Sie ein Beispiel.

    ```bash
    docker rm 9d7327e31212
    ```

    Wie Sie sehen, kann der Container nicht entfernt werden, da er sich im Ausführungszustand befindet.

    ```output
    Error response from daemon: You cannot remove a running container 9d7327e3121200cfe2dccb627544db1442a4e02ed3151f30681db4e538ef9466. Stop the container before attempting removal or force remove
    ```

1. Führen Sie den Befehl `docker stop` aus, um den Container zu beenden. Hier sehen Sie ein Beispiel.

    ```bash
    docker stop 9d7327e31212
    ```
    
1. Führen Sie den Befehl `docker ps` aus, um sicherzustellen, dass der Container nicht mehr ausgeführt wird.

    ```bash
    docker ps
    ```

    Sie sehen Folgendes.

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATEDSTATUS              PORTS               NAMES
    ```

1. Führen Sie den Befehl `docker ps` ein weiteres Mal aus, jedoch geben Sie diesmal das Flag `-a` an. Damit werden alle Container aufgelistet, auch die, die beendet wurden.

    ```bash
    docker ps -a
    ```

    Ihnen sollte eine Ausgabe angezeigt werden, die wie folgt aussieht:

    ```output
    CONTAINER ID        IMAGE               COMMAND                  CREATED     STATUS                          PORTS               NAMES
    9d7327e31212        nginx               "nginx -g 'daemon of…"   11 minutes ago     Exited (0) About a minute ago                       compassionate_allen
    df8aeea0320f        alpine              "echo 'Hello World'"     About an hour ago   Exited (0) About an hour ago                        objective_payne
    3a7efb75c288        nginx               "nginx -g 'daemon of…"   About an hour ago   Exited (0) About an hour ago                        nginx
    ```

    Die Ausgabe enthält den nginx-Container, den Sie soeben beendet haben, sowie die anderen Container, die Sie vorher ausgeführt haben.

1. Führen Sie `docker rm` ein weiteres Mal aus. Ersetzen Sie die angezeigte ID durch eine Ihrer IDs.

    ```bash
    docker rm 9d7327e31212
    ```

1. Führen Sie den folgenden `docker rm`-Befehl aus, um _alle_ aktiven Container zu löschen.

    ```bash
    docker rm $(docker ps -aq)
    ```

1. Führen Sie `docker ps -a` erneut aus. Dann wird angezeigt, dass keine aktiven Container ausgeführt oder beendet werden.

    ```bash
    docker ps -a
    ```

## <a name="delete-a-container-image"></a>Löschen eines Containerimages

Mit dem Befehl `docker rmi` können Sie ein Containerimage löschen.

Sie können ein Image nur löschen, wenn kein Container, der über dieses Image gestartet wurde, aktiv ist, unabhängig davon, ob er ausgeführt oder beendet wird. Allerdings erzwingt das `-f`-Argument die Entfernung aller zugehörigen Container und entfernt anschließend das Containerimage.

1. Führen Sie den Befehl `docker rmi nginx` aus, um das nginx-Image aus Ihrer Linux-VM zu entfernen.

    ```bash
    docker rmi nginx
    ```

    Die angezeigte Ausgabe sollte wie folgt aussehen:

    ```output
    Untagged: nginx:latest
    Untagged: nginx@sha256:24a0c4b4a4c0eb97a1aabb8e29f18e917d05abfe1b7a7c07857230879ce7d3d3
    Deleted: sha256:06144b2878448774e55577ae7d66b5f43a87c2e44322b3884e4e6c70d070b262
    Deleted: sha256:824a442ee3c96744d75be3737a22cc6a47aebad1b30be67f3c2f8f29cb0aa879
    Deleted: sha256:8e3d1e9e4945f930c93c30617512998437f6edafd86676770d29b1581f2520bb
    Deleted: sha256:8b15606a9e3e430cb7ba739fde2fbb3734a19f8a59a825ffa877f9be49059817
    ```

1. Führen Sie den Befehl `docker images` aus, um die Images auf der VM aufzulisten. 

    ```bash
    docker images
    ```

    Das **alpine**-Image wird angezeigt.

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATEDSIZE
    alpine              latest              196d12cf6ab1        8 days ago4.41MB
    ```

1. Führen Sie den folgenden `docker rmi`-Befehl aus, um _alle_ Images von der VM zu löschen.

    ```bash
    docker rmi $(docker images -q)
    ```

1. Führen Sie den Befehl `docker images` erneut aus, und Sie werden sehen, dass keine Images auf der VM vorhanden sind.

    ```bash
    docker images
    ```
