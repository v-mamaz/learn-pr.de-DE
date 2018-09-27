Stellen Sie sich vor, Ihr Unternehmen verwendet Containerimages für die Verwaltung von Computeworkloads. Für das Erstellen von Containerimages werden die lokalen Docker-Tools verwendet.

Sie können Azure Container Registry Tasks zum Erstellen dieser Container verwenden. Container Registry Tasks ermöglicht auch die Integration von DevOps-Prozessen mit automatischer Builderstellung nach dem Committen von Quellcode.

Automatisieren Sie die Erstellung eines Containerimages mit Azure Container Registry Tasks.

## <a name="create-a-container-image-with-azure-container-registry-tasks"></a>Erstellen eines Containerimages mit Azure Container Registry Tasks

Eine Dockerfile-Standarddatei stellt Buildanweisungen bereit. Mit Azure Container Registry Tasks können Sie alle Dockerfile-Dateien wiederverwenden, die Sie derzeit in Ihrer Umgebung verwenden, einschließlich mehrstufiger Builds.

In diesem Beispiel wird eine neue Dockerfile-Datei verwendet.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

Hierzu wird im ersten Schritt eine neue Datei mit dem Namen `Dockerfile` erstellt. Sie können einen beliebigen Text-Editor verwenden, um die Datei zu bearbeiten. In diesem Beispiel verwenden wir den Cloud Shell-Editor. Geben Sie den folgenden Befehl im Cloud Shell-Fenster ein, um den Editor zu öffnen.

```bash
code
```

Kopieren Sie den folgenden Inhalt in die neue Dockerfile-Datei. Speichern Sie die Datei unbedingt.

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

Speichern Sie mithilfe der Tastenkombination <kbd>STRG+S</kbd>. Nennen Sie die Datei nach Aufforderung „`Dockerfile`“.

Durch diese Konfiguration wird dem `node:9-alpine`-Image eine Node.js-Anwendung hinzugefügt. Anschließend wird der Container so konfiguriert, dass er die Anwendung über die Anweisung *EXPOSE* auf Port 80 bereitstellt.

Führen Sie nun den Azure CLI-Befehl `az acr build` aus, um den Build des Containerimages aus der Dockerfile-Datei zu erstellen.

```azurecli
az acr build --registry <acrName> --image helloacrtasks:v1 .
```

Während Sie den Befehl ausführen, können Sie sehen, wie der Build für das Image erstellt und mithilfe von Push in Ihre Containerregistrierung übertragen wird.

## <a name="verify-the-image"></a>Überprüfen des Images

Führen Sie den folgenden Befehl aus, um zu überprüfen, ob das Image erstellt und in der Registrierung gespeichert wurde.

```azurecli
az acr repository list --name <acrName> --output table
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```console
Result
-------------
helloacrtasks
```

Das Image `helloacrbuild` kann jetzt verwendet werden.
