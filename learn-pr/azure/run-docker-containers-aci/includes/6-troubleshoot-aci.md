In dieser Einheit führen Sie einige grundlegende Problembehandlungsvorgänge durch, z.B. das Abrufen von Containerprotokollen und Containerereignissen sowie das Anfügen dieser an eine Containerinstanz. Nach Abschluss dieses Moduls sollten Sie mit den grundlegenden Funktionen für die Problembehandlung von Containerinstanzen vertraut sein.

## <a name="create-a-container"></a>Erstellen eines Containers

Erstellen Sie zunächst einen Container, den Sie für diese Einheit verwenden. Sie können diesen Schritt überspringen, wenn Sie noch über den ersten Container verfügen, den Sie im Rahmen dieses Moduls erstellt haben.

```azurecli
az container create --resource-group myResourceGroup --name mycontainer --image microsoft/aci-helloworld --ports 80 --ip-address Public
```

## <a name="get-logs-from-a-container-instance"></a>Abrufen von Protokollen aus einer Containerinstanz

Die können den Befehl `az container logs` verwenden, um Protokolle aus Ihrem Anwendungscode in einem Container anzuzeigen.

```azazurecli
az container logs --resource-group myResourceGroup --name mycontainer
```

Es folgt die Protokollausgabe des Beispielcontainers, nachdem mehrmals auf eine Web-App zugegriffen wurde.

```bash
listening on port 80
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:24 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:24 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://23.101.136.193/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:25 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:27 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
```

## <a name="get-container-events"></a>Abrufen von Containerereignissen

Der Befehl `az container attach` stellt während des Startvorgangs des Containers Diagnoseinformationen bereit. Nachdem der Container gestartet wurde, werden auch STDOUT und STDERR auf Ihre lokale Konsole gestreamt.

```azazurecli
az container attach --resource-group myResourceGroup --name mycontainer
```

Beispielausgabe


```bash
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-08-20 21:43:26+00:00) pulling image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-08-20 21:43:32+00:00) Successfully pulled image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-08-20 21:43:33+00:00) Created container
(count: 1) (last timestamp: 2018-08-20 21:43:33+00:00) Started container

Start streaming logs:
listening on port 80
listening on port 80
```

## <a name="execute-a-command-in-a-container"></a>Ausführen eines Befehls in einem Container

Azure Container Instances unterstützt die Ausführung eines Befehls in einem ausgeführten Container. Die Ausführung eines Befehls in einem bereits gestarteten Container ist besonders bei der Anwendungsentwicklung und Problembehandlung von großem Nutzen. Am häufigsten wird dieses Features zum Starten einer interaktiven Befehlsshell verwendet, sodass Probleme in einem ausgeführten Container behoben werden können.

In diesem Beispiel wird eine interaktive Terminalsitzung mit dem ausgeführten Container gestartet.

```azurecli
az container exec --resource-group myResourceGroup --name mycontainer --exec-command /bin/sh
```

Sobald der Befehl ausgeführt wurde, arbeiten Sie effektiv innerhalb des Containers. In diesem Beispiel wurde der `ls`-Befehl ausgeführt, um den Inhalt des Arbeitsverzeichnisses anzuzeigen.

```bash
usr/src/app # ls
index.html         node_modules       package.json
index.js           package-lock.json
```

Geben Sie `exit` ein, um die Remotesitzung zu beenden.

## <a name="monitor-container-cpu-and-memory"></a>Überwachen von Container-CPU und -Arbeitsspeicher

Sie sollten die Metriken zur CPU- und Arbeitsspeicherauslastung abrufen. Zu diesem Zweck müssen Sie zuerst die ID der Azure-Containerinstanz abrufen. In diesem Beispiel wird die ID in einer Variable namens `CONTAINER_ID` platziert.

```azurecli
CONTAINER_ID=$(az container show --resource-group myResourceGroup --name mycontainer --query id --output tsv)
```

Verwenden Sie nun den `az monitor metrics list`-Befehl, um die Informationen zur CPU-Auslastung abzurufen.

```azurecli
az monitor metrics list --resource $CONTAINER_ID --metric CPUUsage --output table
```

Beispielausgabe

```bash
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:39:00  CPU Usage
2018-08-20 21:40:00  CPU Usage
2018-08-20 21:41:00  CPU Usage
2018-08-20 21:42:00  CPU Usage
2018-08-20 21:43:00  CPU Usage      0.375
2018-08-20 21:44:00  CPU Usage      0.875
2018-08-20 21:45:00  CPU Usage      1
2018-08-20 21:46:00  CPU Usage      3.625
2018-08-20 21:47:00  CPU Usage      1.5
2018-08-20 21:48:00  CPU Usage      2.75
2018-08-20 21:49:00  CPU Usage      1.625
2018-08-20 21:50:00  CPU Usage      0.625
2018-08-20 21:51:00  CPU Usage      0.5
2018-08-20 21:52:00  CPU Usage      0.5
2018-08-20 21:53:00  CPU Usage      0.5
```

Der folgende Befehl kann zum Abrufen der Informationen zur Arbeitsspeicherauslastung verwendet werden.

```azurecli
az monitor metrics list --resource $CONTAINER_ID --metric MemoryUsage --output table
```

Beispielausgabe

```bash
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:43:00  Memory Usage
2018-08-20 21:44:00  Memory Usage  0.0
2018-08-20 21:45:00  Memory Usage  15917056.0
2018-08-20 21:46:00  Memory Usage  16744448.0
2018-08-20 21:47:00  Memory Usage  16842752.0
2018-08-20 21:48:00  Memory Usage  17190912.0
2018-08-20 21:49:00  Memory Usage  17506304.0
2018-08-20 21:50:00  Memory Usage  17702912.0
2018-08-20 21:51:00  Memory Usage  17965056.0
2018-08-20 21:52:00  Memory Usage  18509824.0
2018-08-20 21:53:00  Memory Usage  18649088.0
2018-08-20 21:54:00  Memory Usage  18845696.0
2018-08-20 21:55:00  Memory Usage  19181568.0
```

Diese Informationen stehen Ihnen auch im Azure-Portal zur Verfügung. Öffnen Sie im Azure-Portal die Übersichtsseite einer Containerinstanz, um eine grafische Darstellung der Informationen zur CPU- und Arbeitsspeicherauslastung anzuzeigen.

![Ansicht der Informationen zu der CPU- und Arbeitsspeicherauslastung von Azure Container Instances im Azure-Portal](../media-draft/cpu-memory.png)

## <a name="clean-up"></a>Bereinigen

Dies ist die letzte Einheit des Azure Container Instances-Lernmoduls. Sie können nun die erstellten Ressourcen bereinigen, indem Sie die Ressourcengruppe löschen. Verwenden Sie hierzu den Befehl „az group delete“.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie einige Problembehandlungsvorgänge kennengelernt, z.B. das Abrufen von Containerprotokollen und Containerereignissen sowie das Anfügen dieser an eine Containerinstanz.