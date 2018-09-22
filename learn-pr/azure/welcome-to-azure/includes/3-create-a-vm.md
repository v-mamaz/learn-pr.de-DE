Sie haben sich wahrscheinlich auf einen bestimmten Fachbereich spezialisiert. Vielleicht sind Sie Speicheradministrator oder Experte für Virtualisierung, oder Sie beschäftigen sich mit den neusten Sicherheitsmaßnahmen. Wenn Sie noch studieren, haben Sie sich möglicherweise aber noch gar nicht spezialisiert.

::: zone pivot="windows-cloud"

Die meisten Menschen – egal, in welcher Position –, die sich zum ersten Mal mit einer Cloud beschäftigen, erstellen zunächst einmal einen virtuellen Computer. In diesem Beispiel wird ein virtueller Computer erstellt, der Windows Server 2016 ausführt.

::: zone-end

::: zone pivot="linux-cloud"

Die meisten Menschen – egal, in welcher Position –, die sich zum ersten Mal mit einer Cloud beschäftigen, erstellen zunächst einmal einen virtuellen Computer. In diesem Beispiel wird ein virtueller Computer erstellt, der Ubuntu 16.04 ausführt.

::: zone-end

Es gibt verschiedene Möglichkeiten, einen virtuellen Computer in Azure zu erstellen. In diesem Beispiel wird mithilfe eines virtuellen Windows- oder Linux-Computers ein interaktives Terminal namens Cloud Shell erstellt. Wenn Sie täglich über das Terminal arbeiten, ist ihnen bestimmt klar, dass dies die schnellste Möglichkeit ist.

::: zone pivot="windows-cloud"

> [!TIP]
> Arbeiten Sie lieber mit Linux, oder möchten Sie etwas Neues ausprobieren? Klicken Sie oben auf der Seite auf **Linux**, um einen virtuellen Linux-Computer auszuführen.

::: zone-end

::: zone pivot="linux-cloud"

> [!TIP]
> Arbeiten Sie lieber mit Windows, oder möchten Sie etwas Neues ausprobieren? Klicken Sie oben auf der Seite auf **Windows**, um einen virtuellen Windows Server-Computer auszuführen.

::: zone-end

Nachfolgend werden einige Grundbegriffe erläutert, und Sie erfahren, wie Sie Ihren ersten virtuellen Computer starten können.

## <a name="what-is-a-virtual-machine"></a>Was ist ein virtueller Computer?

Ein virtueller Computer (VM) ist eine Softwareemulation eines physischen Computers. Da es sich um Software handelt, können Tausende von Azure-VMs innerhalb einer Minute erstellt und anschließend wieder gelöscht werden, wenn Sie sie nicht mehr brauchen. Die Kosten sind gering, und Sie zahlen auf die Minute genau nur dann für die Computeressourcen, wenn Sie sie benötigen. Außerdem gibt es einige Möglichkeiten, die VMs so zu konfigurieren, dass sie Ihren Ansprüchen gerecht werden.

::: zone pivot="windows-cloud"

Eine Momentaufnahme einer VM, die gerade ausgeführt wird, wird als _Image_ bezeichnet. Azure stellt Images für Windows sowie für einige Linux-Versionen zur Verfügung. Außerdem können Sie eigene vorkonfigurierte Images erstellen, damit Bereitstellungen schneller durchgeführt werden können. In diesem Beispiel wird eine Windows Server 2016-VM erstellt, die von Microsoft bereitgestellt wird.

::: zone-end

::: zone pivot="linux-cloud"

Eine Momentaufnahme einer VM, die gerade ausgeführt wird, wird als _Image_ bezeichnet. Azure stellt Images für Windows sowie für einige Linux-Versionen zur Verfügung. Außerdem können Sie eigene vorkonfigurierte Images erstellen, damit Bereitstellungen schneller durchgeführt werden können. In diesem Beispiel wird eine Ubuntu 16.04-VM erstellt, die von Canonical bereitgestellt werden.

::: zone-end

## <a name="what-defines-a-virtual-machine-on-azure"></a>Was macht einen virtuellen Computer in Azure aus?

Ein virtueller Computer wird von verschiedenen Faktoren beeinflusst, einschließlich der Größe und dem Standort. Bevor Sie den virtuellen Computer erstellen, werden nachfolgend die wichtigsten Aspekte erläutert.

