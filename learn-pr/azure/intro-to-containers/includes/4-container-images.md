Bisher haben Sie Docker-Images heruntergeladen und ausgeführt, die von anderen Benutzern erstellt wurden. In dieser Einheit erstellen Sie eigene Containerimages. Sie lernen Folgendes:

* Das manuelle Erstellen eines Images
* Das Erstellen des gleichen Images mithilfe eines stärker automatisierten Prozesses in Form einer Dockerfile
* Das Veröffentlichen Ihres Images auf Docker Hub, einer öffentlichen Containerregistrierung

## <a name="what-is-a-dockerfile"></a>Was ist eine Dockerfile?

Eine Dockerfile ist eine Textdatei, die alle Voraussetzungen für das Ausführen Ihres Containers enthält.

Eine Anweisung in der Dockerfile kann Folgendes definieren:

* Das übergeordnete Image, auf dem Ihr Image basiert
* Ein zu installierendes Softwarepaket
* Eine Konfigurationsdatei oder eine andere Datei, die für die Ausführung Ihrer App erforderlich ist
* Netzwerkeinstellungen, z.B. der Port, der zur Verfügung gestellt werden soll
* Der Befehl, der beim Start des Containers ausgeführt werden soll

Sie können ein Containerimage manuell oder mithilfe einer Dockerfile erstellen, um den Prozess zu automatisieren. Das manuelle Erstellen eines Docker-Images ist gut geeignet, um die Vorgehensweise zu erlernen. Durch das Erstellen einer Dockerfile wird der Prozess beschleunigt und kann einfacher wiederholt werden.

## <a name="what-is-docker-hub"></a>Was ist Docker Hub?

Docker Hub ist ein Ort, an dem Sie Docker-Images speichern und herunterladen können. Sie können Docker-Images herunterladen, die von Docker und der Docker-Community erstellt wurden, z.B. das nginx-Image, das Sie zuvor verwendet haben. Sie können ebenfalls eigene Images für die Docker-Community oder nur für Ihr Team freigeben.

## <a name="create-an-image-manually"></a>Manuelles Erstellen eines Images

In dieser Einheit erstellen Sie ein Docker-Image, das eine einfache Python-Anwendung ausführt.

