<span data-ttu-id="90391-101">Bevor Sie einen Container oder eine integrierte Containeranwendung in Azure ausführen, werden Sie wahrscheinlich in einer lokalen Entwicklungsumgebung, wie z.B. Ihrem Laptop, arbeiten.</span><span class="sxs-lookup"><span data-stu-id="90391-101">Before you run a container or container-integrated application in Azure, you'll most likely work in a local development environment like your laptop.</span></span> <span data-ttu-id="90391-102">Diese Einheit hilft Ihnen dabei, Ihr System für die Containerentwicklung vorzubereiten.</span><span class="sxs-lookup"><span data-stu-id="90391-102">This unit helps you prepare your system for container development.</span></span>

## <a name="docker-for-windows-and-mac"></a><span data-ttu-id="90391-103">Docker für Windows und Mac</span><span class="sxs-lookup"><span data-stu-id="90391-103">Docker for Windows and Mac</span></span>

<span data-ttu-id="90391-104">Docker, Inc. hat zwei Anwendungen zum Installieren und Konfigurieren einer lokalen Containerentwicklungsumgebung veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="90391-104">Docker, Inc. has published two applications to install and configure a local container development environment.</span></span> <span data-ttu-id="90391-105">Im Wesentlichen bereitet jede Anwendung Ihr System mit Docker-Tools, wie z.B. der erforderlichen CLI und Automatisierungstools, vor.</span><span class="sxs-lookup"><span data-stu-id="90391-105">Essentially, each application prepares your system with Docker tooling, such as the necessary CLI and automation tools.</span></span> <span data-ttu-id="90391-106">Außerdem wird ein virtueller Computer erstellt, der die Docker-Plattform hostet.</span><span class="sxs-lookup"><span data-stu-id="90391-106">A virtual machine is also created that hosts the Docker platform.</span></span> <span data-ttu-id="90391-107">Die Umgebung ist so konfiguriert, dass Docker-Befehle an den virtuellen Computer weitergereicht werden.</span><span class="sxs-lookup"><span data-stu-id="90391-107">The environment is configured such that Docker commands are passed through to the virtual machine.</span></span> <span data-ttu-id="90391-108">Jede dieser Anwendungen ähnelt sich bezüglich der Funktionalität und umfasst die folgenden Funktionen:</span><span class="sxs-lookup"><span data-stu-id="90391-108">Each of these applications is similar in functionality and includes the following features:</span></span>

- <span data-ttu-id="90391-109">Docker-Plattform: Kernkomponenten, die zum Erstellen und Ausführen von Containern notwendig sind</span><span class="sxs-lookup"><span data-stu-id="90391-109">Docker platform - The core components necessary to create and run containers.</span></span>
- <span data-ttu-id="90391-110">Docker CLI: Befehlszeilenschnittstelle für die Interaktion mit Docker-Containern</span><span class="sxs-lookup"><span data-stu-id="90391-110">Docker CLI - The command-line interface for interacting with Docker containers</span></span>
- <span data-ttu-id="90391-111">Docker Compose: Automatisierungstools zum Definieren und Ausführen von Anwendungen mit mehreren Containern</span><span class="sxs-lookup"><span data-stu-id="90391-111">Docker Compose - Automation tooling for defining and running multi-container applications.</span></span>

<span data-ttu-id="90391-112">Um Docker auf Ihrem System zu installieren, führen Sie den Link für Ihr Betriebssystem aus.</span><span class="sxs-lookup"><span data-stu-id="90391-112">To install Docker on your system, follow the link that matches your operating system.</span></span>

- <span data-ttu-id="90391-113">Docker für Windows: https://www.docker.com/docker-windows</span><span class="sxs-lookup"><span data-stu-id="90391-113">Docker for Windows - https://www.docker.com/docker-windows</span></span>
- <span data-ttu-id="90391-114">Docker für Mac: https://www.docker.com/docker-mac</span><span class="sxs-lookup"><span data-stu-id="90391-114">Docker for Mac - https://www.docker.com/docker-mac</span></span>

