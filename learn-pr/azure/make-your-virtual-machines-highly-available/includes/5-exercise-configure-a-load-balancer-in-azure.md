Sie haben bereits wichtigsten Ressourcen für Ihre Architektur online Bank erstellt. In dieser Übung führen Sie das Setup durch Konfigurieren von Sicherheitseinstellungen, ein Back-End-Adresspool, Integritätsregeln für Tests und Regeln des Lastenausgleichs. Nachdem Setup abgeschlossen ist, testen Sie den Load Balancer durch Entfernen eines virtuellen Computers aus dem Pool, und überprüfen, dass Clientanforderungen an diesen virtuellen Computer nicht mehr gesendet werden.

## <a name="inbound-rules"></a>Regeln für eingehenden Datenverkehr

Erstellen Sie eine Sicherheitsregel für eingehenden Datenverkehr zu für eingehende HTTP-Verbindungen, die Verwendung von Port 80 an.

1. In der [Azure-Portal](https://portal.azure.com/?azure-portal=true), klicken Sie im linken Menü auf **alle Ressourcen**. Klicken Sie in der Ressourcenliste auf **Woodgrove-NSG**.

1. Auf der **Woodgrove-NSG** Blatt unter **Einstellungen**, klicken Sie auf **Eingangssicherheitsregeln**, und klicken Sie dann auf **hinzufügen**.

1. Auf der **eingangssicherheitsregel hinzufügen** auf dem Blatt, geben Sie die folgende Informationen:
    - Quelle: **Diensttag**
    - Quelldiensttag: **Internet**
    - Quellportbereiche: **\***
    - Ziel: **alle**
    - Zielportbereich: **80**
    - Protokoll: **TCP**
    - Aktion: **zulassen**
    - Priorität: **100**
    - Name: **Woodgrove-HTTP-Regel**

1. Klicken Sie auf **Hinzufügen**.

Erstellen Sie eine Sicherheitsregel für eingehenden Datenverkehr um, die Verwendung von Port 3389 eingehende RDP-Verbindungen zu ermöglichen.

1. Auf der **Woodgrove-NSG - Sicherheitsregeln für eingehende** auf dem Blatt klicken Sie auf **hinzufügen**.

1. Auf der **eingangssicherheitsregel hinzufügen** auf dem Blatt, geben Sie die folgende Informationen:
    - Quelle: **Diensttag**
    - Quelldiensttag: **Internet**
    - Quellportbereiche: **\***
    - Ziel: **alle**
    - Zielportbereich: **3389**
    - Protokoll: **TCP**
    - Aktion: **zulassen**
    - Priorität: **200**
    - Name: **Woodgrove-RDP-Regel**

1. Klicken Sie auf **Hinzufügen**.

## <a name="prepare-a-script-to-install-and-configure-iis-on-the-vms"></a>Vorbereiten eines Skripts zum Installieren und Konfigurieren von IIS auf den virtuellen Computern

1. Kopieren Sie die folgenden PowerShell-Befehle in einem Text-Editor ein:

    ```powershell
    # install IIS server role
    Install-WindowsFeature -name Web-Server -IncludeManagementTools

    # remove default htm file
    remove-item  C:\inetpub\wwwroot\iisstart.htm

    # Add a new htm file that displays server name
    Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Web page from <b>" + $env:computername + "</b>")
    ```

1. Speichern Sie die Datei lokal **ConfigureIIS.ps1**.

### <a name="install-and-configure-iis-on-vms"></a>Installieren und Konfigurieren von IIS auf virtuellen Computern

1. Klicken Sie im Azure-Portal im linken Menü auf **alle Ressourcen**. Klicken Sie in der Ressourcenliste auf **Woodgrove-SVR01**.

1. Klicken Sie auf der Seite "Übersicht" auf **Connect**.

1. In der **Herstellen einer Verbindung mit dem virtuellen Computer** auf dem Blatt klicken Sie auf **RDP-Datei herunterladen**. Klicken Sie im Popupfenster auf **öffnen**.

1. Klicken Sie im Fenster **Remotedesktopverbindung** auf **Verbinden**.

1. In der **Windows-Sicherheit** Dialogfeld klicken Sie auf **Weitere Optionen**, und klicken Sie dann auf **verwenden ein anderes Konto**.

1. In der **Windows Security** Dialogfeld Geben Sie die Anmeldeinformationen, die Sie verwendet werden, wenn Sie die virtuellen Computer bereitgestellt, und klicken Sie dann auf **OK**.

1. Wenn Sie erhalten eine **Remotedesktopverbindung** Warnung Zertifikat, klicken Sie auf **Ja**.

1. Öffnen Sie auf dem lokalen Computer den Ordner mit dem Skript aus.

1. Kopie **ConfigureIIS.ps1** in die Zwischenablage.

1. Wechseln Sie zu der RDP-Sitzung. Klicken Sie dann öffnen Sie Windows Explorer, und fügen Sie **ConfigureIIS.ps1** zu **C:\\**.

1. Klicken Sie in der RDP-Sitzung auf **starten**, und öffnen Sie dann **Windows PowerShell**.

1. Geben Sie an der PowerShell-Eingabeaufforderung den folgenden Befehl aus, und drücken Sie dann die **EINGABETASTE:**

    ```powershell
    cd \
    ```

1. Geben Sie an der PowerShell-Eingabeaufforderung den folgenden Befehl aus, und drücken Sie dann die **EINGABETASTE:**

    ```powershell
    .\ConfigureIIS.ps1
    ```

1. Schließen Sie die RDP-Verbindung.

1. Wiederholen Sie die Schritte 1 bis 13 für **Woodgrove-SVR02** und **Woodgrove-SVR03**.

## <a name="create-a-back-end-address-pool"></a>Erstellen eines Back-End-Adresspools

Als Nächstes verwenden Sie das Portal, um einen Back-End-Adresspool für den öffentlichen Load Balancer zu erstellen.

1. Klicken Sie im Azure-Portal im linken Menü auf **alle Ressourcen**. Klicken Sie in der Ressourcenliste auf **Woodgrove-LB-**.

1. Auf der **Woodgrove-LB-** Blatt unter **Einstellungen**, klicken Sie auf **Back-End-Pools**, und klicken Sie dann auf **hinzufügen**.

1. Auf der **Back-End-Pool hinzufügen** auf dem Blatt, fügen Sie die folgenden Informationen hinzu:
    - Name: **Woodgrove-BEP**
    - Zugeordnete: Wählen Sie **verfügbarkeitsgruppe**
    - Verfügbarkeitsgruppe: **Woodgrove-AS**

1. Klicken Sie auf **Zielnetzwerk-IP-Konfiguration hinzufügen**. Klicken Sie auf die **virtuellen Zielcomputer** Liste **Woodgrove-SVR01**. In der **Netzwerk-IP-Konfiguration** wählen Sie die VM IP-Adresspool.

1. Klicken Sie auf **Zielnetzwerk-IP-Konfiguration hinzufügen**. Klicken Sie auf die **virtuellen Zielcomputer** Liste **Woodgrove-SVR02**, und klicken Sie in der **Netzwerk-IP-Konfiguration** wählen Sie die VM IP-Adresspool.

1. Klicken Sie auf **Zielnetzwerk-IP-Konfiguration hinzufügen**. Klicken Sie auf die **virtuellen Zielcomputer** Liste **Woodgrove-SVR03**, und klicken Sie in der **Netzwerk-IP-Konfiguration** wählen Sie die VM IP-Adresspool.

1. Auf der **Back-End-Pool hinzufügen** auf dem Blatt klicken Sie auf **OK**.

1. Warten Sie, bis die Lastenausgleichsmodul-Konfiguration vor dem Fortfahren mit der Übung aktualisiert wurde.

## <a name="create-a-health-probe-for-the-load-balancer"></a>Erstellen eines Integritätstests für den Load balancer

Fügen Sie einen Integritätstest für HTTP über Port 80.

1. Auf der **Woodgrovelb** Blatt unter **Einstellungen**, klicken Sie auf **Integritätstests**, und klicken Sie dann auf **hinzufügen**.

1. Auf der **Integritätstest hinzufügen** auf dem Blatt, fügen Sie die folgenden Informationen hinzu:
    - Name: **woodgrove-HP**
    - Protokoll: **HTTP**
    - Port: **80**
    - Pfad: **/**
    - Intervall: **15**
    - Fehlerschwellenwert: **2**

1. Auf der **Integritätstest hinzufügen** auf dem Blatt klicken Sie auf **OK**.

1. Warten Sie, bis die Lastenausgleichsmodul-Konfiguration vor dem Fortfahren mit der Übung aktualisiert wurde.

## <a name="create-a-load-balancer-rule"></a>Erstellen einer Load Balancer-Regel

Abschließend erstellen Sie eine lastenausgleichsregel für den HTTP über Port 80, die den Integritätstest der Back-End-Adresspool zuordnet.

1. Auf der **Woodgrove-LB-** Blatt unter **Einstellungen**, klicken Sie auf **Lastenausgleichsregeln**, und klicken Sie dann auf **hinzufügen**.

1. Auf der **lastenausgleichsregel hinzufügen** Blatt in der **Namen** geben **Woodgrove-HTTP-LBRule**. Klicken Sie dann stellen Sie sicher, dass die folgende Informationen automatisch eingegeben wurde:
    - IP-Version: **IPv4**
    - Frontend IP-Adresse: **LoadBalancerFrontEnd**
    - Protokoll: **TCP**
    - Port: **80**
    - Back-End-Port: **80**
    - Back-End-Pool: **Woodgrove-BEP**
    - Integritätstest: **Woodgrove-HP**
    - Sitzungspersistenz: **keine**
    - Das inaktiv-Timeout: **4 Minuten**
    - Floating-IP: **deaktiviert**

1. Auf der **lastenausgleichsregel hinzufügen** auf dem Blatt klicken Sie auf **OK**.

1. Warten Sie, bis die Lastenausgleichsmodul-Konfiguration vor dem Fortfahren mit der Übung aktualisiert wurde.

## <a name="test-the-load-balancer"></a>Testen des Lastenausgleichs

1. Klicken Sie im Azure-Portal im linken Menü auf **alle Ressourcen**, und klicken Sie dann in der Ressourcenliste auf **Woodgrove-LB-IP-**.

1. Auf der **Übersicht über die** Blatt die **IP-Adresse**, und klicken Sie dann auf die **Kopie** Schaltfläche.

1. Fügen Sie in einer neuen Browserregisterkarte die IP-Adresse in die Adressleiste Ihres Browsers ein. Notieren Sie den Namen des Servers ein, und lassen Sie diese Registerkarte geöffnet.

1. Klicken Sie im Azure-Portal im linken Menü auf **alle Ressourcen**. Klicken Sie auf dem Server, dem Sie oben notiert haben. Klicken Sie dann in der Ressourcenliste.

1. Auf der **Übersicht** auf dem Blatt klicken Sie auf **beenden**, und klicken Sie dann auf **Ja**.

1. Warten Sie, bis der virtuelle Computer beendet wurde, und wechseln Sie zur Registerkarte "", die Sie in Schritt 3 angezeigt. Aktualisieren Sie die Seite.

1. Der Load Balancer sendet nun Ihre HTTP-Anforderung an eine Ihrer anderen VMs.

In dieser Übung haben Sie die Bereitstellung von Ihrem Back-End-VMs und den Load Balancer.