1. Beginnen Sie mit dem Einbinden einer Containerinstanz aus dem [python](https://hub.docker.com/_/python/?azure-portal=true)-Image.

    ```bash
    docker run --name python-demo -it python bash
    ```

    Es dauert einen Moment, bis Docker das Image von Docker Hub heruntergeladen hat. Während der Wartezeit können Sie sich mit der Funktionsweise des Befehls vertraut machen.

    * Das Argument `--name` gibt den Namen Ihres Containers an, nämlich „python-demo“.
    * Die Argumente `-i` und `-t` werden zu einem Argument, `-it`, kombiniert. Mit diesen Argumenten wird eine interaktive Sitzung mit dem ausgeführten Container erstellt.
      * `-i` erstellt eine interaktive Sitzung mit dem Container.
      * `-t` erstellt ein Pseudoterminal, das dauerhaft ausgeführt wird.
    * `python` gibt das Basisimage an. Docker lädt dieses Image von Docker Hub herunter. Dieses Image ist mit einer Umgebung für die Python-Programmierung vorkonfiguriert.
    * `bash` gibt das Programm an, das ausgeführt werden soll.

    Stellen Sie sich dieses Setup als interaktive Umgebung vor, in der Sie Python-Apps schreiben. Sobald Ihre App fertig ist und ausgeführt wird, können Sie ein Image oder eine Momentaufnahme Ihrer Umgebung erstellen. Wenn Sie Ihre App weiter verbessern, können Sie zusätzliche Images für sich und Ihr Team erstellen.

    Ihre Terminalsitzung wechselt zum Pseudoterminal des Containers. Ihnen wird Folgendes angezeigt:

    ```docker
    root@d8ccada9c61e:/#
    ```

1. Führen Sie Folgendes über Ihre Docker-Sitzung aus, um ein Verzeichnis namens `./app` zu erstellen. Wechseln Sie anschließend in dieses Verzeichnis.

    ```bash
    mkdir ./app && cd ./app
    ```

    Obwohl es nicht zwingend erforderlich ist, können Sie Ihren Python-Code über das Verzeichnis `./app` hinzufügen.

1. Führen Sie Folgendes aus, um ein einfaches Python-Programm zu erstellen.

    ```bash
    echo 'print("Hello World!")' > hello.py
    ```

    Dieses Programm gibt „Hello World!“ im Terminal aus.

    > [!TIP]
    > In der Praxis können Sie ein Verzeichnis in Ihrer Arbeitsstation in ein Verzeichnis in Ihrem Container _einbinden_. Dadurch können Sie Ihren bevorzugten Editor verwenden, um Code auf Ihrer Arbeitsstation zu schreiben. Wenn Sie die Datei speichern, wird diese auch im Container angezeigt.

1. Führen Sie Folgendes aus, um Ihr Python-Programm zu testen.

    ```bash
    python hello.py
    ```

    Sie sehen Folgendes.

    ```output
    Hello World!
    ```

1. Beenden Sie die interaktive Sitzung.

    ```bash
    exit
    ```

1. Führen Sie über Ihren virtuellen Linux-Computer `docker ps` aus, um alle ausgeführten Container aufzulisten:

    ```bash
    docker ps
    ```

    Sie sehen, dass keine Container ausgeführt werden. 

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    ```

    Das liegt daran, dass das Beenden des Containers auch Ihre Bash-Sitzung beendet. Wenn die Anwendung oder der Dienst, den Ihr Container ausführt, beendet wird, hält Docker den Container an.

1. Führen Sie `docker ps` erneut aus, und fügen Sie das Argument `-a` hinzu. Dieser Befehl gibt alle ausgeführten und angehaltenen Container zurück.

    ```bash
    docker ps -a
    ```

    Folgendes sollte angezeigt werden:

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
    cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
    ```

   Ihr Container, **python-demo**, weist den Status **Exited** (Beendet) auf.

1. Führen Sie `docker commit` aus, um ein Image Ihres Containers zu erstellen.

   ```bash
   docker commit python-demo python-custom
   ```

   In diesem Fall erstellt Docker ein Image namens **python-custom** aus dem Container namens **python-demo**. Den Namen des Images können Sie nach Belieben ändern.

1. Führen Sie `docker images` aus, um Ihre Images aufzuführen.

    ```bash
    docker images
    ```

    Das Image **python-custom** wird angezeigt.

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-custom       latest              1f231e7127a1        6 seconds ago       922MB
    python              latest              638817465c7d        24 hours ago        922MB
    ```

1. Verwenden Sie `docker run`, um Ihr Image zu testen.

    ```bash
    docker run python-custom python app/hello.py
    ```

    Denken Sie daran, dass `docker run` den auszuführenden Befehl als letztes Argument verwendet. In diesem Fall ist der Befehl `python app/hello.py`.

    Sie sehen Folgendes.

    ```output
    Hello World!
    ```

    Da Sie diesen Container nicht interaktiv ausführen, wird das Python-Programm beendet, und der Container wird angehalten.

## <a name="use-a-dockerfile-to-create-an-image-automatically"></a>Verwenden einer Dockerfile zum automatischen Erstellen eines Images

In diesem Fall verwenden Sie einen stärker automatisierten Prozess, um das gleiche Docker-Image zu erstellen, das das Python-Programm ausführt.

Das manuelle Erstellen eines Images ist optimal dafür geeignet, neue Features zu entdecken und mit diesen zu experimentieren. Angenommen, Sie möchten den Prozess für Ihr Team freigeben oder diesen wiederholbar gestalten. Dies kann der Fall sein, wenn Sie jeden Abend ein neues Image erstellen möchten, das die neueste Version der Software ausführt, die Ihr Team erstellt.

An diesem Punkt kommt die Dockerfile ins Spiel. Stellen Sie sich eine Dockerfile als Möglichkeit vor, um Anweisungen festzuhalten, die Sie normalerweise manuell ausführen würden.

1. Führen Sie diesen Befehl über Ihren virtuellen Linux-Computer aus, um eine Dockerfile zu erstellen, die Ihr Python-Programm ausführt.

    ```bash
    cat << EOF > Dockerfile
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    EOF
    ```

    In diesem Beispiel wird nur eine einfache Möglichkeit zum Erstellen der Datei vorgestellt. In der Praxis würden Sie Ihren bevorzugten Code-Editor für die Erstellung verwenden.

    Geben Sie die Dockerfile in der Konsole aus.

    ```bash
    cat Dockerfile
    ```

    Sie sehen Folgendes.

    ```output
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    ```

    Im Folgenden finden Sie einen Überblick über die Funktionen einer Dockerfile.

    * `FROM` gibt das übergeordnete Image an, auf dem dieses Image basieren soll. In diesem Fall ist **python** das übergeordnete Image.
    * `WORKDIR` gibt das Arbeitsverzeichnis für alle `RUN`- und `CMD`-Anweisungen an, die später in der Dockerfile angezeigt werden. Docker erstellt dieses Verzeichnis für Sie, in diesem Fall `./app`.
    * `RUN` gibt einen Befehl an, der im Container ausgeführt werden soll. Sie können `RUN` zum Installieren von Software, zum Durchführen von Konfigurationsänderungen und zum Bereinigen des Containers vor der Erfassung verwenden. In dieser Einheit schreiben wir ein einfaches Python-Programm unter `./app/hello.py`.
    * `CMD` gibt den Prozess an, der beim Start des Containers ausgeführt werden soll. In diesem Fall wird `python hello.py` über das Verzeichnis `/.app` ausgeführt.

    Sie haben wahrscheinlich bemerkt, dass diese Schritte nahezu identisch mit denen sind, die Sie zum manuellen Erstellen des Images durchgeführt haben. Indem Sie diese Schritte in Form von Code ausdrücken, kann der Prozess einfacher freigegeben und wiederholt werden.

1. Führen Sie `docker build` aus, um das Image mithilfe der Anweisungen zu erstellen, die in der Dockerfile enthalten sind.

    ```bash
    docker build -t python-dockerfile .
    ```

    Es dauert in der Regel nur wenige Sekunden, bis Docker Ihr Image erstellt hat.

    Ihnen sollte eine Ausgabe wie die folgende angezeigt werden.

    ```output
    Sending build context to Docker daemon  2.048kB
    Step 1/4 : FROM python
     ---> 638817465c7d
    Step 2/4 : WORKDIR ./app
     ---> Running in 990d17e86466
    Removing intermediate container 990d17e86466
     ---> 59a074a092cc
    Step 3/4 : RUN echo 'print("Hello World!")' > hello.py
     ---> Running in aed707c53bc5
    Removing intermediate container aed707c53bc5
     ---> d7f55a9d0e85
    Step 4/4 : CMD python hello.py
     ---> Running in e87ec55a8d36
    Removing intermediate container e87ec55a8d36
     ---> 98c39b91770f
    Successfully built 98c39b91770f
    Successfully tagged python-dockerfile:latest
    ```

1. Verwenden Sie `docker images`, um Ihre Images aufzuführen.

    ```bash
    docker images
    ```

    Sie sehen das Image **python-dockerfile**, das Sie gerade erstellt haben.

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-dockerfile   latest              8ed5f85c5e5b        24 seconds ago      923MB
    python-custom       latest              6789cbe2cceb        4 minutes ago       923MB
    python              latest              a9d071760c82        2 weeks ago         923MB
    ```

1. Verwenden Sie `docker run`, um Ihren Container zu testen.

    ```bash
    docker run python-dockerfile
    ```

    Sie sehen Folgendes.

    ```output
    Hello World!
    ```

    Im Gegensatz zum Testen eines manuell erstellten Images geben Sie hier nicht den Befehl an, der ausgeführt werden soll (`python app/hello.py`). Dieser ist in Ihrer Dockerfile enthalten, der Befehl ist also im Image integriert.

## <a name="publish-your-image-to-docker-hub"></a>Veröffentlichen Ihres Images auf Docker Hub

Sie benötigen ein Konto, um ein Image auf Docker Hub zu veröffentlichen. In diesem Abschnitt richten Sie ein Docker Hub-Konto ein und veröffentlichen das Image **python-dockerfile** auf Docker Hub.

1. [Erstellen Sie ein Docker Hub-Konto](https://hub.docker.com?azure-portal=true).

1. Exportieren Sie den Docker Hub-Kontonamen als Umgebungsvariable. Ersetzen Sie **account-name** durch den Namen Ihres Kontos.

    ```bash
    export docker_account=account-name
    ```

    Diese Umgebungsvariable erleichtert das Ausführen der folgenden Befehle.

1. Führen Sie `docker tag` aus, um das Image mit Ihrem Docker Hub-Kontonamen zu versehen.

    ```bash
    docker tag python-dockerfile $docker_account/python-dockerfile
    ```

1. Führen Sie `docker login` aus, um sich bei Docker Hub anzumelden.

    ```bash
    docker login
    ```

    Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, wenn Sie dazu aufgefordert werden.

1. Führen Sie `docker push` aus, um das Image **python-dockerfile** in Docker Hub hochzuladen.

    ```bash
    docker push $docker_account/python-dockerfile
    ```

    Ihnen wird daraufhin eine Ausgabe angezeigt, die in etwa wie folgt aussieht:

    ```output
    The push refers to repository [docker.io/account/python-dockerfile]
    f39073ca4d5a: Pushed
    9dfcec2738a9: Pushed
    ffab8273c674: Mounted from account/python
    e6f6cbe5e14e: Mounted from account/python
    3eb255f8a6ac: Mounted from account/python
    b860b6c48eec: Mounted from account/python
    1fa8778eb779: Mounted from account/python
    fa0c3f992cbd: Mounted from account/python
    ce6466f43b11: Mounted from account/python
    719d45669b35: Mounted from account/python
    3b10514a95be: Mounted from account/python
    latest: digest: sha256:b816c32382d06ac74530d56f2a7b83000c86174218f430c6bb5039fdcfba38aa size: 2631
    ```

    Ihr Docker-Image ist nun in Docker Hub gespeichert. Sie können `docker pull` oder `docker run` von einem anderen Computer aus verwenden, um Ihr Image herunterzuladen oder über Docker Hub auszuführen. Hier sind zwei Beispiele:

    1. In diesem Beispiel wird das aktuelle Image von Docker Hub heruntergeladen.

        ```bash
        docker pull my_docker_account/python-dockerfile
        ```

    1. In diesem Beispiel wird der Container ausgeführt.

        ```bash
        docker run my_docker_account/python-dockerfile
        ```

1. Testen Sie Ihren Container.

    Navigieren Sie zu [Ihrem Docker Hub-Konto](https://hub.docker.com?azure-portal=true). Ihr Docker-Image wird auf der Registerkarte **Repositories** (Repositorys) angezeigt.

    ![Das Docker-Image auf Docker Hub](../media/4-docker-hub-python-dockerfile.png)
