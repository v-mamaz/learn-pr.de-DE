In der letzten Einheit haben Sie mit vorgefertigten Containerimages gearbeitet, um einfache Docker-Vorgänge durchzuführen. In dieser Einheit erstellen Sie benutzerdefinierte Containerimages, übermitteln diese mithilfe von Push an eine öffentliche Containerregistrierung und führen Container über diese Images aus.

Containerimages können manuell oder mit einer sogenannten Dockerfile erstellt werden, um den Vorgang zu automatisieren. Es wird empfohlen, eine Dockerfile-Datei zu verwenden, aber in dieser Einheit werden beide Methoden veranschaulicht. Sie sollen verstehen, wie der manuelle Vorgang funktioniert, damit Sie wissen, was bei der Automatisierung mithilfe einer Dockerfile-Datei geschieht.

## <a name="manual-image-creation"></a>Manuelle Imageerstellung

Wenn Sie ein Containerimage manuell erstellen, werden die folgenden Aktionen durchgeführt:

- Sie starten eine Instanz eines Containers.
- Sie beginnen eine Terminalsitzung mit dem Container.
- Sie passen den Container an, indem Sie Software installieren und Konfigurationen ändern.
- Erfassen des Containers in einem neuen Image mit dem Befehl `docker capture`.

In diesem ersten Beispiel starten Sie eine Instanz eines Containers, in dem Python ausgeführt wird, erstellen eine „Hallo Welt“-Anwendung und erfassen den Container in einem neuen Image.

Führen Sie zunächst einen Container über das NGINX-Image aus. Dieser Befehl unterscheidet sich etwas von den Befehlen, die Sie in den vorherigen Einheiten ausgeführt haben. Weil Sie eine Terminalsitzung mit dem ausgeführten Container starten möchten, werden die Argumente `-t` und `-i` einbezogen. In Kombination weisen diese Argumente Docker an, ein Pseudoterminal zuzuweisen, das weiter ausgeführt wird. D.h., die Argumente `-t` und `-i` erstellen eine interaktive Sitzung mit dem ausführten Container.

Dann geben Sie an,dass das `python`-Containerimage verwendet werden soll und dass der Prozess, der im Container ausgeführt werden soll, `bash` ist.

```bash
docker run --name python-demo -ti python bash
```

Nachdem der Befehl ausgeführt wurde, sollte Ihre Terminalsitzung zum Pseudoterminal des Containers wechseln. Dieses erkennen Sie an der Terminalaufforderung, die sich etwa wie folgt geändert haben sollte:

```output
root@d8ccada9c61e:/#
```

Jetzt arbeiten Sie im Container. Sie werden feststellen, dass das Arbeiten in einem Container sich kaum vom Arbeiten in einem virtuellen oder physischen System unterscheidet. Sie können z.B. Dateien auflisten, erstellen und löschen, Software installieren und Konfigurationen anpassen. In diesem Beispiel wird ein Python-basiertes „Hallo Welt“-Skript erstellt. Führen Sie dazu den folgenden Befehl aus:

```bash
echo 'print("Hello World!")' > hello.py
```

Führen Sie den folgenden Befehl aus, um das Skript zu testen, während Sie sich noch im Container befinden:

```bash
python hello.py
```

Das erzeugt die folgende Ausgabe:

```output
Hello World!
```

Wenn das Skript wie erwartet ausgeführt wird, können Sie den Container über den Befehl `exit` verlassen:

```bash
exit
```

Verwenden Sie im Terminal Ihres lokalen Systems den Befehl `docker ps`, um alle Container aufzulisten, die aufgeführt werden:

```bash
docker ps
```

Beachten Sie, dass nichts ausgeführt wird. Wenn Sie `exit` in den ausgeführten Container eingegeben haben, wurde der Bash-Prozess abgeschlossen, wodurch der Container angehalten wurde. Dies entspricht dem erwarteten Verhalten und ist in Ordnung.

```output
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

Verwenden Sie `docker ps` erneut, und schließen Sie das `-a`-Argument mit ein. Dieser Befehl gibt eine Liste aller Container zurück, egal ob diese ausgeführt werden oder nicht.

```bash
docker ps -a
```

Beachten Sie, dass ein Container mit dem Namen *python-demo* den Status *Beendet* aufweist. Dieser Container ist die angehaltene Instanz des Containers, den Sie gerade beendet haben.

```output
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
```

Verwenden Sie den `docker commit`-Befehl, um ein neues Containerimage aus diesem Container zu erstellen. Das folgende Beispiel weist *docker commit* an, ein Image namens *python-custom* aus den *python-demo*-Containern zu erstellen.

```bash
docker commit python-demo python-custom
```

Nach Abschluss des Befehls sollten Sie eine Ausgabe ähnlich der folgenden erhalten:

```output
sha256:91a0cf9aa9857bebcd7ebec3418970f97f043e31987fd4a257c8ac8c8418dc38
```

Führen Sie nun `docker images` aus, um eine Liste der Containerimages anzuzeigen:

```bash
docker images
```

Sie sollten nun das benutzerdefinierte Python-Image sehen.

```output
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
python-custom       latest              1f231e7127a1        6 seconds ago       922MB
python              latest              638817465c7d        24 hours ago        922MB
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