## <a name="docker-for-windows-environments"></a><span data-ttu-id="90391-115">Docker für Windows-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="90391-115">Docker for Windows environments</span></span>

<span data-ttu-id="90391-116">Wenn Sie Docker für Windows verwenden, sind zwei Umgebungen verfügbar: Linux und Windows.</span><span class="sxs-lookup"><span data-stu-id="90391-116">When you use Docker for Windows, two environments are available: Linux and Windows.</span></span> <span data-ttu-id="90391-117">Mit der Linux-Umgebung können Sie Linux-Container auf Ihrem Windows-System ausführen.</span><span class="sxs-lookup"><span data-stu-id="90391-117">Using the Linux environment allows you to run Linux containers on your Windows system.</span></span> <span data-ttu-id="90391-118">Sie können eine Umgebung auswählen, indem Sie mit der rechten Maustaste auf das Docker-Taskleistensymbol klicken, **Wechseln zu Linux-Containern** auswählen und den angezeigten Anweisungen auf dem Bildschirm folgen.</span><span class="sxs-lookup"><span data-stu-id="90391-118">You can select an environment by right-clicking on the Docker task bar icon, selecting **Switch to Linux containers**, and following the on-screen prompts.</span></span>

![Docker für Windows, Wechseln zu Linux-Containern](../media-draft/2-docker-linux.png)

> [!NOTE]
> <span data-ttu-id="90391-120">Bei den Schritten in diesem Tutorial wird davon ausgegangen, dass Ihr System für die Arbeit mit Linux-Containern konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="90391-120">The steps in this tutorial assume that your system is configured to work with Linux containers.</span></span>

## <a name="docker-on-linux"></a><span data-ttu-id="90391-121">Docker unter Linux</span><span class="sxs-lookup"><span data-stu-id="90391-121">Docker on Linux</span></span>

<span data-ttu-id="90391-122">Wenn Sie auf einem Linux-basierten System arbeiten, können die Docker-Serverkomponenten und CLI-Tools manuell installiert werden.</span><span class="sxs-lookup"><span data-stu-id="90391-122">If you're working on a Linux-based system, the Docker server components and CLI tools can be manually installed.</span></span> <span data-ttu-id="90391-123">Befolgen Sie die Anweisungen unter [About Docker CE](https://docs.docker.com/install/#server) (Informationen zu Docker CE).</span><span class="sxs-lookup"><span data-stu-id="90391-123">Follow the instructions found on [About Dokcer CE](https://docs.docker.com/install/#server) for your specific Linux distribution.</span></span>

## <a name="validate-configuration"></a><span data-ttu-id="90391-124">Überprüfen der Konfiguration</span><span class="sxs-lookup"><span data-stu-id="90391-124">Validate configuration</span></span>

<span data-ttu-id="90391-125">Um zu überprüfen, ob Docker erfolgreich installiert und konfiguriert wurde, öffnen Sie ein Terminal, und führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="90391-125">To validate that Docker has been successfully installed and configured, open a terminal and run the following command:</span></span>

```bash
docker search nginx
```

<span data-ttu-id="90391-126">Wenn die Ausgabe der folgenden ähnelt, ist Ihre Umgebung bereit für die nächste Einheit.</span><span class="sxs-lookup"><span data-stu-id="90391-126">If you see output similar to the following, your environment is read for the next unit.</span></span>

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

## <a name="summary"></a><span data-ttu-id="90391-127">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="90391-127">Summary</span></span>

<span data-ttu-id="90391-128">In dieser Einheit haben Sie eine lokale Containerentwicklungsumgebung vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="90391-128">In this unit, you prepared a local container development environment.</span></span> <span data-ttu-id="90391-129">In der nächsten Einheit erfahren Sie mehr über grundlegende Docker-Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="90391-129">In the next unit, you will learn about some basic Docker operations.</span></span>