Sie möchten sichergehen, dass Sie Clients oder Websites innerhalb Ihrer Umgebung unter Verwendung verschlüsselter Tunnel über das öffentliche Internet mit Azure verbinden können. In dieser Übung erstellen Sie ein Point-to-Site-VPN-Gateway und stellen anschließend über einen Clientcomputer eine Verbindung mit diesem Gateway her. Aus Sicherheitsgründen verwenden Sie Verbindungen mit nativer Azure-Zertifikatauthentifizierung.

Der Prozess umfasst folgende Schritte:

1. Erstellen eines RouteBased-VPN-Gateways

1. Hochladen des öffentlichen Schlüssels für ein Stammzertifikat zur Authentifizierung

1. Generieren eines Clientzertifikats auf der Grundlage des Stammzertifikats und anschließendes Installieren des Clientzertifikats auf jedem Clientcomputer, der eine Verbindung mit dem VNet herstellt, um die Authentifizierung zu ermöglichen

1. Erstellen von VPN-Clientkonfigurationsdateien mit den erforderlichen Informationen, damit der Client eine Verbindung mit dem VNet herstellen kann

## <a name="before-you-begin"></a>Vorbereitung

Für diese Aufgabe benötigen Sie Folgendes:

- Azure PowerShell

- Einen Ordner namens „C:\cert“

So installieren Sie Azure PowerShell:

1. Klicken Sie mit der rechten Maustaste auf die Windows-Schaltfläche, und klicken Sie anschließend auf **Windows PowerShell (Administrator)**.

1. Klicken Sie in der Meldung der **Benutzerkontensteuerung** auf **Ja**.

1. Geben Sie im PowerShell-Fenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```PowerShell
    Import-Module AzureRM
    ```

1. Geben Sie bei dem Sicherheitshinweis „A“ ein, und drücken Sie die EINGABETASTE.

## <a name="sign-in-and-set-variables"></a>Anmelden und Festlegen von Variablen

Gehen Sie wie folgt vor, um sich anzumelden und Variablen festzulegen:

1. Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE, um eine Verbindung mit Azure herzustellen:

    ```PowerShell
    Connect-AzureRmAccount
    ```

1. Rufen Sie eine Liste mit Ihren Azure-Abonnements ab.

    ```PowerShell
    Get-AzureRmSubscription
    ```
1. Geben Sie das Abonnement an, das Sie verwenden möchten.

    ```PowerShell
    Select-AzureRmSubscription -SubscriptionName "{Name of your subscription}"
    ```

    Ersetzen Sie „Name des Abonnements“ durch den Namen Ihres Abonnements.

1. Geben Sie die folgenden Variablen ein, und drücken Sie nach jeder Eingabe die EINGABETASTE.

    ```PowerShell
    $VNetName  = "VNetData"
    $FESubName = "FrontEnd"
    $BESubName = "Backend"
    $GWSubName = "GatewaySubnet"
    $VNetPrefix1 = "192.168.0.0/16"
    $VNetPrefix2 = "10.254.0.0/16"
    $FESubPrefix = "192.168.1.0/24"
    $BESubPrefix = "10.254.1.0/24"
    $GWSubPrefix = "192.168.200.0/26"
    $VPNClientAddressPool = "172.16.201.0/24"
    $RG = "TestRG"
    $Location = "East US"
    $GWName = "VNetDataGW"
    $GWIPName = "VNetDataGWPIP"
    $GWIPconfName = "gwipconf"
    ```

## <a name="configure-a-vnet"></a>Konfigurieren eines VNets

1. Erstellen Sie eine Ressourcengruppe.

    ```PowerShell
    New-AzureRmResourceGroup -Name $RG -Location $Location
    ```

1. Erstellen Sie Subnetzkonfigurationen für das virtuelle Netzwerk. Benennen Sie sie mit **Front-End, Back-End** und **GatewaySubnet**. Diese Subnetze befinden sich alle innerhalb des Präfix des virtuellen Netzwerks.

    ```PowerShell
    $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
    $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
    $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
    ```

1. Erstellen Sie das virtuelle Netzwerk unter Verwendung der Subnetzwerte und eines statischen DNS-Servers. 
    > [!IMPORTANT]
    > Ignorieren Sie die Warnmeldung, und warten Sie, bis die Ausführung des Befehls abgeschlossen ist.

    ```PowerShell
    New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3
    ```

1. Geben Sie nun die Variablen für das Netzwerk an, das Sie soeben erstellt haben.

    ```PowerShell
    $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    ```

1. Fordern Sie eine dynamisch zugewiesene öffentliche IP-Adresse an.

    ```PowerShell
    $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
    $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
    ```

## <a name="create-the-vpn-gateway"></a>Erstellen des VPN-Gateways

Achten Sie beim Erstellen dieses VPN-Gateways auf Folgendes:

- „GatewayType“ muss „Vpn“ lauten.
- „VpnType“ muss „RouteBased“ lauten.

> [!NOTE]
> Hinweis: Dieser Teil der Übung kann abhängig vom Wert der Gateway-SKU bis zu 45 Minuten dauern.

1. Führen Sie zum Erstellen des VPN-Gateways den folgenden Befehl aus, und drücken Sie die EINGABETASTE.

    ```PowerShell
    New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
    -Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
    -VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"
    ```

1. Warten Sie, bis die Ausgabe des Befehls angezeigt wird.

## <a name="add-the-vpn-client-address-pool"></a>Hinzufügen des VPN-Clientadresspools

1. Führen Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE.

    ```PowerShell
    $Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
    Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
    ```

1. Warten Sie, bis die Ausgabe des Befehls angezeigt wird.

## <a name="generate-a-client-certificate"></a>Generieren eines Clientzertifikats

