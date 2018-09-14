In dieser Übung erstellen Sie einen Load Balancer, ein virtuelles Netzwerk und mehrere virtuelle Computer im Azure-Portal verwenden.

Nehmen wir an, dass Sie bei der Woodgrove Bank ein Startupunternehmen arbeiten, die zu online-Banking Services zu starten. Diesem Sektor ist stark umkämpft, daher Sie von mindestens 99,99 % Verfügbarkeit garantiert müssen. Sie haben festgestellt, dass Azure Load Balancer einen Pool von drei virtuellen Maschinen auf dieses Ziel erfüllt.

## <a name="create-a-public-load-balancer"></a>Erstellen eines öffentlichen Lastenausgleichs

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

1. Klicken Sie in der Randleiste **erstellen Sie eine Ressource**. Klicken Sie auf die **neu** auf dem Blatt klicken Sie auf **Networking**, und klicken Sie dann auf **Load Balancer**.

1. In der **Load Balancer erstellen** Blatt eingeben, oder wählen Sie die folgende Informationen:
    - Name: **Woodgrove-LB-**
    - Typ: **öffentliche**
    - SKU: **Basic**
    - Öffentliche IP-Adresse: Wählen Sie **neu erstellen**. Geben Sie in das Textfeld ein **Woodgrove-LB-IP-**. Übernehmen Sie die Zuweisung als **dynamische**.
    - Ressourcengruppe: Wählen Sie **vorhandene** , und wählen Sie <rgn>[Ressourcengruppennamen Sandkasten]</rgn>.
    - Speicherort: Wählen Sie eine Region in Ihrer Nähe.

1. Klicken Sie auf **Erstellen**.

1. Warten Sie, bis der Load Balancer bereitgestellt hat, bevor Sie mit der Übung fortfahren.

## <a name="create-a-virtual-network"></a>Erstellen eines virtuellen Netzwerks

1. Klicken Sie im linken Menü auf **erstellen Sie eine Ressource**. In der **neu** auf dem Blatt klicken Sie auf **Networking**, und klicken Sie dann auf **virtuelles Netzwerk**.

1. In der **virtuelles Netzwerk erstellen** Blatt eingeben, oder wählen Sie die folgende Informationen:
    - Name: **Woodgrove-VNET**
    - Adressraum: **172.20.0.0/16**
    - Ressourcengruppe: Wählen Sie **vorhandene**, und wählen Sie dann <rgn>[Ressourcengruppennamen Sandkasten]</rgn>.
    - Subnet: **backendSubnet**
    - Adressraum: **172.20.0.0/24**
    - DDoS-Schutz: **Basic**
    - Dienstendpunkte: **deaktiviert**

1. Klicken Sie auf **Erstellen**.

1. Warten Sie, bis das virtuelle Netzwerk bereitgestellt wurde, bevor Sie mit der Übung fortfahren.

## <a name="create-a-vm-template"></a>Erstellen Sie eine VM-Vorlage

Definieren Sie zunächst die grundlegenden Informationen über den virtuellen Computer:

1. Klicken Sie im Azure-Portal im linken Menü auf **VMs**, und klicken Sie dann auf **erstellen virtuellen Computer**.

1. Auf der **Compute** Blatt in der **empfohlen** auf **Windows Server**.

1. Klicken Sie auf dem Blatt **Windows Server** auf **Windows Server 2016 Datacenter**.

1. Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.

1. In der **Grundlagen** Blatt in der **Namen** geben **Woodgrove-SVR01**.

1. In der **Benutzername** und **Kennwortfelder**, geben Sie einen sicheren Namen und ein Kennwort für ein Administratorkonto auf dem Server.

1. Wählen Sie im Feld **Abonnement** Ihr Azure-Abonnement aus.

1. Klicken Sie unter **Ressourcengruppe**Option **vorhandene**. Wählen Sie in der Liste **Woodgrove-RG**.

1. Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.

1. Klicken Sie auf **OK**.

Wählen Sie eine Größe für den virtuellen Computer aus, und klicken Sie dann konfigurieren Sie die Einstellungen zu:

1. Auf der **wählen Sie eine Größe** Blatt eine **Standard** SKU, z. B. **D2s_v3**. Klicken Sie dann auf **Auswählen**.

1. Auf der **Einstellungen** auf dem Blatt klicken Sie auf **verfügbarkeitsgruppe**.

