Als eine Technologie, die professionelle haben Sie wahrscheinlich Fachwissen in einem bestimmten Bereich. Vielleicht sind Sie ein Speicheradministrator oder Experten Virtualisierung oder vielleicht konzentrieren Sie sich auf die neueste Sicherheitsmaßnahmen. Wenn Sie ein Schüler/Student sind, können Sie weiterhin untersuchen Sie am meisten interessieren.

::: zone pivot="windows-cloud"

Unabhängig von Ihrer Rolle die meisten Benutzer mit der Cloud beginnen durch Erstellen eines virtuellen Computers. Hier müssen Sie einen virtuellen Computer unter Windows Server 2016 angezeigt.

::: zone-end

::: zone pivot="linux-cloud"

Unabhängig von Ihrer Rolle die meisten Benutzer mit der Cloud beginnen durch Erstellen eines virtuellen Computers. Hier müssen Sie einen virtuellen Computer unter Ubuntu 16.04 angezeigt.

::: zone-end

Es gibt viele Möglichkeiten zum Erstellen eines virtuellen Computers in Azure. Hier müssen Sie eine Windows oder Linux-VM mit einem interaktiven Terminal aufgerufen von Cloud Shell angezeigt. Wenn Sie über das Terminal auf täglicher Basis arbeiten, wissen Sie, dass dies oft am schnellsten erledigen ist.

::: zone pivot="windows-cloud"

> [!TIP]
> Bevorzugen Linux oder etwas Neues ausprobieren möchten? Wählen Sie **Linux** zwischen dem oberen Rand dieser Seite können Sie einen virtuellen Linux-Computer ausführen.

::: zone-end

::: zone pivot="linux-cloud"

> [!TIP]
> Bevorzugen Windows, oder etwas Neues ausprobieren möchten? Wählen Sie **Windows** zwischen dem oberen Rand dieser Seite können Sie einen Windows Server-Computer ausführen.

::: zone-end

Lassen Sie uns einige Grundbegriffe überprüfen, und erhalten Sie Ihren ersten virtuellen Computer einrichten und ausführen.

## <a name="what-is-a-virtual-machine"></a>Was ist ein virtueller Computer?

Einen virtuellen Computer oder virtuellen Computer ist eine Softwareemulation eines physischen Computers. Da VMs vorhanden, als die Software, Dutzende, Hunderte sind oder sogar Tausende von virtuellen Azure-Computer innerhalb weniger Minuten generiert werden können, gelöscht klicken Sie dann, wenn Sie sie nicht mehr benötigen. Mit geringen Kosten und minutengenauer Abrechnung Zahlen Sie nur für die Compute-Ressourcen, die Sie, solange Sie sie verwenden verwenden. Darüber hinaus stehen viele Möglichkeiten zur Konfiguration der virtuellen Computer Ihre Bedürfnisse angepasst.

::: zone pivot="windows-cloud"

Eine Momentaufnahme von einer laufenden virtuellen Maschine heißt ein _Image_. Azure bietet Images für Windows und verschiedene Arten von Linux. Sie können auch eigene vorkonfigurierten Images aus, um Bereitstellungen schneller wechseln Sie erstellen. Hier werden Sie von einer Windows Server 2016-VM, von Microsoft bereitgestellten angezeigt.

::: zone-end

::: zone pivot="linux-cloud"

Eine Momentaufnahme von einer laufenden virtuellen Maschine heißt ein _Image_. Azure bietet Images für Windows und verschiedene Arten von Linux. Sie können auch eigene vorkonfigurierten Images aus, um Bereitstellungen schneller wechseln Sie erstellen. Hier müssen Sie einen virtuellen Ubuntu 16.04-Computer von Canonical bereitgestellten angezeigt.

::: zone-end

## <a name="what-defines-a-virtual-machine-on-azure"></a>Definiert einen virtuellen Computer in Azure?

Ein virtuellen Computer wird durch eine Reihe von Faktoren wie die Größe und Position definiert. Bevor Sie Ihre virtuellen Computer bereitstellen, lassen Sie uns kurz welcher Aufwand erforderlich ist.

