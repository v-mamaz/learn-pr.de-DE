Hier erstellen Sie einen Container in Azure und machen ihn mit einem vollqualifizierten Domänennamen (FQDN) über das Internet verfügbar.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="why-use-azure-container-instances"></a>Was spricht für die Verwendung von Azure Container Instances?

Azure Container Instances ist hilfreich für Szenarien mit isolierten Containern. Hierzu zählen unter anderem einfache Anwendungen, Aufgabenautomatisierung und Buildaufträge. Azure Container Instances bietet folgende Vorteile:

- **Schneller Start:** Containern können in Sekundenschnelle gestartet werden.
- **Sekundengenaue Abrechnung:** Kosten fallen nur während der Containerausführung an.
- **Sicherheit auf Hypervisor-Ebene:** Isolieren Sie Ihre Anwendung so umfassend wie auf einem virtuellen Computer.
- **Benutzerdefinierte Größen:** Geben Sie exakte Werte für CPU-Kerne und Arbeitsspeicher an.
- **Persistenter Speicher:** Binden Sie Azure Files-Freigaben direkt in einen Container ein, um den Zustand abzurufen und zu speichern.
- **Linux und Windows:** Erstellen Sie Zeitpläne für Windows- und Linux-Container über die gleiche API.

Für Szenarien, die eine umfassende Containerorchestrierung erfordern (etwa für die containerübergreifende Dienstermittlung, automatische Skalierung und für koordinierte Anwendungsupgrades), empfehlen wir Azure Kubernetes Service (AKS).

## <a name="create-a-container"></a>Erstellen eines Containers

Um einen Container zu erstellen, müssen Sie einen Namen, ein Docker-Image und eine Azure-Ressourcengruppe für den Befehl **az container create** angeben. Durch Angeben einer DNS-Namensbezeichnung kann der Container optional auch für das Internet verfügbar gemacht werden. In diesem Beispiel stellen Sie einen Container bereit, der eine kompakte Web-App hostet. Außerdem können Sie den Standort des Images auswählen. Im Beispiel unten wird „USA, Osten“ verwendet, allerdings können Sie diese Angabe durch einen Ihnen am nächstgelegenen Standort aus der folgenden Liste ersetzen.

<!-- TODO: fix region list so it's not hardcoded here --> Mit der kostenlosen Sandbox können Sie in einem Teil der globalen Azure-Regionen Ressourcen erstellen. Wählen Sie eine Region aus der folgenden Liste aus, wenn Sie Ressourcen erstellen:

:::row:::
    :::column:::
        - westus2
        - centralus
        - eastus
        - westeurope
        - southeastasia
    :::column-end:::
:::row-end:::

Führen Sie in Cloud Shell den folgenden Befehl aus, um eine Containerinstanz zu starten. Der Wert `--dns-name-label` muss innerhalb der Azure-Region, in der Sie die Instanz erstellen, eindeutig sein. Passen Sie `[dns-name]` also ggf. entsprechend an.

```azurecli
az container create --resource-group <rgn>[sandbox resource group name]</rgn> --name mycontainer --image microsoft/aci-helloworld --ports 80 --dns-name-label [dns-name] --location eastus
```

Innerhalb weniger Sekunden erhalten Sie eine Antwort auf Ihre Anforderung. Der Container befindet sich zunächst im Zustand **Wird erstellt...**, wird aber innerhalb weniger Sekunden gestartet. Sie können den Status mit dem Befehl `az container show` überprüfen:

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
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

Wenn der Container den Status **Erfolgreich** erreicht, navigieren Sie in Ihrem Browser zu seinem FQDN, um den Status zu überprüfen.

Hier haben Sie eine Azure-Containerinstanz erstellt, in der ein Webserver und eine Anwendung ausgeführt werden. Mithilfe des FQDN der Containerinstanz haben Sie außerdem auf die Anwendung zugegriffen.