1. Auf der **Ändern der verfügbarkeitsgruppe** auf dem Blatt klicken Sie auf **neu erstellen**.

1. Auf der **neu erstellen** Blatt in der **Namen** geben **Woodgrove-AS**, und klicken Sie dann auf **OK**.

1. Auf der **Einstellungen** Blatt unter **Netzwerksicherheitsgruppe**, klicken Sie auf **erweitert**, und klicken Sie dann auf **(neu) Woodgrove-SVR01-Nsg**.

1. Auf der **Netzwerksicherheitsgruppe erstellen** Blatt in der **Namen** ändern den Namen in **Woodgrove-NSG**, und klicken Sie dann auf **OK**.

1. Auf der **Einstellungen** auf dem Blatt klicken Sie auf **OK**.

Speichern Sie die Einstellungen an der Vorlage, damit Sie problemlos auf mehrere virtuelle Computer bereitstellen können.

1. Auf der **erstellen** auf dem Blatt klicken Sie auf **Vorlage und Parameter herunterladen**.

1. Auf der **Vorlage** auf dem Blatt klicken Sie auf **Hinzufügen zur Bibliothek**.

1. Auf der **speichern Vorlage** Blatt in der **Namen** und **Beschreibung** Felder, geben **Woodgrove-Server-Vorlage**. Klicken Sie anschließend auf **Speichern**.

> [!NOTE]
> Wenn Sie diese Vorlage suchen möchten, klicken Sie auf **alle Dienste** Geben Sie im linken Menü **Vorlage** im Feld "Filter", und klicken Sie dann auf **Vorlagen (Vorschau)**.

## <a name="use-the-template-to-provision-the-first-vm"></a>Verwenden Sie die Vorlage, um den ersten virtuellen Computer bereitzustellen.

1. Auf der **Vorlage** auf dem Blatt klicken Sie auf **bereitstellen**.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt unter **Ressourcengruppe**Option **vorhandene**. Wählen Sie in der Liste **Woodgrove-RG**.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt in der **Administratorkennwort** geben das gleiche Kennwort, das Sie zuvor verwendet haben.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt die **ich stimme den Bestimmungen und Bedingungen** , und klicken Sie dann auf **Kauf** (der Preis ist der regulären Azure Compute anfallen, die hängt von der VM-Tarif).

1. Warten Sie die Bereitstellung des virtuellen Computers ab, bevor Sie mit der Übung fortfahren. Dies ist daher können Sie sicher, dass die Vorlage ordnungsgemäß konfiguriert ist, bevor Sie ihn verwenden, um zusätzliche virtuelle Computer bereitzustellen und alle zugehörigen Ressourcen erstellt wurden sein.

## <a name="use-the-template-to-provision-two-additional-vms"></a>Verwenden Sie die Vorlage zum Bereitstellen von zwei zusätzliche virtuelle Computer

1. Im Azure-Portal auf der **Vorlage** auf dem Blatt klicken Sie auf **bereitstellen**.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt unter **Ressourcengruppe**Option **vorhandene**. Wählen Sie in der Liste **Woodgrove-RG**.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt in der **Name des virtuellen Computers** ändern den Namen in **Woodgrove-SVR02**.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt in der **Netzwerkschnittstellenname** ändern den Namen in **woodgrovesvr02222**.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt in der **Administratorkennwort** geben das gleiche Kennwort, das Sie zuvor verwendet haben.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt in der **Name der öffentlichen Ip-Adresse** ändern den Namen in **Woodgrove-SVR02-IP-**.

1. Auf der **benutzerdefinierte Bereitstellung** Blatt die **ich stimme den Bestimmungen und Bedingungen** , und klicken Sie dann auf **Kauf** (der Preis ist der regulären Azure Compute anfallen, die hängt von der VM-Tarif).

1. Wiederholen Sie die Schritte 1 bis 7, mit den folgenden Informationen:
    - Name des virtuellen Computers: **Woodgrove-SVR03**
    - Netzwerkschnittstellenname: **woodgrovesvr03333**
    - Name der öffentlichen IP-Adresse: **Woodgrove-SVRr03-Ip**

1. Warten Sie, bis die virtuellen Computer bereitgestellt haben, bevor Sie mit der Übung fortfahren.

Sie verfügen nun über einen öffentlichen Load Balancers bereit zur Konfiguration und drei virtuelle Computer bereit, mit diesen Load Balancer verwenden.