:::row:::
    :::column:::
        **Größe**
    :::column-end:::
    :::column span="3"::: Die Prozessorgeschwindigkeit, die Speicherkapazität, die anfängliche Auslastung des Speichers und die erwartete Netzwerkbandbreite werden von der _Größe_ der VM bestimmt. Einige Größen umfassen sogar spezielle Hardware wie GPUs für intensives Grafikrendering und die Bearbeitung von Videos.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **Region**
    :::column-end:::
    :::column span="3"::: Azure besteht aus Rechenzentren, die auf der ganzen Welt verteilt sind. Als _Region_ werden mehrere Azure-Rechenzentren in einem geografisch begrenzten Gebiet bezeichnet. Jede Azure-Ressource, einschließlich virtueller Computer, wird einer Region zugewiesen. Beispiele für Regionen sind „USA, Osten“ und „Europa, Norden“.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **Netzwerk**
    :::column-end:::
    :::column span="3"::: Ein _virtuelles Netzwerk_ ist ein logisch isoliertes Netzwerk in Azure. Jeder virtuelle Computer in Azure wird einem virtuellen Netzwerk zugewiesen. Azure stellt Firewalls auf Cloudebene für Ihre virtuellen Netzwerke (_Netzwerksicherheitsgruppen_) bereit.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **Ressourcengruppen**
    :::column-end:::
    :::column span="3"::: Virtuelle Computer und Cloudressourcen werden in logische Container zusammengefasst, die als _Ressourcengruppen_ bezeichnet werden. Gruppen werden in der Regel verwendet, um mehrere Ressourcen zu organisieren, die gemeinsam als Bestandteile einer Anwendung oder eines Dienst bereitgestellt werden. Sie können Ressourcengruppen über den jeweiligen Namen finden.
    :::column-end:::
:::row-end:::

## <a name="what-is-azure-cloud-shell"></a>Was ist Azure Cloud Shell?

Azure Cloud Shell ist ein browserbasierter Dienst zum Verwalten und Entwickeln von Azure-Ressourcen über die Befehlszeile. Stellen Sie sich Cloud Shell als eine interaktive Konsole vor, die in der Cloud ausgeführt wird.

Cloud Shell stellt zwei Funktionen bereit, aus denen Sie auswählen können: Bash und PowerShell. Über beide Funktionen erhalten Sie Zugriff auf die Azure CLI, die Befehlszeilenschnittstelle für Azure.

Sie können jede beliebige Verwaltungsschnittstelle von Azure verwenden, einschließlich des Azure-Portals, der Azure CLI und Azure PowerShell, um eine VM (egal, welcher Art) zu verwalten. Zu Lernzwecken wird hier die Azure CLI verwendet, um virtuelle Windows- oder Linux-Computer zu erstellen und zu verwalten.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="creating-resources-in-azure"></a>Erstellen von Ressourcen in Azure

Normalerweise ist der erste Schritt das Anlegen einer _Ressourcengruppe_, die alle Elemente enthält, die wir erstellen müssen. Dies ermöglicht uns, alle VMs, Datenträger, Netzwerk-Schnittstellen und andere Elemente unserer Lösung als Einheit zu verwalten. Wir erstellen eine Ressourcengruppe, indem wir in der Azure CLI den Befehl `az group create` ausführen. Der Befehl verwendet `--name` zum Vergeben eines eindeutigen Namens in unserem Abonnement und `--location`, um Azure anzugeben, in welcher Region auf der Welt die Ressourcen standardmäßig angesiedelt sein sollen.

Da wir uns in der kostenlosen Azure-Sandbox-Umgebung befinden, müssen Sie diesen Schritt nicht durchführen, sondern verwenden stattdessen die vorab erstellte Ressourcengruppe **<rgn>[Ressourcengruppenname]</rgn>**.

## <a name="choosing-a-location"></a>Auswählen eines Standorts

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

::: zone pivot="windows-cloud"

## <a name="create-a-windows-vm"></a>Erstellen einer Windows-VM

Nachfolgend wird erläutert, wie Sie Ihre Windows-VM startbereit machen.

