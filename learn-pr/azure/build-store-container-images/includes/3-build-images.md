Mit Azure Container Registry Build können Sie ohne lokale Docker-Tools Containerimages in der Cloud erstellen. Container Registry Build ermöglicht auch die Integration von DevOps-Prozessen mit automatischer Erstellung nach dem Committen von Quellcode.

In dieser Einheit automatisieren Sie die Erstellung eines Containerimages mit Azure Container Registry Build.

## <a name="create-a-container-image-with-build"></a>Erstellen eines Containerimages mit Build

Bei Azure Container Registry Build wird für das Bereitstellen von Buildanweisungen eine Dockerfile-Standarddatei verwendet. Alle Dockerfile-Dateien, die Sie derzeit in Ihrer Umgebung verwenden, einschließlich mehrstufiger Builds, funktionieren mit Azure Container Registry Build.

Erstellen Sie eine Datei mit dem Namen `Dockerfile`, und öffnen Sie diese in einem Text-Editor Ihrer Wahl.

```bash
code Dockerfile
```

Kopieren Sie den folgenden Inhalt in die Datei, speichern Sie sie, und beenden Sie den Text-Editor. Die Dockerfile-Datei fügt dem Image `node:9-alpine` eine Node.js-Anwendung hinzu und konfiguriert den Container so, dass die Anwendung an Port 80 zur Verfügung steht.

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

Führen Sie den folgenden Befehl aus, um das Containerimage aus der Dockerfile-Datei zu erstellen.

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
```

Während dieses Vorgangs können Sie sehen, wie das Image erstellt und mithilfe von Push an Ihre Containerregistrierung übertragen wird.

## <a name="verify-the-image"></a>Überprüfen des Images

Führen Sie nach Abschluss des Buildvorgangs den folgenden Befehl aus, um zu überprüfen, ob das Image erstellt und in der Registrierung gespeichert wurde.

```azurecli
az acr repository list --name <acrName> --output table
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```console
Result
-------------
helloacrbuild
```

Das Image `helloacrbuild` kann jetzt verwendet werden.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit wurde mit Azure Container Registry Build die Erstellung eines Containerimages automatisiert. Dieses Image wurde dann in Azure Container Registry gespeichert. In der nächsten Einheit stellen Sie eine Instanz des neuen Containerimages in Azure Container Instances bereit.