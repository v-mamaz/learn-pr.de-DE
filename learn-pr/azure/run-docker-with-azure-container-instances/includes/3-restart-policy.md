Da Container in Azure Container Instances sehr schnell und bequem bereitgestellt werden können, eignen sich diese perfekt zum Ausführen von einmaligen Aufgaben, wie dem Erstellen, Testen und Rendern von Bildern.

Mit einer konfigurierbaren Neustartrichtlinie können Sie angeben, dass Container nach dem Abschluss ihrer Prozesse beendet werden. Da Containerinstanzen nach Sekunden abgerechnet werden, fallen nur Gebühren für die Computerressourcen an, die beim Ausführen des Containers verwendet werden, der Ihre Aufgabe ausführt.

## <a name="container-restart-policies"></a>Neustartrichtlinien für Container

Azure Container Instances verfügt über drei Optionen für die Neustartrichtlinie:

| Neustartrichtlinie   | Beschreibung |
| ---------------- | :---------- |
| `Always` | Container in der Containergruppe werden immer neu gestartet. Diese Richtlinie eignet sich für Tasks mit langer Ausführungsdauer, z.B. Webserver. Dies ist die **Standardeinstellung**, wenn beim Erstellen des Containers keine Neustartrichtlinie angegeben wird. |
| `Never` | Container in der Containergruppe werden nie neu gestartet. Die Container werden höchstens einmal ausgeführt. |
| `OnFailure` | Container in der Containergruppe werden nur dann neu gestartet, wenn bei dem im Container ausgeführten Prozess ein Fehler auftritt (wenn er also mit einem Exitcode ungleich 0 beendet wird). Die Container werden mindestens einmal ausgeführt. Diese Richtlinie eignet sich für Container mit kurzlebigen Aufgaben. |

## <a name="run-to-completion"></a>Ausführen bis zum Abschluss

Wenn Sie die Richtlinie für den Neustart in der Praxis sehen möchten, erstellen Sie eine Containerinstanz aus dem Image *microsoft/aci-wordcount*, und geben Sie die Neustartrichtlinie *OnFailure* an. Bei diesem Beispielcontainer wird ein Python-Skript ausgeführt, das den Text von Shakespeares „Hamlet“ analysiert, die zehn häufigsten Wörter in STDOUT schreibt und dann beendet wird.

Führen Sie den Beispielcontainer mit dem folgenden `az container create`-Befehl aus:

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer-restart-demo \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure \
    --location eastus
```

Azure Container Instances startet den Container und beendet ihn, wenn die Anwendung (oder wie in diesem Fall das Skript) beendet wird. Wenn Azure Container Instances einen Container beendet, dessen Neustartrichtlinie *Never* oder *OnFailure* lautet, wird der Status des Containers auf **Beendet** festgelegt.

Sie können den Status des Containers mit dem Befehl `az container show` überprüfen:

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer-restart-demo \
    --query containers[0].instanceView.currentState.state
```

Sobald der Status des Beispielcontainers **Beendet** lautet, können Sie die Taskausgabe in den Containerprotokollen anzeigen. Führen Sie den `az container logs`-Befehl aus, um die Ausgabe des Skripts anzuzeigen:

```azurecli
az container logs \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer-restart-demo
```

Ausgabe:

```json
[('the', 990),
 ('and', 702),
 ('of', 628),
 ('to', 610),
 ('I', 544),
 ('you', 495),
 ('a', 453),
 ('my', 441),
 ('in', 399),
 ('HAMLET', 386)]
```