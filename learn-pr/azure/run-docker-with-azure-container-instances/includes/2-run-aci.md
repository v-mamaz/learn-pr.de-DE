Azure Container Instances erleichtert die Erstellung und Verwaltung von Docker-Containern in Azure, ohne dass Sie virtuelle Computer bereitstellen oder einen übergeordneten Dienst einführen müssen. In dieser Einheit erstellen Sie einen Container in Azure und machen ihn mit einem vollqualifizierten Domänennamen (FQDN) über das Internet verfügbar.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Wie alle Azure-Ressourcen muss auch Azure Container Instances in einer Ressourcengruppe (einer logische Sammlung für die Bereitstellung und Verwaltung von Azure-Ressourcen) platziert werden.

Erstellen Sie mit dem Befehl `az group create` eine Ressourcengruppe.

Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen *myResourceGroup* am Standort *eastus* erstellt:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Erstellen eines Containers

Zum Erstellen eines Containers müssen Sie einen Namen, ein Docker-Image und eine Azure-Ressourcengruppe für den Befehl **az container create** angeben. Durch Angeben einer DNS-Namensbezeichnung kann der Container optional auch für das Internet verfügbar gemacht werden. In diesem Beispiel stellen Sie einen Container bereit, der eine kompakte Webanwendung hostet.

Führen Sie den folgenden Befehl aus, um eine Containerinstanz zu starten. Der *--dns-name-label*-Wert muss innerhalb der Azure-Region, in der Sie die Instanz erstellen, eindeutig sein. Passen Sie den Wert also ggf. entsprechend an:

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image microsoft/aci-helloworld \
    --ports 80 \
    --dns-name-label aci-demo
```

Innerhalb weniger Sekunden erhalten Sie eine Antwort auf Ihre Anforderung. Der Container befindet sich zunächst im Zustand **Wird erstellt...**, wird aber innerhalb weniger Sekunden gestartet. Sie können den Status mit dem Befehl `az container show` überprüfen:

```azurecli
az container show \
    --resource-group myResourceGroup \
    --name mycontainer \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

Wenn Sie den Befehl ausführen, werden der vollqualifizierte Domänenname (FQDN) des Containers und der Bereitstellungsstatus angezeigt:

```output
FQDN                                    ProvisioningState
--------------------------------------  -------------------
aci-demo.eastus.azurecontainer.io       Succeeded
```

Wenn der Container den Status **Erfolgreich** erreicht, navigieren Sie in Ihrem Browser zu seinem FQDN:

![Screenshot eines Browsers mit ausgeführter Anwendung in einer Azure-Containerinstanz](../media-draft/aci-app-browser.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine Azure-Containerinstanz erstellt, in der ein Webserver und eine Anwendung ausgeführt werden. Mithilfe des FQDN der Containerinstanz haben Sie außerdem auf die Anwendung zugegriffen.

In der nächsten Einheit konfigurieren Sie Neustartrichtlinien für Containerinstanzen.