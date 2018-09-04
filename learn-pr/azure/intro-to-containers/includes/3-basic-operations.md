Sie verfügen jetzt über eine funktionsfähige Umgebung für die Entwicklung von Containern und können sich nachfolgend über einige grundlegende Containervorgänge informieren. Diese Einheit umfasst nicht einmal ansatzweise alle verfügbaren Docker-Funktionen. Allerdings erfahren Sie, wie Sie Container ausführen, auflisten und löschen können. Im Laufe dieses Moduls erhalten Sie zusätzliche Informationen zu Containervorgängen.

## <a name="run-a-basic-container"></a>Ausführen eines Standardcontainers

Bevor Sie mehr zu den Einzelheiten zum Ausführen und Verwalten von Containern erfahren, erhalten Sie zunächst grundlegende Informationen zum Ausführen eines Containers.

Erstellen Sie Ihren ersten Container über den folgenden Befehl.

```bash
docker run alpine echo "Hello World"
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```bash
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
8e3ba11ec2a2: Pull complete
Digest: sha256:7043076348bf5040220df6ad703798fd8593a0918d06d3ce30c6c93be117e430
Status: Downloaded newer image for alpine:latest
Hello World
```

Der Befehl `docker run` erstellt eine Instanz eines Containers. In diesem Fall wurde der Container aus einem Containerimage mit dem Namen `alpine` erstellt. Dieses wurde heruntergeladen und in Ihrem lokalen System gespeichert. Nachdem der Container gestartet wurde, wurde der Befehl `echo "Hello World"` innerhalb des Containers ausgeführt und die Ausgabe an Ihr Terminal übergeben.

Noch müssen Sie sich keine Gedanken zu den technischen Details der einzelnen Aktionen machen. Diese werden im Laufe dieses Moduls näher erläutert.

## <a name="get-container-images"></a>Aufrufen von Containerimages

Container werden wie im Beispiel „Hallo Welt“ dargestellt über ein Containerimage ausgeführt. Dieses Image umfasst das containerbasierte Betriebssystem und jegliche zusätzlichen Prozesse, Anwendungen und Konfigurationen. Containerimages werden in einer Containerimageregistrierung gespeichert. In dem Beispiel „Hallo Welt“ wurde das Image *Alpine* aus Docker Hub entnommen. Es handelt sich dabei um eine öffentliche Containerregistrierung.

Nachfolgend wird erläutert, wie Sie ein zuvor erstelltes Containerimage suchen und herunterladen können.

Führen Sie den folgenden Befehl aus, um eine Liste mit Images abzurufen, die heruntergeladen und in Ihrem System gespeichert wurden.

```bash
docker images
```

Wenn Sie alle Schritte wie beschrieben ausgeführt haben, sollte das Image „Alpin“ angezeigt werden. Dieses Image wurde heruntergeladen, als das Beispiel „Hallo Welt“ ausgeführt wurde.

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

Verwenden Sie den Befehl `docker search`, um nach einem Containerimage zu suchen. Sie können das folgende Beispiel verwenden, um alle Containerimages aufzulisten, deren Namen `nginx` enthält.

```bash
docker search nginx
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```bash
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                                                  Official build of Nginx.                        9071                [OK]
jwilder/nginx-proxy                                    Automated Nginx reverse proxy for docker con…   1365                                    [OK]
richarvey/nginx-php-fpm                                Container running Nginx + PHP-FPM capable of…   593                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion                 LetsEncrypt container to use with nginx as p…   390                                     [OK]
kong                                                   Open-source Microservice & API Management la…   207                 [OK]
webdevops/php-nginx                                    Nginx with PHP-FPM                              106                                     [OK]
kitematic/hello-world-nginx                            A light-weight nginx container that demonstr…   102
zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server wi…   60                                      [OK]
bitnami/nginx                                          Bitnami nginx Docker Image                      54                                      [OK]
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          38                                      [OK]
linuxserver/nginx                                      An Nginx container, brought to you by LinuxS…   37
tobi312/rpi-nginx                                      NGINX on Raspberry Pi / armhf                   20                                      [OK]
nginxdemos/nginx-ingress                               NGINX Ingress Controller for Kubernetes . Th…   11
blacklabelops/nginx                                    Dockerized Nginx Reverse Proxy Server.          10                                      [OK]
wodby/drupal-nginx                                     Nginx for Drupal container image                9                                       [OK]
webdevops/nginx                                        Nginx container                                 8                                       [OK]
nginxdemos/hello                                       NGINX webserver that serves a simple page co…   7                                       [OK]
centos/nginx-18-centos7                                Platform for running nginx 1.8 or building n…   6
1science/nginx                                         Nginx Docker images that include Consul Temp…   4                                       [OK]
centos/nginx-112-centos7                               Platform for running nginx 1.12 or building …   3
pebbletech/nginx-proxy                                 nginx-proxy sets up a container running ngin…   2                                       [OK]
travix/nginx                                           NGinx reverse proxy                             1                                       [OK]
toccoag/openshift-nginx                                Nginx reverse proxy for Nice running on same…   1                                       [OK]
ansibleplaybookbundle/nginx-apb                        An APB to deploy NGINX                          0                                       [OK]
mailu/nginx                                            Mailu nginx frontend                            0                                       [OK]
```

