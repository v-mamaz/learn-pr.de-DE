Bevor Sie einen Container oder eine integrierte Containeranwendung in Azure ausführen, werden Sie wahrscheinlich in einer lokalen Entwicklungsumgebung, wie z.B. Ihrem Laptop, arbeiten. Diese Einheit hilft Ihnen dabei, Ihr System für die Containerentwicklung vorzubereiten.

## <a name="docker-for-windows-and-mac"></a>Docker für Windows und Mac

Docker, Inc. hat zwei Anwendungen zum Installieren und Konfigurieren einer lokalen Containerentwicklungsumgebung veröffentlicht. Im Wesentlichen bereitet jede Anwendung Ihr System mit Docker-Tools, wie z.B. der erforderlichen CLI und Automatisierungstools, vor. Außerdem wird ein virtueller Computer erstellt, der die Docker-Plattform hostet. Die Umgebung ist so konfiguriert, dass Docker-Befehle an den virtuellen Computer weitergereicht werden. Jede dieser Anwendungen ähnelt sich bezüglich der Funktionalität und umfasst die folgenden Funktionen:

- Docker-Plattform: Kernkomponenten, die zum Erstellen und Ausführen von Containern notwendig sind
- Docker CLI: Befehlszeilenschnittstelle für die Interaktion mit Docker-Containern
- Docker Compose: Automatisierungstools zum Definieren und Ausführen von Anwendungen mit mehreren Containern

Um Docker auf Ihrem System zu installieren, führen Sie den Link für Ihr Betriebssystem aus.

- Docker für Windows: https://www.docker.com/docker-windows
- Docker für Mac: https://www.docker.com/docker-mac

## <a name="docker-for-windows-environments"></a>Docker für Windows-Umgebungen

Wenn Sie Docker für Windows verwenden, sind zwei Umgebungen verfügbar: Linux und Windows. Mit der Linux-Umgebung können Sie Linux-Container auf Ihrem Windows-System ausführen. Sie können eine Umgebung auswählen, indem Sie mit der rechten Maustaste auf das Docker-Taskleistensymbol klicken, **Wechseln zu Linux-Containern** auswählen und den angezeigten Anweisungen auf dem Bildschirm folgen.

![Docker für Windows, Wechseln zu Linux-Containern](../media-draft/2-docker-linux.png)

> [!NOTE]
> Bei den Schritten in diesem Tutorial wird davon ausgegangen, dass Ihr System für die Arbeit mit Linux-Containern konfiguriert ist.

## <a name="docker-on-linux"></a>Docker unter Linux

Wenn Sie auf einem Linux-basierten System arbeiten, können die Docker-Serverkomponenten und CLI-Tools manuell installiert werden. Befolgen Sie die Anweisungen unter [About Docker CE](https://docs.docker.com/install/#server) (Informationen zu Docker CE).

## <a name="validate-configuration"></a>Überprüfen der Konfiguration

Um zu überprüfen, ob Docker erfolgreich installiert und konfiguriert wurde, öffnen Sie ein Terminal, und führen Sie den folgenden Befehl aus:

```bash
docker search nginx
```

Wenn die Ausgabe der folgenden ähnelt, ist Ihre Umgebung bereit für die nächste Einheit.

```bash
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                                                  Official build of Nginx.                        9034                [OK]
jwilder/nginx-proxy                                    Automated Nginx reverse proxy for docker con…   1362                                    [OK]
richarvey/nginx-php-fpm                                Container running Nginx + PHP-FPM capable of…   589                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion                 LetsEncrypt container to use with nginx as p…   390                                     [OK]
kong                                                   Open-source Microservice & API Management la…   204                 [OK]
webdevops/php-nginx                                    Nginx with PHP-FPM                              106                                     [OK]
kitematic/hello-world-nginx                            A light-weight nginx container that demonstr…   102
zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server wi…   59                                      [OK]
bitnami/nginx                                          Bitnami nginx Docker Image                      54                                      [OK]
linuxserver/nginx                                      An Nginx container, brought to you by LinuxS…   37
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          36                                      [OK]
tobi312/rpi-nginx                                      NGINX on Raspberry Pi / armhf                   20                                      [OK]
nginxdemos/nginx-ingress                               NGINX Ingress Controller for Kubernetes . Th…   11
wodby/drupal-nginx                                     Nginx for Drupal container image                9                                       [OK]
blacklabelops/nginx                                    Dockerized Nginx Reverse Proxy Server.          9                                       [OK]
webdevops/nginx                                        Nginx container                                 8                                       [OK]
nginxdemos/hello                                       NGINX webserver that serves a simple page co…   7                                       [OK]
centos/nginx-18-centos7                                Platform for running nginx 1.8 or building n…   6
1science/nginx                                         Nginx Docker images that include Consul Temp…   4                                       [OK]
centos/nginx-112-centos7                               Platform for running nginx 1.12 or building …   3
pebbletech/nginx-proxy                                 nginx-proxy sets up a container running ngin…   2                                       [OK]
toccoag/openshift-nginx                                Nginx reverse proxy for Nice running on same…   1                                       [OK]
travix/nginx                                           NGinx reverse proxy                             1                                       [OK]
ansibleplaybookbundle/nginx-apb                        An APB to deploy NGINX                          0                                       [OK]
mailu/nginx                                            Mailu nginx frontend                            0                                       [OK]
```

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine lokale Containerentwicklungsumgebung vorbereitet. In der nächsten Einheit erfahren Sie mehr über grundlegende Docker-Vorgänge.