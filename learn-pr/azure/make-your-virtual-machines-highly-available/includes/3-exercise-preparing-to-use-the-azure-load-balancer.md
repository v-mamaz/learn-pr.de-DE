In dieser Übung erstellen Sie einen Lastenausgleich, ein virtuelles Netzwerk und mehrere virtuelle Computer über das Azure-Portal.

Angenommen, Sie arbeiten bei der Woodgrove Bank – einem Start-Up-Unternehmen, das Onlinebankingdienste anbieten möchte. Aufgrund des hohen Wettbewerbsdrucks in dieser Branche müssen Sie eine Verfügbarkeit von 99,99 Prozent gewährleisten. Sie haben ermittelt, dass Sie eine Azure Load Balancer-Instanz mit einem Pool von drei virtuellen Computern benötigen, um dieses Ziel zu erreichen.

## <a name="create-a-public-load-balancer"></a>Erstellen eines öffentlichen Lastenausgleichs

1. Navigieren Sie in einem Browser zum [Azure-Portal](https://portal.azure.com/?azure-portal=true), und melden Sie sich bei Ihrem Konto an.

1. Klicken Sie auf der Seitenleiste auf **Ressource erstellen**, klicken Sie auf dem Blatt **Neu** auf **Netzwerk**, und klicken Sie anschließend auf **Lastenausgleich**.

1. Geben Sie auf dem Blatt „Lastenausgleich erstellen“ folgende Informationen ein, bzw. wählen Sie sie aus:
    - Name: **woodgrove-LB**
    - Typ: **Öffentlich**
    - SKU: **Basic**
    - Öffentliche IP-Adresse: Klicken Sie auf **Neu erstellen**, geben Sie **woodgrove-LB-ip** in das Textfeld ein, und behalten Sie die Zuweisung **Dynamisch** bei.
    - Ressourcengruppe: Klicken Sie auf **Neu erstellen**, und geben Sie **woodgrove-RG** in das Feld ein.
    - Standort: Wählen Sie eine Region in Ihrer Nähe aus.

1. Klicken Sie auf **Erstellen**.

1. Warten Sie, bis der Lastenausgleich bereitgestellt wurde, bevor Sie mit der Übung fortfahren.

## <a name="create-a-virtual-network"></a>Erstellen eines virtuellen Netzwerks

1. Klicken Sie im linken Menü auf **Ressource erstellen**, klicken Sie auf dem Blatt **Neu** auf **Netzwerk**, und klicken Sie anschließend auf **Virtuelles Netzwerk**.

1. Geben Sie auf dem Blatt **Virtuelles Netzwerk erstellen** folgende Informationen ein, bzw. wählen Sie sie aus:
    - Name: **woodgrove-VNET**
    - Adressraum: **172.20.0.0/16**
    - Ressourcengruppe: Klicken Sie auf **Vorhandene verwenden**, und wählen Sie **woodgrove-RG** aus.
    - Subnetz: **backendSubnet**
    - Adressraum: **172.20.0.0/24**
    - DDoS-Schutz: **Basic**
    - Dienstendpunkte: **Deaktiviert**

1. Klicken Sie auf **Erstellen**.

1. Warten Sie, bis das virtuelle Netzwerk bereitgestellt wurde, bevor Sie mit der Übung fortfahren.

## <a name="create-a-vm-template"></a>Erstellen einer VM-Vorlage

Definieren Sie zunächst die grundlegenden Informationen für den virtuellen Computer:

1. Klicken Sie im linken Menü des Azure-Portals auf **Virtuelle Computer** und anschließend auf **Virtuellen Computer erstellen**.

1. Klicken Sie auf dem Blatt „Compute“ im Abschnitt **Empfohlen** auf **Windows Server**.

1. Klicken Sie auf dem Blatt **Windows Server** auf **Windows Server 2016 Datacenter**.

1. Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.

1. Geben Sie auf dem Blatt **Grundlagen** im Feld **Name** den Namen **woodgrove-SVR01** ein.

1. Geben Sie in den Feldern **Benutzername** und **Kennwort** einen sicheren Namen und ein sicheres Kennwort für ein Administratorkonto auf diesem Server ein.

1. Wählen Sie im Feld **Abonnement** Ihr Azure-Abonnement aus.

1. Klicken Sie unter **Ressourcengruppe** auf **Vorhandene verwenden**, und wählen Sie in der Liste die Option **woodgrove-RG** aus.

1. Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.

1. Klicken Sie auf **OK**.

Wählen Sie eine Größe für den virtuellen Computer aus, und konfigurieren Sie die Einstellungen:

1. Wählen Sie auf dem Blatt **Größe auswählen** eine SKU vom Typ **Standard** aus (etwa **D2s_v3**), und klicken Sie auf **Auswählen**.

1. Klicken Sie auf dem Blatt **Einstellungen** auf **Verfügbarkeitsgruppe**.

1. Klicken Sie auf dem Blatt **Verfügbarkeitsgruppe ändern** auf **Neu erstellen**.

1. Geben Sie auf dem Blatt **Neu erstellen** im Feld **Name** den Namen **woodgrove-AS** ein, und klicken Sie anschließend auf **OK**.

1. Klicken Sie auf dem Blatt **Einstellungen** unter **Netzwerksicherheitsgruppe** auf **Erweitert** und anschließend auf **(neu) woodgrove-SVR01-nsg**.

1. Ändern Sie auf dem Blatt **Netzwerksicherheitsgruppe erstellen** den Namen im Feld **Name** in **woodgrove-NSG**, und klicken Sie anschließend auf **OK**.

1. Klicken Sie auf dem Blatt **Einstellungen** auf **OK**.

Speichern Sie die Einstellungen in einer Vorlage, um komfortabel mehrere virtuelle Computer bereitstellen zu können.

1. Klicken Sie auf dem Blatt **Erstellen** auf **Vorlage und Parameter herunterladen**.

1. Klicken Sie auf dem Blatt **Vorlage** auf **Zu Bibliothek hinzufügen**.

1. Geben Sie auf dem Blatt **Vorlage speichern** in den Feldern **Name** und **Beschreibung** jeweils **woodgrove-server-template** ein, und klicken Sie anschließend auf **Speichern**.

> [!NOTE]
> Wenn Sie nach dieser Vorlage suchen möchten, klicken Sie im linken Menü auf **Alle Dienste**, geben Sie **Vorlage** in das Filterfeld ein, und klicken Sie auf **Vorlagen (VORSCHAU)**.

## <a name="use-the-template-to-provision-the-first-vm"></a>Bereitstellen des ersten virtuellen Computers mit der Vorlage

1. Klicken Sie auf dem Blatt **Vorlage** auf **Bereitstellen**.

1. Klicken Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** unter **Ressourcengruppe** auf **Vorhandene verwenden**, und wählen Sie in der Liste die Option **woodgrove-RG** aus.

1. Geben Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** im Feld **Administratorkennwort** das gleiche Kennwort ein wie vorhin.

1. Aktivieren Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** das Kontrollkästchen **Ich stimme den oben genannten Geschäftsbedingungen zu**, und klicken Sie anschließend auf **Kaufen**. (Dabei fallen die normalen Azure-Computegebühren an. Diese orientieren sich am VM-Tarif.)

1. Warten Sie, bis der virtuelle Computer bereitgestellt wurde, bevor Sie mit der Übung fortfahren. So können Sie sich vor der Bereitstellung weiterer virtueller Computer vergewissern, dass die Vorlage ordnungsgemäß konfiguriert ist und alle dazugehörigen Ressourcen erstellt wurden.

## <a name="use-the-template-to-provision-two-additional-vms"></a>Bereitstellen zwei weiterer virtueller Computer mit der Vorlage

1. Klicken Sie im Azure-Portal auf dem Blatt **Vorlage** auf **Bereitstellen**.

1. Klicken Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** unter **Ressourcengruppe** auf **Vorhandene verwenden**, und wählen Sie in der Liste die Option **woodgrove-RG** aus.

1. Ändern Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** den Namen im Feld **Name des virtuellen Computers** in **woodgrove-SVR02**.

1. Ändern Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** den Namen im Feld **Network Interface Name** (Name der Netzwerkschnittstelle) in **woodgrovesvr02222**.

1. Geben Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** im Feld **Administratorkennwort** das gleiche Kennwort ein wie vorhin.

1. Ändern Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** den Namen im Feld **Öffentliche IP-Adresse** in **woodgrove-SVR02-ip**.

1. Aktivieren Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** das Kontrollkästchen **Ich stimme den oben genannten Geschäftsbedingungen zu**, und klicken Sie anschließend auf **Kaufen**. (Dabei fallen die normalen Azure-Computegebühren an. Diese orientieren sich am VM-Tarif.)

1. Wiederholen Sie die Schritte 1 bis 7 mit den folgenden Informationen:
    - Name des virtuellen Computers: **woodgrove-SVR03**
    - Name der Netzwerkschnittstelle: **woodgrovesvr03333**
    - Name der öffentliche IP-Adresse: **woodgrove-SVRr03-ip**

1. Warten Sie, bis die virtuellen Computer bereitgestellt wurden, bevor Sie mit der Übung fortfahren.

Sie verfügen nun über einen konfigurationsbereiten öffentlichen Lastenausgleich sowie über drei virtuelle Computer, die Sie mit diesem Lastenausgleich verwenden können.