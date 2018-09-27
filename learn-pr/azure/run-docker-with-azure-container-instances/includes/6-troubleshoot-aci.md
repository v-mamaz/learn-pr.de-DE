Im Folgenden führen Sie einige grundlegende Problembehandlungsvorgänge durch, z.B. das Abrufen von Containerprotokollen und Containerereignissen sowie das Anfügen dieser an eine Containerinstanz. Nach Abschluss dieses Moduls sollten Sie mit den grundlegenden Funktionen für die Problembehandlung bei Containerinstanzen vertraut sein.

## <a name="create-a-container"></a>Erstellen eines Containers

Beginnen Sie mit der Erstellung des folgenden Containers: 

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --image microsoft/sample-aks-helloworld \
    --ports 80 \
    --ip-address Public \
    --location eastus
```

## <a name="get-logs-from-a-container-instance"></a>Abrufen von Protokollen aus einer Containerinstanz

Sie können den Befehl `az container logs` verwenden, um Protokolle aus Ihrem Anwendungscode in einem Container anzuzeigen:

```azurecli
az container logs \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer
```

Beispielausgabe:

```output
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
Running inside /app/prestart.sh, you could add migrations to this file, e.g.:

#! /usr/bin/env bash

# Let the DB start
sleep 10;
# Run migrations
alembic upgrade head
```

## <a name="get-container-events"></a>Abrufen von Containerereignissen

Der Befehl `az container attach` stellt während des Startvorgangs des Containers Diagnoseinformationen bereit. Nachdem der Container gestartet wurde, werden auch STDOUT und STDERR auf Ihre lokale Konsole gestreamt:

```azurecli
az container attach \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer
```

Beispielausgabe:

```output
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-09-21 23:48:14+00:00) pulling image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:09+00:00) Successfully pulled image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:12+00:00) Created container
(count: 1) (last timestamp: 2018-09-21 23:49:13+00:00) Started container

Start streaming logs:
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
```

> [!TIP]
> Drücken Sie zum Trennen der Verbindung mit einem angefügten Container <kbd>STRG+C</kbd>.

## <a name="execute-a-command-in-a-container"></a>Ausführen eines Befehls in einem Container

Azure Container Instances unterstützt die Ausführung eines Befehls in einem ausgeführten Container. Die Ausführung eines Befehls in einem bereits gestarteten Container ist besonders bei der Anwendungsentwicklung und Problembehandlung von großem Nutzen. Am häufigsten wird dieses Feature zum Starten einer interaktiven Shell zum Debuggen von Problemen in einem ausgeführten Container verwendet.

In diesem Beispiel wird eine interaktive Terminalsitzung mit dem ausgeführten Container gestartet:

```azurecli
az container exec \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --exec-command /bin/sh
```

Sobald der Befehl ausgeführt wurde, arbeiten Sie effektiv innerhalb des Containers. In diesem Beispiel wurde der `ls`-Befehl ausgeführt, um den Inhalt des Arbeitsverzeichnisses anzuzeigen:

```output
# ls
__pycache__  main.py  prestart.sh  static  templates  uwsgi.ini
```

Führen Sie `exit` aus, um die Remotesitzung zu beenden.

## <a name="monitor-container-cpu-and-memory"></a>Überwachen von Container-CPU und -speicher

Sie sollten die Metriken zur CPU- und Speicherauslastung abrufen. Zu diesem Zweck müssen Sie zuerst die ID der Azure-Containerinstanz abrufen. In diesem Beispiel wird die ID in einer Variable namens `CONTAINER_ID` platziert:

```azurecli
CONTAINER_ID=$(az container show --resource-group <rgn>[sandbox resource group name]</rgn> --name mycontainer --query id --output tsv)
```

Verwenden Sie nun den `az monitor metrics list`-Befehl, um die Informationen zur CPU-Auslastung abzurufen:

```azurecli
az monitor metrics list \
    --resource $CONTAINER_ID \
    --metric CPUUsage \
    --output table
```

Beispielausgabe:

```output
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

Der folgende Befehl kann zum Abrufen der Informationen zur Speicherauslastung verwendet werden:

```azurecli
az monitor metrics list \
    --resource $CONTAINER_ID \
    --metric MemoryUsage \
    --output table
```

Beispielausgabe:

```output
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

Diese Informationen stehen Ihnen auch im Azure-Portal zur Verfügung. Öffnen Sie im Azure-Portal die Übersichtsseite einer Containerinstanz, um eine visuelle Darstellung der Informationen zur CPU- und Speicherauslastung anzuzeigen.

![Ansicht der Informationen zur CPU- und Speicherauslastung von Azure Container Instances im Azure-Portal](../media/6-cpu-memory.png)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