1. Führen Sie rechts auf dieser Seite in Cloud Shell den Befehl `az vm create` aus, um eine neue VM zu erstellen. Der Befehl erstellt die VM am Standort „USA, Osten“. Sie können diesen jedoch in einen beliebigen der oben aufgeführten Standorte ändern &mdash;. Wir empfehlen allerdings, einen in Ihrer Nähe auszuwählen.

    ```azurecli
    az vm create \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --image Win2016Datacenter \
      --size Standard_DS2_v2 \
      --location eastus \
      --admin-username azureuser
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    Obwohl Sie das Windows-Administratorkennwort über den Befehl angeben können, werden Sie hier aufgefordert, eines einzugeben. Wählen Sie ein Kennwort, das mindestens 12 Zeichen in einer Kombination aus Groß- und Kleinbuchstaben, Zahlen und Symbolen umfasst. Verwenden Sie kein Kennwort, das Sie an anderer Stelle verwenden.

    Es dauert vier bis fünf Minuten, bis Sie auf die VM zugreifen können. Vergleichen Sie das mit der Zeit, die es dauert, ein System für Ihr Rechenzentrum zu kaufen, es einzubauen und zu konfigurieren. Der Unterschied ist erheblich.

Solange Sie warten, können Sie sich den Befehl genauer ansehen, den Sie zuvor ausgeführt haben.

* Die VM hat den Namen **myVM**. Über diesen Namen kann die VM in Azure ermittelt werden. Außerdem handelt es sich um den internen Hostnamen der VM oder den Computernamen.
* Die Ressourcengruppe bzw. der logische Container der VM wird als **<rgn>[Sandbox-Ressourcengruppenname]</rgn>** bezeichnet.
* **Win2016Datacenter** gibt das Image der Windows Server 2016-VM an.
* **Standard_DS2_v2** bezieht sich auf die Größe der VM. Diese Größe bietet zwei virtuelle CPUs und 7 GB Arbeitsspeicher.
* Über den Benutzernamen und das Kennwort können Sie später eine Verbindung mit der VM herstellen. Sie können beispielsweise über Remotedesktop oder WinRM eine Verbindung herstellen, um mit dem System arbeiten zu können bzw. um dieses zu konfigurieren.

Standardmäßig weist Azure Ihrer VM eine öffentliche IP-Adresse zu. Sie können eine VM so konfigurieren, dass man über das Internet oder nur über das interne Netzwerk auf sie zugreifen kann.

Sie können sich auch das folgende Kurzvideo zu den Optionen für das Erstellen und Verwalten von VMs ansehen.

#### <a name="options-to-create-and-manage-vms"></a>Optionen für das Erstellen und Verwalten von virtuellen Computern

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

Wenn die VM bereit ist, erhalten Sie eine Meldung. Hier sehen Sie ein Beispiel.

```json
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1E-1B-3B",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "104.211.9.245",
  "resourceGroup": "myResourceGroup",
  "zones": ""
}
```

::: zone-end

::: zone pivot="linux-cloud"

## <a name="create-a-linux-vm"></a>Erstellen eines virtuellen Linux-Computers

Nachfolgend wird erläutert, wie Sie Ihre Linux-VM startbereit machen.

1. Führen Sie rechts auf dieser Seite in Cloud Shell den Befehl `az vm create` aus, um die VM zu erstellen. Der folgende Befehl erstellt die VM am Standort „USA, Osten“. Sie können diesen jedoch in einen beliebigen der oben aufgeführten Standorte ändern. Wir empfehlen allerdings, einen in Ihrer Nähe auszuwählen.

    ```azurecli
    az vm create \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --image UbuntuLTS \
      --location eastus \
      --size Standard_DS2_v2 \
      --generate-ssh-keys
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    Es dauert etwa zwei Minuten, bis Sie auf die VM zugreifen können. Vergleichen Sie das mit der Zeit, die es dauert, ein System für Ihr Rechenzentrum zu kaufen, es einzubauen und zu konfigurieren. Der Unterschied ist erheblich.

Solange Sie warten, können Sie sich den Befehl genauer ansehen, den Sie zuvor ausgeführt haben.

* Die VM hat den Namen **myVM**. Über diesen Namen kann die VM in Azure ermittelt werden. Außerdem handelt es sich um den internen Hostnamen der VM oder den Computernamen.
* Die Ressourcengruppe bzw. der logische Container der VM wird als **<rgn>[Sandbox-Ressourcengruppenname]</rgn>** bezeichnet.
* **UbuntuLTS** bezeichnet das Image der Ubuntu 16.04 LTS-VM.
* **Standard_DS2_v2** bezieht sich auf die Größe der VM. Diese Größe bietet zwei virtuelle CPUs und 7 GB Arbeitsspeicher.
* Über die Option `--generate-ssh-keys` wird ein SSH-Schlüsselpaar erstellt, mit dem Sie sich bei der VM anmelden können.

Standardmäßig weist Azure Ihrer VM eine öffentliche IP-Adresse zu. Sie können eine VM so konfigurieren, dass man über das Internet oder nur über das interne Netzwerk auf sie zugreifen kann.

Sie können sich auch das folgende Kurzvideo zu den Optionen für das Erstellen und Verwalten von VMs ansehen.

#### <a name="options-to-create-and-manage-vms"></a>Optionen für das Erstellen und Verwalten von virtuellen Computern

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

Wenn die VM bereit ist, erhalten Sie eine Meldung. Hier sehen Sie ein Beispiel.

```json
{
    "fqdns": "",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
    "location": "eastus",
    "macAddress": "00-0D-3A-1D-EB-02",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.4",
    "publicIpAddress": "137.135.110.210",
    "resourceGroup": "myResourceGroup",
    "zones": ""
}
```

::: zone-end

## <a name="summary"></a>Zusammenfassung

Es bedarf nur wenig, damit Sie innerhalb weniger Minuten in Azure eine VM erstellen können. Mit einigen der benötigten Aspekte wie der Größe einer VM und Firewallregeln sind Sie wahrscheinlich schon vertraut.

Als nächstes erfahren Sie, wie Sie einen Webserver auf Ihrer VM installieren und diesen konfigurieren, um eine Standardwebsite bereitzustellen.