:::row:::
    :::column:::
        **Größe**
    :::column-end:::
    ::: Spaltenweite = "3"::: ein VM _Größe_ definiert die prozessorgeschwindigkeit, die Menge an Arbeitsspeicher, wie viel Speicher und erwartete Netzwerkbandbreite. Einige Größen enthalten auch spezielle Hardware wie z. B. GPUs für hohe Grafikrendering und intensive videobearbeitung.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **Region**
    :::column-end:::
    ::: Spaltenweite = "3"::: Azure setzt sich aus der ganzen Welt verteilte Rechenzentren. Ein _Region_ ist ein Satz von Azure-Rechenzentren in einem benannten geografischen Standort. Jede Azure-Ressource, einschließlich Virtual Machines, wird eine Region zugewiesen. USA, Osten "und" Europa, Norden sind Beispiele für Bereiche auf.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **Netzwerk**
    :::column-end:::
    ::: Spaltenweite = "3"::: ein _virtuelles Netzwerk_ ein logisch isolierten Netzwerks in Azure ist. Jeder virtuelle Computer in Azure ist mit einem virtuellen Netzwerk verknüpft. Azure bietet Firewalls auf Cloud für Ihre virtuellen Netzwerke _network Security Groups,_.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **Ressourcengruppen**
    :::column-end:::
    ::: Spaltenweite = "3"::: virtuellen Computern und anderen Cloudressourcen sind in logischen Containern Namens gruppiert _Ressourcengruppen_. Gruppen werden in der Regel verwendet, um Gruppen von Ressourcen zu organisieren, die zusammen als Teil einer Anwendung oder einem Dienst bereitgestellt werden. Sie verweisen auf eine Ressourcengruppe mit dem Namen.
    :::column-end:::
:::row-end:::

## <a name="what-is-azure-cloud-shell"></a>Was ist Azure Cloud Shell?

Azure Cloud Shell ist eine browserbasierte befehlszeilenumgebung für die Verwaltung und Entwicklung von Azure-Ressourcen. Stellen Sie sich Cloud Shell als eine interaktive Konsole, die Sie in der Cloud ausführen.

Cloudshell bietet zwei Benutzeroberflächen zur Auswahl: Bash und PowerShell. Beide enthalten den Zugriff auf die Azure-Befehlszeilenschnittstelle, die Befehlszeilenschnittstelle für Azure.

Alle Azure-Verwaltungsschnittstelle, einschließlich der Azure-Portal, Azure-Befehlszeilenschnittstelle und Azure PowerShell, können alle Arten von virtuellen Computer zu verwalten. Zu Lernzwecken verwenden hier Sie die Azure-Befehlszeilenschnittstelle zum Erstellen und Verwalten einer Windows oder Linux-VM.

::: zone pivot="windows-cloud"

## <a name="create-a-windows-vm"></a>Erstellen einer Windows-VM

[!include[](../../../includes/azure-sandbox-activate.md)]

Wir rufen Ihre Windows-VM ausgeführt.

<!--

TODO: Omitted for sandbox. Possibly re-insert later for non-sandbox workflow.

1. From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```
-->

1. Führen Sie in Cloud Shell auf der rechten Seite der Seite, die `az vm create` Befehl aus, um den virtuellen Computer erstellen. Es wird empfohlen, dass Sie das Kennwort an, die Sie später problemlos wiederfinden unten ändern.

      > [!NOTE]
    > Wählen Sie ein Kennwort, das über mindestens 8 Zeichen mit einer Kombination aus Groß- und Kleinbuchstaben, Zahlen und Symbole enthält.

    ```azurecli
    az vm create \
      --name myWindowsVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --image Win2016Datacenter \
      --size Standard_DS2_v2 \
      --admin-username azureuser \
      --admin-password "Password1234&"
    ```

    > [!TIP]
    > Sie können die **Kopie** , um jeden Befehl zu kopieren. Um es einzufügen, klicken Sie mit der rechten Maustaste auf die neue Zeile in der Cloud Shell-Fenster, und wählen Sie **einfügen**.

    Ihres virtuellen Computers dauert vier bis fünf Minuten kommen. Vergleichen Sie, die mit der Zeit, die es dauert, erwerben, einsetzen und konfigurieren ein System in Ihrem Rechenzentrum. Ein Unterschied!

Während Sie warten, sehen Sie sich an den Befehl aus, den Sie gerade ausgeführt haben.

* Die VM heißt **"mywindowsvm"**. Dieser Name identifiziert die virtuellen Computer in Azure. Es wird auch der interne Hostname des virtuellen Computers oder das Name des Computers.
* Die Ressourcengruppe und des virtuellen Computers logischer Container, den Namen  **<rgn>[Ressourcengruppennamen Sandkasten]</rgn>**.
* **Win2016Datacenter** gibt an, das Windows Server 2016-VM-Image.
* **"Standard_ds2_v2"** bezieht sich auf die Größe des virtuellen Computers. Diese Größe verfügt über zwei virtuelle CPUs und 7 GB Arbeitsspeicher.
* Benutzername und Kennwort können Sie später eine Verbindung mit Ihrem virtuellen Computer herzustellen. Beispielsweise können Sie eine Verbindung herstellen über Remotedesktop oder WinRM zum Arbeiten mit und das System konfigurieren.

Standardmäßig weist Azure eine öffentliche IP-Adresse Ihres virtuellen Computers. Sie können konfigurieren, dass eine VM, die aus dem Internet oder nur aus dem internen Netzwerk zugegriffen werden.

Sie können auch zu einigen der Optionen in diesem kurzen Video Auschecken, die Sie zum Erstellen und Verwalten von virtuellen Computern haben.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

Wenn der virtuelle Computer bereit ist, sehen Sie Informationen dazu. Hier sehen Sie ein Beispiel.

```console
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myWindowsVM",
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