Wenn Sie ein Image erst herunterladen möchten, bevor Sie es ausführen, verwenden Sie den Befehl `docker pull`. Das folgende Beispiel pullt das *NGINX*-Image in Ihr System.

```bash
docker pull nginx
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```bash
Using default tag: latest
latest: Pulling from library/nginx
be8881be8156: Pull complete
f2f27ed9664f: Extracting [===============>                                   ]  6.652MB/22.14MB
54ff137eb1b2: Download complete
```

Führen Sie `docker images` erneut aus, um alle Images in Ihrem System aufzulisten. Dann sollten Sie sehen, dass das *NGINX*-Image zu Ihrem System hinzugefügt wurde.

```bash
docker images
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              c82521676580        26 hours ago        109MB
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

## <a name="run-containers"></a>Ausführen von Containern

Da Sie jetzt das *NGINX*-Image ermittelt und heruntergeladen haben, können Sie jetzt darüber einen Container ausführen. Wenn Sie die Docker-CLI verwenden, um ein Containerimage auszuführen, greifen Sie auf den Befehl `docker run` zurück.

Im folgenden Beispiel gibt das Argument `-d` an, dass der Container im Modus „Getrennt“ ausgeführt wird. In dieser Konfiguration führt der Container einen festgelegten Prozess aus. Wenn dieser Prozess anhält oder abstürzt, wird auch der Container angehalten. Das `-p 8080:80`-Argument gibt an, dass Netzwerkdatenverkehr, den der Port 8080 auf dem Containerhost empfängt (in diesem fall Ihr Entwicklungssystem), an Port 80 auf dem Container weitergeleitet wird. Bei Argument `ngingx` handelt es sich um den Namen, des Containerimages, das ausgeführt werden soll.

