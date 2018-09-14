In dieser Übung erstellen Sie ein virtuelles Netzwerk in Microsoft Azure. Anschließend erstellen Sie zwei virtuelle Computer und verwenden das virtuelle Netzwerk, um die virtuellen Computer miteinander und mit dem Internet zu verbinden.

Bevor Sie diese Einheit beginnen, müssen Sie zum Anmelden [Azure Cloud Shell](https://shell.azure.com) mit den Anmeldeinformationen Ihres Testabonnements. Wir werden Azure-Befehlszeilenschnittstelle über Azure Cloud Shell verwenden, um die Ressourcengruppen, virtuelle Netzwerke und virtuelle Computer zu erstellen.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

1. In der **Willkommen bei Azure Cloud Shell** Fenster, klicken Sie auf **Bash (Linux)**.

1. Klicken Sie im Fenster **You have no storage mounted** (Sie haben keinen Speicher bereitgestellt) auf **Speicher erstellen**.

1. Klicken Sie in der Azure PowerShell-Eingabeaufforderung Geben Sie den folgenden Code, und drücken Sie EINGABETASTE. Ersetzen Sie die `<myResourceGroup>` Wert mit einem aussagekräftigen Namen zu vereinfachen, zu beachten, wenn Sie später erstellten Ressourcen bereinigen. Sie verwenden diese Namen durch das Zurücksetzen dieser Anleitung.

    ```azurecli
    az group create --name <myResourceGroup> --location eastus
    ```

## <a name="create-a-virtual-network"></a>Erstellen eines virtuellen Netzwerks

1. Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE, um ein virtuelles Netzwerk zu erstellen. Ersetzen Sie die `<myVirtualNetwork>` Wert mit einem aussagekräftigen Namen zu erleichtern, denken Sie daran

    ```azurecli
    az network vnet create --name <myVirtualNetwork> --resource-group <myResourceGroup> --subnet-name default
    ```

## <a name="create-two-virtual-machines"></a>Erstellen von zwei virtuellen Computern

1. Um den ersten virtuellen Computer zu erstellen, führen Sie den folgenden Befehl an einer Windows-VM mit einer öffentlichen IP-Adresse zu erstellen, die über Port 3389 (Remotedesktop) zugänglich ist. Benennen Sie den virtuellen Computer `dataProcStage1`:

    ```azurecli
    az vm create --name dataProcStage1 --resource-group <myResourceGroup> --admin-username "DataAdmin" --image Win2016Datacenter
    ```

1. Geben Sie an den Eingabeaufforderungen Werte für Ihr Kennwort ein. Denken Sie daran, dieses Kennwort notieren, da Sie diese später, um Zugriff auf den Server benötigen.

1. Erstellen Sie nun den zweiten virtuellen Computer. Dieser virtuelle Computer müssen sich nicht auf eine öffentliche IP-Adresse aus. Führen Sie den folgenden Befehl zum Erstellen einer Windows-VM **ohne** eine öffentliche IP-Adresse, die mit einer leeren Zeichenfolge. Benennen Sie den virtuellen Computer `dataProcStage2`:

    ```azurecli
    az vm create -n dataProcStage2 -g <myResourceGroup> --public-ip-address "" --admin-username "DataAdmin" --image Win2016Datacenter
    ```

1. Nach Abschluss des Vorgangs enthält die Ausgabe des zweiten Befehls einen Wert für „publicIpAddress“.  

## <a name="connect-to-dataprocstage1-using-remote-desktop"></a>Herstellen einer Verbindung dataProcStage1 mit mithilfe von Remotedesktop

1. Drücken Sie auf Ihrem Clientcomputer die Windows-Taste, und geben Sie „RDP“ ein.

1. Sicherstellen, dass **Remotedesktopverbindung** app ausgewählt ist, und drücken Sie dann die EINGABETASTE.

1. In der **Remotedesktopverbindung** Dialogfeld die **Computer** Geben Sie den Wert der `dataProcStage1`die öffentliche IP-Adresse ein, und klicken Sie dann auf **Connect**.
    
    Anweisungen, um remote IP-Adresse zu erhalten, wenn Sie nicht geschrieben

1. Klicken **Sie im Dialogfeld mit der Frage, ob Sie dieser Remoteverbindung**vertrauen, auf **Verbinden**.

1. In der **Windows Security** Dialogfeld Geben Sie den Benutzernamen und Kennwort bei der Erstellung `dataProcStage1`. 

    Ändern Sie hier den Profilen

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **OK**.

1. Melden Sie sich bei dem Remotecomputer in Azure an.

1. Klicken Sie in der Meldung **Netzwerke** auf **Nein**.

1. Schließen Sie den Server-Manager.

1. Klicken Sie in der Remotesitzung mit der rechten Maustaste in der Windows-Taste, und klicken Sie auf **Eingabeaufforderung**.

1. Geben Sie im Eingabeaufforderungsfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE.

    ```cmd
    ping dataProcStage2 -4
    ```

1. Es sollen keine Antwort vom `dataProcStage2`. Dies ist, da standardmäßig Windows-Firewall auf ICMP-Antworten können `dataProcStage2`.

## <a name="connect-to-dataprocstage2-using-remote-desktop"></a>Herstellen einer Verbindung dataProcStage2 mit mithilfe von Remotedesktop

Konfigurieren Sie die Windows-Firewall auf `dataProcStage2` mithilfe einer neuen remote desktop Seesion. Allerdings müssen Sie keinen Zugriff auf `dataProcStage2` auf dem Desktop. Denken Sie daran, `dataProcStage2` verfügt nicht über eine öffentliche IP-Adresse. Sie werden mithilfe von Remotedesktop aus `dataProcStage1` für die Verbindung `dataProcStage2`.

1. Auf `dataProcStage1`, drücken Sie die Windows-Schlüssels und des Typs **RDP**. Wählen Sie die App **Remotedesktopverbindung** aus, und drücken Sie die EINGABETASTE.

1. In der **Computer** Feld `dataProcStage2`, und klicken Sie dann auf **Connect**. Basierend auf den Standard-Netzwerkkonfiguration`dataProcStage1` kann zum Auflösen der Adresse für `dataProcStage2` mit den Namen des Computers.

1. Klicken **Sie im Dialogfeld mit der Frage, ob Sie dieser Remoteverbindung**vertrauen, auf **Verbinden**.

1. In der **Windows Security** Dialogfeld Geben Sie den Benutzernamen und Kennwort bei der Erstellung `dataProcStage2`.

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **OK**. Melden Sie sich nun bei dem Remotecomputer in Azure an.

1. Klicken Sie in der Meldung **Netzwerke** auf **Nein**.

1. Schließen Sie den Server-Manager.

1. Auf `dataProcStage2`, drücken Sie Windows, den Typ des **Firewall**, und drücken Sie EINGABETASTE. Die Konsole **Windows-Firewall mit erweiterter Sicherheit** wird angezeigt.

1. Klicken Sie im linken Bereich auf **Eingehende Regeln**.

1. Im rechten Bereich einen Bildlauf nach unten, und mit der rechten Maustaste **Datei- und Druckerfreigabe (Echoanforderung - ICMPv4 eingehend)**, und klicken Sie dann auf **Regel aktivieren**.

1. Wechseln Sie zurück zu den `dataProcStage1` -Konsole und in das Eingabeaufforderungsfenster, geben Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE.

    ```cmd
    ping dataProcStage2 -4
    ```

1. `dataProcStage2` antwortet mit vier Antworten, die Konnektivität zwischen den beiden virtuellen Computern zu veranschaulichen.

## <a name="summary"></a>Zusammenfassung

Sie haben erfolgreich ein erstelltes virtuelles Netzwerk, zwei virtuelle Computer, die mit diesem virtuellen Netzwerk verbunden sind, mit einem virtuellen Computer verbunden und gezeigt über eine Netzwerkverbindung mit dem anderen virtuellen Computer im gleichen virtuellen Netzwerk erstellt. Azure Virtual Network können Ressourcen im Azure-Netzwerk verbinden. Diese Ressourcen müssen sich jedoch innerhalb der gleichen Ressourcengruppe und innerhalb des gleichen Abonnements befinden. Als Nächstes untersuchen VPN-Gateways, wir die Verbindung der virtuelles Netzwerk in verschiedenen Ressourcengruppen, Abonnements und sogar geografische Regionen zu ermöglichen.