[!include[](../../../includes/azure-sandbox-activate.md)]

Lassen Sie uns loslegen Ihrer Linux-VM.

<!--

TODO: Omitted for sandbox. Possibly re-insert later for non-sandbox workflow.
 
1. From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```
-->

1. Führen Sie in Cloud Shell auf der rechten Seite der Seite, die `az vm create` Befehl aus, um den virtuellen Computer erstellen.

    ```azurecli
    az vm create \
      --name myLinuxVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --generate-ssh-keys
    ```

    > [!TIP]
    > Sie können die **Kopie** , um jeden Befehl zu kopieren. Um es einzufügen, klicken Sie mit der rechten Maustaste auf die neue Zeile in der Cloud Shell-Fenster, und wählen Sie **einfügen**.

    Ihr virtueller Computer dauert ungefähr zwei Minuten, aktiviert wird. Vergleichen Sie, die mit der Zeit, die es dauert, erwerben, einsetzen und konfigurieren ein System in Ihrem Rechenzentrum. Ein Unterschied!

Während Sie warten, sehen Sie sich an den Befehl aus, den Sie gerade ausgeführt haben.

* Die VM heißt **MyLinuxVM**. Dieser Name identifiziert die virtuellen Computer in Azure. Es wird auch der interne Hostname des virtuellen Computers oder das Name des Computers.
* Die Ressourcengruppe und des virtuellen Computers logischer Container, den Namen  **<rgn>[Ressourcengruppennamen Sandkasten]</rgn>**.
* **UbuntuLTS** gibt das Ubuntu 16.04 LTS-VM-Image.
* **"Standard_ds2_v2"** bezieht sich auf die Größe des virtuellen Computers. Diese Größe verfügt über zwei virtuelle CPUs und 7 GB Arbeitsspeicher.
* Die `--generate-ssh-keys` Option erstellt eine SSH-Schlüsselpaar, damit Sie mit dem virtuellen Computer anmelden können.

Standardmäßig weist Azure eine öffentliche IP-Adresse Ihres virtuellen Computers. Sie können konfigurieren, dass eine VM, die aus dem Internet oder nur aus dem internen Netzwerk zugegriffen werden.

Sie können auch zu einigen der Optionen in diesem kurzen Video Auschecken, die Sie zum Erstellen und Verwalten von virtuellen Computern haben.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

Wenn der virtuelle Computer bereit ist, sehen Sie Informationen dazu. Hier sehen Sie ein Beispiel.

```console
{
    "fqdns": "",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myLinuxVM",
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

Mit nur wenigen Konzepte in der Tasche können Sie einen virtuellen Computer in Azure in nur wenigen Minuten einrichten. Viele dieser Konzepte, z. B. eine VM Größe und Firewall-Regeln, sind Ihnen wahrscheinlich vertraut, Ihnen bereits.

Als Nächstes werden Sie einen Webserver auf Ihrem virtuellen Computer installieren und konfigurieren Ihrem Webserver eine einfache Website bereitstellen.