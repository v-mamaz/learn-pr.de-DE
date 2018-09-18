In dieser Übung erstellen Sie in Microsoft Azure ein virtuelles Netzwerk. Anschließend erstellen Sie zwei virtuelle Computer und verwenden das virtuelle Netzwerk, um die virtuellen Computer miteinander und mit dem Internet zu verbinden.

Vor Beginn dieser Einheit müssen Sie sich mit den Anmeldeinformationen Ihres Testabonnements bei [Azure Cloud Shell](https://shell.azure.com) anmelden. Wir verwenden Azure Cloud Shell, um die Ressourcengruppen, die virtuellen Netzwerke und die virtuellen Computer zu erstellen.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

1. Klicken Sie im Fenster **Welcome to Azure Cloud Shell** (Willkommen bei Azure Cloud Shell) auf **PowerShell (Linux)**.

1. Klicken Sie im Fenster **You have no storage mounted** (Sie haben keinen Speicher bereitgestellt) auf **Speicher erstellen**.

1. Geben Sie an der Azure PowerShell-Eingabeaufforderung den folgenden Code ein, und drücken Sie die EINGABETASTE.

    ```PowerShell
    az group create --name myResourceGroup --location eastus
    ```

## <a name="create-a-virtual-network"></a>Erstellen eines virtuellen Netzwerks

1. Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE, um ein virtuelles Netzwerk zu erstellen.

    ```PowerShell
    az network vnet create --name myVirtualNetwork --resource-group myResourceGroup --subnet-name default
    ```

## <a name="create-two-virtual-machines"></a>Erstellen von zwei virtuellen Computern

1. Erstellen Sie den ersten virtuellen Computer. Führen Sie dazu den folgenden Befehl aus, um einen virtuellen Windows-Computer mit einer öffentlichen IP-Adresse zu erstellen, auf die über den Port 3389 (Remotedesktop) zugegriffen werden kann:

    ``` PowerShell
    az vm create --name dataProcessingStage1 --resource-group MyResourceGroup --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. Geben Sie an den Eingabeaufforderungen Werte für Ihr Kennwort ein.

1. Führen Sie den folgenden Befehl aus, um einen virtuellen Windows-Computer ohne öffentliche IP-Adresse zu erstellen:

    ```PowerShell
    az vm create -n dataProcessingStage2 -g MyResourceGroup --public-ip-address '' --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. Nach Abschluss des Vorgangs enthält die Ausgabe des zweiten Befehls einen Wert für „publicIpAddress“.

## <a name="connect-to-dataprocessingstage1-using-remote-desktop"></a>Herstellen einer Remotedesktopverbindung mit „dataProcessingStage1“

1. Drücken Sie auf Ihrem Clientcomputer die Windows-Taste, und geben Sie „RDP“ ein.

1. Vergewissern Sie sich, dass die App **Remotedesktopverbindung** ausgewählt ist, und drücken Sie die EINGABETASTE.

1. Geben Sie im Dialogfeld **Remotedesktopverbindung** im Feld **Computer** den Wert von „dataProcessingStage1PublicIPAddress“ ein, und klicken Sie anschließend auf **Verbinden**.

1. Klicken **Sie im Dialogfeld mit der Frage, ob Sie dieser Remoteverbindung**vertrauen, auf **Verbinden**.

1. Geben Sie im Dialogfeld **Windows-Sicherheit** den Benutzernamen und das Kennwort ein, den bzw. das Sie bei der Erstellung von „dataProcessingStage1“ verwendet haben.

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **OK**.

1. Melden Sie sich bei dem Remotecomputer in Azure an.

1. Klicken Sie in der Meldung **Netzwerke** auf **Nein**.

1. Schließen Sie den Server-Manager.

1. Klicken Sie in der Remotesitzung mit der rechten Maustaste auf das Startmenü, und klicken Sie auf **Eingabeaufforderung**.

1. Geben Sie im Eingabeaufforderungsfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE.

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. Vom Remotecomputer sollte keine Antwort zurückgegeben werden. Das liegt daran, dass ICMP-Antworten standardmäßig von der Windows-Firewall blockiert werden.

## <a name="connect-to-dataprocessingstage2-using-remote-desktop"></a>Herstellen einer Remotedesktopverbindung mit „dataProcessingStage2“

1. Drücken Sie auf Ihrem Clientcomputer die Windows-Taste, und geben Sie **RDP** ein. Wählen Sie die App **Remotedesktopverbindung** aus, und drücken Sie die EINGABETASTE.

1. Geben Sie im Feld **Computer** den Wert von „dataProcessingStage2PublicIPAddress“ ein, und klicken Sie anschließend auf **Verbinden**.

1. Klicken **Sie im Dialogfeld mit der Frage, ob Sie dieser Remoteverbindung**vertrauen, auf **Verbinden**.

1. Geben Sie im Dialogfeld **Windows-Sicherheit** den Benutzernamen und das Kennwort ein, den bzw. das Sie bei der Erstellung von „dataProcessingStage2“ verwendet haben.

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **OK**. Melden Sie sich nun bei dem Remotecomputer in Azure an.

1. Klicken Sie in der Meldung **Netzwerke** auf **Nein**.

1. Schließen Sie den Server-Manager.

1. Drücken Sie auf „DataProcessingStage2“ die Windows-Taste, geben Sie **Firewall** ein, und drücken Sie die EINGABETASTE. Die Konsole **Windows-Firewall mit erweiterter Sicherheit** wird angezeigt.

1. Klicken Sie im linken Bereich auf **Eingehende Regeln**.

1. Scrollen Sie im rechten Bereich nach unten, klicken Sie mit der rechten Maustaste auf **Datei- und Druckerfreigabe (Echoanforderung – ICMPv4 eingehend)**, und klicken Sie anschließend auf **Regel aktivieren**.

1. Wechseln Sie wieder zur Konsole „dataProcessingStage1“, geben Sie im Eingabeaufforderungsfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE.

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. „dataProcessingStage2“ gibt vier Antworten zurück und bestätigt so die Konnektivität zwischen den beiden virtuellen Computern.

## <a name="summary"></a>Zusammenfassung

Sie haben erfolgreich ein virtuelles Netzwerk und zwei virtuelle Computer erstellt, die an das virtuelle Netzwerk angefügt sind. Darüber hinaus haben Sie eine Verbindung mit einem der virtuellen Computer hergestellt und die Netzwerkkonnektivität mit dem anderen virtuellen Computer im gleichen virtuellen Netzwerk überprüft. Sie können Azure Virtual Network verwenden, um Ressourcen innerhalb des Azure-Netzwerks zu verbinden. Diese Ressourcen müssen sich jedoch innerhalb der gleichen Ressourcengruppe und innerhalb des gleichen Abonnements befinden. Als Nächstes beschäftigen wir uns mit VPN-Gateways. Mit einem VPN-Gateway können Sie virtuelle Netzwerk in unterschiedlichen Ressourcengruppen, Abonnements und sogar geografischen Regionen verbinden.