Führen Sie einen Container über das neue Image aus. Sie müssen auch angeben, welcher Befehl oder Prozess innerhalb des Containers ausgeführt werden soll. Führen Sie in diesem Beispiel `python hello.py` aus.


```bash
docker run python-custom python hello.py
```

Der Container wird gestartet, und er gibt die Meldung „Hallo Welt“ aus. Der Python-Prozess ist dann abgeschlossen, und der Container wird angehalten.

```output
Hello World!
```

## <a name="automated-image-creation"></a>Automatische Imageerstellung

Im letzten Abschnitt wurde ein Containerimage manuell erstellt. Obwohl diese Methode für eine einmalige oder experimentelle Imageerstellung bestens geeignet ist, ist sie in einer Produktionsumgebung nicht tolerierbar. Die Erstellung eines Containerimages kann mithilfe einer *Dockerfile* und des `docker build`-Befehls automatisiert werden. Der *docker build*-Befehl startet im Wesentlichen einen Container, führt die in der *Dockerfile* enthaltenen Anweisungen aus und erfasst anschließend die Ergebnisse für ein neues Containerimage.

Erstellen Sie eine Datei namens *Dockerfile*, und geben Sie folgenden Text ein:

```bash
FROM python

WORKDIR ./app

RUN echo 'print("Hello World!")' > hello.py

CMD python hello.py
```

Die *FROM*-Anweisung gibt das Basisimage an, das während der Imageerstellung verwendet wird. Die *RUN*-Anweisung führt Befehle innerhalb des Containers aus. *RUN* kann dann zum Installieren von Software, zur Durchführung von Konfigurationsänderungen und zum Bereinigen des Containers vor der Erfassung genutzt werden. Die *CMD*-Anweisung gibt den Prozess an, der ausgeführt werden soll, wenn ein Container gestartet wird.

Verwenden Sie den `docker build`-Befehl, um ein neues Containerimage mithilfe der in der Dockerfile angegebenen Anweisungen zu erstellen.

```bash
docker build -t python-dockerfile .
```

Eine Ausgabe ähnlich der folgenden sollte angezeigt werden.

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

Verwenden Sie den `docker images`-Befehl, um eine Liste von Containerimages zurückzugeben.

```bash
docker images
```

Sie sollten nun das benutzerdefinierte Image sehen.

```output
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
python-dockerfile   latest              98c39b91770f        About a minute ago   922MB
python              latest              638817465c7d        26 hours ago         922MB
alpine              latest              11cd0b38bc3c        2 weeks ago          4.41MB
```

Verwenden Sie den `docker run`-Befehl, um einen Container aus dem benutzerdefinierten Image auszuführen.

Beachten Sie, dass dem Befehl `docker run` keine Argumente bereitgestellt wurden. Anders als bei der manuellen Erstellung eines Containerimages ermöglicht eine Dockerfile das Einschließen eines Befehls, der beim Containerstart ausgeführt wird. In diesem Fall ist der spezifische Befehl `python hello.py`, wodurch der Container das Python-Skript ausführt.

```bash
docker run python-dockerfile
```

Nachdem Sie den Befehl ausgeführt haben, sollte die Containerausgabe angezeigt werden.

```output
Hello World!
```

## <a name="push-the-image-to-a-public-registry"></a>Pushen des Images an eine öffentliche Registrierung

Docker Hub ist eine öffentliche Containerregistrierung. Damit Containerimages per Push an Docker Hub übertragen werden können, müssen Sie über ein Docker-Konto verfügen. Besuchen Sie ggf. die [Docker Hub-Website](https://hub.docker.com/), um sich für ein Konto zu registrieren.

Wenn Sie ein Docker Hub-Konto besitzen, muss das Containerimage mit dem Kontonamen gekennzeichnet werden. Verwenden Sie hierzu den `docker tag`-Befehl.

Im folgenden Beispiel wird das Image *python-dockerfile* mit dem Docker Hub-Kontonamen gekennzeichnet. Ersetzen Sie `<account name>` durch Ihren Docker Hub-Kontonamen.

```bash
docker tag python-dockerfile <account name>/python-dockerfile
```

Stellen Sie dann sicher, dass Sie über den `docker login`-Befehl bei Docker Hub angemeldet sind.

```bash
docker login
```

Übertragen Sie zuletzt das Image *python-dockerfile* mit dem Befehl `docker push` per Push an Docker Hub. Ersetzen Sie `<account name>` durch Ihren Docker Hub-Kontonamen.

```bash
docker push <account name>/python-dockerfile
```

Während das Containerimage in Docker Hub hochgeladen wird, wird Ihnen eine Ausgabe ähnlich der folgenden angezeigt:

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
```

Das Containerimage ist nun in Docker Hub gespeichert, und Sie können von jedem Gerät mit einer Internetverbindung über `docker pull` oder `docker run` auf dieses zugreifen.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie zwei Containerimages erstellt. Das erste wurde manuell erstellt, das zweite über eine Dockerfile.