1. Erstellen Sie das selbstsignierte Stammzertifikat.

    ```PowerShell
    $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
    -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
    ```

1. Generieren Sie ein Clientzertifikat.

    ```PowerShell
    New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
    -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
    ```

1. Exportieren Sie den öffentlichen Schlüssel des Stammzertifikats. Geben Sie auf Ihrem Clientcomputer den folgenden Befehl ein, und drücken Sie die EINGABETASTE.

    ```PowerShell
    certmgr
    ```

1. Navigieren Sie zu „Personal/Certificates“. Klicken Sie mit der rechten Maustaste auf „P2SRootCert“, klicken Sie auf **Alle Aufgaben**, und klicken Sie anschließend auf **Exportieren**.

1. Klicken Sie im Zertifikatexport-Assistenten auf **Weiter**.

1. Vergewissern Sie sich, dass **Nein, privaten Schlüssel nicht exportieren** ausgewählt ist, und klicken Sie auf **Weiter**.

1. Vergewissern Sie sich auf der Seite **Dateiformat für den Export**, dass **Base-64-codiert X.509 (.CER)** ausgewählt ist, und klicken Sie auf **Weiter**.

1. Geben Sie auf der Seite **Zu exportierende Datei** unter **Dateiname** die Zeichenfolge **C:\cert\P2SRootCert.cer** ein, und klicken Sie anschließend auf „Weiter“.

1. Klicken Sie auf der **Abschlussseite des Zertifikatexport-Assistenten**auf **Fertig stellen**.

1. Klicken Sie im **Meldungsfeld des Zertifikatexport-Assistenten** auf **OK**.

## <a name="upload-the-root-certificate-public-key-information"></a>Hochladen der Informationen des öffentlichen Schlüssels des Stammzertifikats

1. Führen Sie im PowerShell-Fenster den folgenden Befehl aus, um eine Variable für den Zertifikatnamen zu deklarieren:

    ```PowerShell
    $P2SRootCertName = "P2SRootCert.cer"
    ```

1. Führen Sie den folgenden Befehl aus:

    ```PowerShell
    $filePathForCert = "C:\cert\P2SRootCert.cer"
    $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
    $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
    $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
    ```

1. Laden Sie nun das Zertifikat in Azure hoch. Daraufhin wird es von Azure als vertrauenswürdiges Stammzertifikat erkannt.

    ```PowerShell
    Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNetDataGW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
    ```

## <a name="configure-the-native-vpn-client"></a>Konfigurieren des nativen VPN-Clients

1. Führen Sie den folgenden Befehl aus, um VPN-Clientkonfigurationsdateien im ZIP-Format zu erstellen.

    ```PowerShell
    $profile=New-AzureRmVpnClientConfiguration -ResourceGroupName "TestRG" -Name "VNetDataGW" -AuthenticationMethod "EapTls"
    $profile.VPNProfileSASUrl
    ```

1. Kopieren Sie die URL aus der Befehlsausgabe, und fügen Sie sie in Ihrem Browser ein. Daraufhin sollte der Browser mit dem Herunterladen einer ZIP-Datei beginnen. Entzippen Sie die Datei, und legen Sie sie an einem geeigneten Speicherort ab.

1. Navigieren Sie in dem extrahierten Ordner entweder zum Ordner „WindowsAmd64“ (für Windows-Computer mit 64 Bit) oder zum Ordner „WindowsZX86“ (für Computer mit 32 Bit).

1. Doppelklicken Sie auf die Datei „VpnClientSetupxxxxx.exe“ für Ihre Architektur.

1. Klicken Sie im Bildschirm **Der Computer wurde durch Windows geschützt.** auf **Weitere Informationen** und anschließend auf **Trotzdem ausführen**.

1. Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.

1. Klicken Sie im Dialogfeld **VNetData** auf **Ja**.

## <a name="connect-to-azure"></a>Herstellen einer Verbindung mit Azure

1. Drücken Sie die Windows-Taste, geben Sie **Einstellungen** ein, und drücken Sie die EINGABETASTE.

1. Klicken Sie im Fenster **Einstellungen** auf **Netzwerk und Internet**.

1. Klicken Sie im linken Bereich auf **VPN**.

1. Klicken Sie im rechten Bereich auf **VNetData** und anschließend auf **Verbinden**.

1. Klicken Sie im Fenster „VNetData“ auf **Verbinden**.

1. Klicken Sie im nächsten VNetData-Fenster auf **Weiter**.

1. Klicken Sie in der Meldung der **Benutzerkontensteuerung** auf **Ja**.

> [!NOTE]
> Sollten diese Schritte nicht funktionieren, ist möglicherweise ein Neustart des Computers erforderlich.

## <a name="verify-your-connection"></a>Überprüfen der Verbindung

1. Drücken Sie die Windows-Taste, geben Sie **cmd** ein, und drücken Sie die EINGABETASTE. Das Fenster **Eingabeaufforderung** wird angezeigt.

1. Geben Sie `IPCONFIG /ALL` ein, und drücken Sie die EINGABETASTE.

1. Kopieren Sie die IP-Adresse unter dem PPP-Adapter „VNetData“, oder schreiben Sie sich die Adresse auf.

1. Vergewissern Sie sich, dass die IP-Adresse im **VPNClientAddressPool-Bereich 172.16.201.0/24** liegt.

1. Sie haben erfolgreich eine Verbindung mit dem Azure-VPN-Gateway hergestellt.

## <a name="summary"></a>Zusammenfassung

Sie haben soeben ein VPN-Gateway eingerichtet, das es Ihnen ermöglicht, eine verschlüsselte Clientverbindung mit einem VNet in Azure herzustellen. Dieser Ansatz eignet sich hervorragend für Clientcomputer und kleinere Site-to-Site-Verbindungen.