Eine vollständige Liste mit `docker run`-Argumenten finden Sie in der [Referenz zur Ausführung von Docker](https://docs.docker.com/engine/reference/run/).

```bash
docker run -d -p 8080:80 nginx
```

Dieser Vorgang gibt die vollständige Container-ID zurück.

```bash
bd2424bfe7a5423d7d65efdf0b1622770d59e212db7b82862c3129fb630b5721
```

Listen Sie die Container, die auf Ihrem System ausgeführt werden, mithilfe des Befehls `docker ps` auf.

```bash
docker ps
```

Es sollte ein einzelner Container angezeigt werden, der ausgeführt wird. Dabei handelt es sich um den NGINX-Container, der im letzten Schritt ausgeführt wurde. Beachten Sie, dass der Container sowohl über eine ID als auch über einen Namen verfügt. Beide Werte können verwendet werden, um den Container zu verwalten. Notieren Sie sich die Container-ID. Dieser Wert wird in der nächsten Einheit verwendet.

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
bd2424bfe7a5        nginx               "nginx -g 'daemon of…"   37 minutes ago      Up 37 minutes       0.0.0.0:8080->80/tcp   gallant_engelbart
```

Öffnen Sie einen Internetbrowser, und geben Sie die Adresse http://localhost:8080 ein, um den Container zu testen. Anschließend sollte die Standardwebsite von NGINX angezeigt werden.

![Microsoft Edge mit dem Begrüßungsbildschirm von NGINX](../media-draft/3-nginx.png)

## <a name="delete-containers"></a>Löschen von Containern

Wenn Sie einen Container nicht mehr verwenden möchten, können Sie diesen löschen, indem Sie den Namen oder die ID des Containers zum Befehl `docker rm` hinzufügen. Testen Sie dies mit der ID des Containers, der NGINX ausführt. Ersetzen Sie die ID in diesem Beispiel durch die ID aus Ihrer Umgebung.

```bash
docker rm bd2424bfe7a5
```

Beachten Sie, dass der Container nicht entfernt werden kann, da er sich im Ausführungszustand befindet.

```bash
Error response from daemon: You cannot remove a running container a31c5a5f2a8d6e420435bfcadbe158fa6a26ed29c005a892171505cc0c2861b2. Stop the container before attempting removal or force remove
```

Halten Sie den Container über den Befehl `docker stop` an.

```bash
docker stop bd2424bfe7a5
```

Beachten Sie dabei, dass der NGINX-Container nicht aufgeführt wird, wenn Sie `docker ps` ausführen, um alle Container aufzulisten.

```bash
docker ps
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

Fügen Sie dem Befehl `docker ps` das Argument `-a` hinzu, um eine Liste aller Container zurückzugeben, einschließlich der Container, die angehalten wurden.

```bash
docker ps -a
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
bd2424bfe7a5        nginx               "nginx -g 'daemon of…"   13 seconds ago      Exited (0) 3 seconds ago                       focused_spence
```

Versuchen Sie erneut, den Löschvorgang auszuführen. Ersetzen Sie die ID in diesem Beispiel durch die ID aus Ihrer Umgebung.

```bash
docker rm bd2424bfe7a5
```

Dieser Vorgang gibt die Container-ID zurück.

```bash
bd2424bfe7a5
```

## <a name="delete-a-container-image"></a>Löschen eines Containerimage

Wenn Sie ein Containerimage nicht mehr verwenden, können Sie es über den Befehl `docker rmi` entfernen. Wenn ein Container über das Containerimage gestartet wurde, kann dieses nicht gelöscht werden. Dabei spielt es keine Rolle, ob der Container noch ausgeführt wird oder angehalten wurde. Sie müssen zunächst die Container entfernen. Wenn Sie das Argument `-f` zum Befehl `docker rmi` hinzufügen, wird erzwungen, dass alle zugeordneten Container entfernt werden. Anschließend wird auch das Containerimage entfernt.

Entfernen Sie das NGINX-Containerimage mithilfe des folgenden Befehls.

```bash
docker rmi nginx
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```bash
Untagged: nginx:latest
Untagged: nginx@sha256:4a5573037f358b6cdfa2f3e8a9c33a5cf11bcd1675ca72ca76fbe5bd77d0d682
Deleted: sha256:8b89e48b5f157d9455c963b57c85d21e2337c58b8c983bc06f88476610adc129
Deleted: sha256:119ded3eca5e85ef43ee966e74564c604ccda064d955a8c5ed762e1d5e87f428
Deleted: sha256:6ece91c2763d826487e707f7b8ec063742ad0ee56cc9e605465cce95550c9a7f
Deleted: sha256:cdb3f9544e4c61d45da1ea44f7d92386639a052c620d1550376f22f5b46981af
```

## <a name="summary"></a>Zusammenfassung

In dieser Einheit wurden einige grundlegende Docker-Vorgänge erläutert. In der nächsten Einheit erfahren Sie, wie Sie ein benutzerdefiniertes Containerimage erstellen.