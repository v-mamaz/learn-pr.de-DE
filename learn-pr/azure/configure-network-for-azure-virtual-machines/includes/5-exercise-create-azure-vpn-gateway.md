<span data-ttu-id="7556b-101">Sie möchten sichergehen, dass Sie Clients oder Websites innerhalb Ihrer Umgebung unter Verwendung verschlüsselter Tunnel über das öffentliche Internet mit Azure verbinden können.</span><span class="sxs-lookup"><span data-stu-id="7556b-101">You want to ensure that you can connect clients or sites within your environment into Azure using encrypted tunnels across the public internet.</span></span> <span data-ttu-id="7556b-102">In dieser Einheit erstellen Sie ein Point-to-Site-VPN-Gateway und stellen anschließend über einen Clientcomputer eine Verbindung mit diesem Gateway her.</span><span class="sxs-lookup"><span data-stu-id="7556b-102">In this unit, you'll create a point-to-site VPN gateway, and then connect to that gateway from a client computer.</span></span> <span data-ttu-id="7556b-103">Aus Sicherheitsgründen verwenden Sie Verbindungen mit nativer Azure-Zertifikatauthentifizierung.</span><span class="sxs-lookup"><span data-stu-id="7556b-103">You'll use native Azure certificate authentication connections for security.</span></span>

<span data-ttu-id="7556b-104">Der Prozess umfasst folgende Schritte:</span><span class="sxs-lookup"><span data-stu-id="7556b-104">You will carry out the following process:</span></span>

1. <span data-ttu-id="7556b-105">Erstellen eines RouteBased-VPN-Gateways</span><span class="sxs-lookup"><span data-stu-id="7556b-105">Create a RouteBased VPN gateway.</span></span>

1. <span data-ttu-id="7556b-106">Hochladen des öffentlichen Schlüssels für ein Stammzertifikat zur Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="7556b-106">Upload the public key for a root certificate for authentication purposes.</span></span>

1. <span data-ttu-id="7556b-107">Generieren eines Clientzertifikats auf der Grundlage des Stammzertifikats und anschließendes Installieren des Clientzertifikats auf jedem Clientcomputer, der eine Verbindung mit dem virtuellen Netzwerk herstellt, um die Authentifizierung zu ermöglichen</span><span class="sxs-lookup"><span data-stu-id="7556b-107">Generate a client certificate from the root certificate, and then install the client certificate on each client computer that will connect to the virtual network for authentication purposes.</span></span>

1. <span data-ttu-id="7556b-108">Erstellen von VPN-Clientkonfigurationsdateien mit den erforderlichen Informationen, damit der Client eine Verbindung mit dem virtuellen Netzwerk herstellen kann</span><span class="sxs-lookup"><span data-stu-id="7556b-108">Create VPN client configuration files, which contain the necessary information for the client to connect to the virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7556b-109">Vorbereitung</span><span class="sxs-lookup"><span data-stu-id="7556b-109">Before you begin</span></span>
<!---TODO: These should be prerequisites in the first unit and on the index.yml--->

<span data-ttu-id="7556b-110">Für dieses Modul benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="7556b-110">To complete this module, you must have:</span></span>

- <span data-ttu-id="7556b-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7556b-111">Azure PowerShell</span></span>

- <span data-ttu-id="7556b-112">Einen Ordner namens „C:\cert“</span><span class="sxs-lookup"><span data-stu-id="7556b-112">A folder called C:\cert</span></span>

<span data-ttu-id="7556b-113">So installieren Sie Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7556b-113">To install Azure PowerShell:</span></span>

1. <span data-ttu-id="7556b-114">Klicken Sie mit der rechten Maustaste auf die Windows-Schaltfläche, und klicken Sie anschließend auf **Windows PowerShell (Administrator)**.</span><span class="sxs-lookup"><span data-stu-id="7556b-114">Right-click the Windows button and click **PowerShell (Admin)**.</span></span>

1. <span data-ttu-id="7556b-115">Klicken Sie in der Meldung der **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="7556b-115">In the **User Account Control** message box, click **Yes**.</span></span>

1. <span data-ttu-id="7556b-116">Geben Sie im PowerShell-Fenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="7556b-116">In the PowerShell window, type the following command and press Enter:</span></span>

    ```PowerShell
    Import-Module AzureRM
    ```

1. <span data-ttu-id="7556b-117">Geben Sie bei dem Sicherheitshinweis „A“ ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-117">At the security prompt, type A and press Enter.</span></span>

## <a name="sign-in-and-set-variables"></a><span data-ttu-id="7556b-118">Anmelden und Festlegen von Variablen</span><span class="sxs-lookup"><span data-stu-id="7556b-118">Sign in and set variables</span></span>

<span data-ttu-id="7556b-119">Gehen Sie wie folgt vor, um sich anzumelden und Variablen festzulegen:</span><span class="sxs-lookup"><span data-stu-id="7556b-119">To sign in and set variables, carry out the following steps:</span></span>

1. <span data-ttu-id="7556b-120">Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE, um eine Verbindung mit Azure herzustellen:</span><span class="sxs-lookup"><span data-stu-id="7556b-120">Connect to Azure by entering the following command and pressing Enter:</span></span>

    ```PowerShell
    Connect-AzureRmAccount
    ```

1. <span data-ttu-id="7556b-121">Rufen Sie eine Liste mit Ihren Azure-Abonnements ab.</span><span class="sxs-lookup"><span data-stu-id="7556b-121">Get a list of your Azure subscriptions.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
1. <span data-ttu-id="7556b-122">Geben Sie das Abonnement an, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="7556b-122">Specify the subscription that you want to use.</span></span>

    ```PowerShell
    Select-AzureRmSubscription -SubscriptionName "{Name of your subscription}"
    ```

    <span data-ttu-id="7556b-123">Ersetzen Sie „Name des Abonnements“ durch den Namen Ihres Abonnements.</span><span class="sxs-lookup"><span data-stu-id="7556b-123">Replace "Name of subscription" with your subscription name.</span></span>

1. <span data-ttu-id="7556b-124">Geben Sie die folgenden Variablen ein, und drücken Sie nach jeder Eingabe die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-124">Enter the following variables and press Enter after each one.</span></span>

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

## <a name="configure-a-virtual-network"></a><span data-ttu-id="7556b-125">Konfigurieren eines virtuellen Netzwerks</span><span class="sxs-lookup"><span data-stu-id="7556b-125">Configure a virtual network</span></span>

1. <span data-ttu-id="7556b-126">Erstellen Sie eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="7556b-126">Create a resource group.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name $RG -Location $Location
    ```

1. <span data-ttu-id="7556b-127">Erstellen Sie Subnetzkonfigurationen für das virtuelle Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="7556b-127">Create subnet configurations for the virtual network.</span></span> <span data-ttu-id="7556b-128">Benennen Sie sie mit **Front-End, Back-End** und **GatewaySubnet**.</span><span class="sxs-lookup"><span data-stu-id="7556b-128">These have the name **FrontEnd, BackEnd**, and **GatewaySubnet**.</span></span> <span data-ttu-id="7556b-129">Diese Subnetze befinden sich alle innerhalb des Präfix des virtuellen Netzwerks.</span><span class="sxs-lookup"><span data-stu-id="7556b-129">All of these subnets exist within the virtual network prefix.</span></span>

    ```PowerShell
    $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
    $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
    $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
    ```

1. <span data-ttu-id="7556b-130">Erstellen Sie das virtuelle Netzwerk unter Verwendung der Subnetzwerte und eines statischen DNS-Servers.</span><span class="sxs-lookup"><span data-stu-id="7556b-130">Create the virtual network using the subnet values and a static DNS server.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7556b-131">Ignorieren Sie die Warnmeldung, und warten Sie dann, bis die Ausführung des Befehls abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="7556b-131">Ignore the warning message, and then wait for the command to finish.</span></span>

    ```PowerShell
    New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3
    ```

1. <span data-ttu-id="7556b-132">Geben Sie nun die Variablen für das Netzwerk an, das Sie soeben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="7556b-132">Now specify the variables for this network that you have just created.</span></span>

    ```PowerShell
    $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    ```

1. <span data-ttu-id="7556b-133">Fordern Sie eine dynamisch zugewiesene öffentliche IP-Adresse an.</span><span class="sxs-lookup"><span data-stu-id="7556b-133">Request a dynamically assigned public IP address.</span></span>

    ```PowerShell
    $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
    $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
    ```

## <a name="create-the-vpn-gateway"></a><span data-ttu-id="7556b-134">Erstellen des VPN-Gateways</span><span class="sxs-lookup"><span data-stu-id="7556b-134">Create the VPN gateway</span></span>

<span data-ttu-id="7556b-135">Achten Sie beim Erstellen dieses VPN-Gateways auf Folgendes:</span><span class="sxs-lookup"><span data-stu-id="7556b-135">When creating this VPN gateway:</span></span>

- <span data-ttu-id="7556b-136">„GatewayType“ muss „Vpn“ lauten.</span><span class="sxs-lookup"><span data-stu-id="7556b-136">GatewayType must be Vpn</span></span>
- <span data-ttu-id="7556b-137">„VpnType“ muss „RouteBased“ lauten.</span><span class="sxs-lookup"><span data-stu-id="7556b-137">VpnType must be RouteBased</span></span>

> [!NOTE]
> <span data-ttu-id="7556b-138">Beachten Sie, dass dieser Teil der Übung abhängig vom Wert der Gateway-SKU bis zu 45 Minuten dauern kann.</span><span class="sxs-lookup"><span data-stu-id="7556b-138">Note that this part of the exercise can take up to 45 minutes to complete, depending on the value of GatewaySku.</span></span>

1. <span data-ttu-id="7556b-139">Führen Sie zum Erstellen des VPN-Gateways den folgenden Befehl aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-139">To create the VPN gateway, run the following command and press Enter.</span></span>

    ```PowerShell
    New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
    -Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
    -VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"
    ```

1. <span data-ttu-id="7556b-140">Warten Sie, bis die Ausgabe des Befehls angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="7556b-140">Wait for the command output to appear.</span></span>

## <a name="add-the-vpn-client-address-pool"></a><span data-ttu-id="7556b-141">Hinzufügen des VPN-Clientadresspools</span><span class="sxs-lookup"><span data-stu-id="7556b-141">Add the VPN client address pool</span></span>

1. <span data-ttu-id="7556b-142">Führen Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-142">Run the following command and press Enter.</span></span>

    ```PowerShell
    $Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
    Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
    ```

1. <span data-ttu-id="7556b-143">Warten Sie, bis die Ausgabe des Befehls angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="7556b-143">Wait for the command output to appear.</span></span>

## <a name="generate-a-client-certificate"></a><span data-ttu-id="7556b-144">Generieren eines Clientzertifikats</span><span class="sxs-lookup"><span data-stu-id="7556b-144">Generate a client certificate</span></span>

1. <span data-ttu-id="7556b-145">Erstellen Sie das selbstsignierte Stammzertifikat.</span><span class="sxs-lookup"><span data-stu-id="7556b-145">Create the self-signed root certificate.</span></span>

    ```PowerShell
    $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
    -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
    ```

1. <span data-ttu-id="7556b-146">Generieren Sie ein Clientzertifikat.</span><span class="sxs-lookup"><span data-stu-id="7556b-146">Generate a client certificate.</span></span>

    ```PowerShell
    New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
    -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
    ```

1. <span data-ttu-id="7556b-147">Exportieren Sie den öffentlichen Schlüssel des Stammzertifikats.</span><span class="sxs-lookup"><span data-stu-id="7556b-147">Export the root certificate public key.</span></span> <span data-ttu-id="7556b-148">Geben Sie auf Ihrem Clientcomputer den folgenden Befehl ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-148">On your client computer, type the following command and press Enter.</span></span>

    ```PowerShell
    certmgr
    ```

1. <span data-ttu-id="7556b-149">Navigieren Sie zu „Personal/Certificates“.</span><span class="sxs-lookup"><span data-stu-id="7556b-149">Navigate to Personal/Certificates.</span></span> <span data-ttu-id="7556b-150">Klicken Sie mit der rechten Maustaste auf „P2SRootCert“, klicken Sie auf **Alle Aufgaben**, und klicken Sie anschließend auf **Exportieren**.</span><span class="sxs-lookup"><span data-stu-id="7556b-150">Right-click P2SRootCert, click **All tasks**, and then select **Export**.</span></span>

1. <span data-ttu-id="7556b-151">Klicken Sie im Zertifikatexport-Assistenten auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="7556b-151">In the Certificate Export Wizard, click **Next**.</span></span>

1. <span data-ttu-id="7556b-152">Vergewissern Sie sich, dass **Nein, privaten Schlüssel nicht exportieren** ausgewählt ist, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="7556b-152">Ensure that **No, do not export the private key** is selected, and then click **Next**.</span></span>

1. <span data-ttu-id="7556b-153">Vergewissern Sie sich auf der Seite **Format der zu exportierenden Datei**, dass **Base-64-codiert X.509 (.CER)** ausgewählt ist, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="7556b-153">On the **Export File Format** page, ensure that **Base-64 encoded X.509 (.CER)** is selected, and then click **Next**.</span></span>

1. <span data-ttu-id="7556b-154">Geben Sie auf der Seite **Zu exportierende Datei** unter **Dateiname** die Zeichenfolge **C:\cert\P2SRootCert.cer** ein, und klicken Sie anschließend auf „Weiter“.</span><span class="sxs-lookup"><span data-stu-id="7556b-154">In the **File to Export** page, under **File name**, enter **C:\cert\P2SRootCert.cer**, and then click Next.</span></span>

1. <span data-ttu-id="7556b-155">Klicken Sie auf der **Abschlussseite des Zertifikatexport-Assistenten**auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="7556b-155">On the **Completing the Certificate Export Wizard** page, click **Finish**.</span></span>

1. <span data-ttu-id="7556b-156">Klicken Sie im **Meldungsfeld des Zertifikatexport-Assistenten** auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7556b-156">On the **Certificate Export Wizard** message box, click **OK**.</span></span>

## <a name="upload-the-root-certificate-public-key-information"></a><span data-ttu-id="7556b-157">Hochladen der Informationen des öffentlichen Schlüssels des Stammzertifikats</span><span class="sxs-lookup"><span data-stu-id="7556b-157">Upload the root certificate public key information</span></span>

1. <span data-ttu-id="7556b-158">Führen Sie im PowerShell-Fenster den folgenden Befehl aus, um eine Variable für den Zertifikatnamen zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="7556b-158">In the PowerShell window, execute the following command to declare a variable for the certificate name:</span></span>

    ```PowerShell
    $P2SRootCertName = "P2SRootCert.cer"
    ```

1. <span data-ttu-id="7556b-159">Führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="7556b-159">Execute the following command:</span></span>

    ```PowerShell
    $filePathForCert = "C:\cert\P2SRootCert.cer"
    $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
    $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
    $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
    ```

1. <span data-ttu-id="7556b-160">Laden Sie nun das Zertifikat in Azure hoch.</span><span class="sxs-lookup"><span data-stu-id="7556b-160">Now upload the certificate to Azure.</span></span> <span data-ttu-id="7556b-161">Daraufhin wird es von Azure als vertrauenswürdiges Stammzertifikat erkannt.</span><span class="sxs-lookup"><span data-stu-id="7556b-161">Azure then recognizes it as a trusted root certificate.</span></span>

    ```PowerShell
    Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNetDataGW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
    ```

## <a name="configure-the-native-vpn-client"></a><span data-ttu-id="7556b-162">Konfigurieren des nativen VPN-Clients</span><span class="sxs-lookup"><span data-stu-id="7556b-162">Configure the native VPN client</span></span>

1. <span data-ttu-id="7556b-163">Führen Sie den folgenden Befehl aus, um VPN-Clientkonfigurationsdateien im ZIP-Format zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7556b-163">Execute the following command to create VPN client configuration files in .ZIP format.</span></span>

    ```PowerShell
    $profile=New-AzureRmVpnClientConfiguration -ResourceGroupName "TestRG" -Name "VNetDataGW" -AuthenticationMethod "EapTls"
    $profile.VPNProfileSASUrl
    ```

1. <span data-ttu-id="7556b-164">Kopieren Sie die URL aus der Befehlsausgabe, und fügen Sie sie in Ihren Browser ein.</span><span class="sxs-lookup"><span data-stu-id="7556b-164">Copy the URL returned in the output from this command and paste it into your browser.</span></span> <span data-ttu-id="7556b-165">Daraufhin sollte der Browser mit dem Herunterladen einer ZIP-Datei beginnen.</span><span class="sxs-lookup"><span data-stu-id="7556b-165">Your browser should start downloading a .ZIP file.</span></span> <span data-ttu-id="7556b-166">Entzippen Sie die Datei, und legen Sie sie an einem geeigneten Speicherort ab.</span><span class="sxs-lookup"><span data-stu-id="7556b-166">Unzip it and put it in a suitable location.</span></span>

1. <span data-ttu-id="7556b-167">Navigieren Sie im extrahierten Ordner entweder zum Ordner „WindowsAmd64“ (für 64-Bit-Windows-Computer) oder zum Ordner „WindowsZX86“ (für 32-Bit-Computer).</span><span class="sxs-lookup"><span data-stu-id="7556b-167">In the extracted folder, navigate to either the WindowsAmd64 folder (for 64-bit Windows computers) or the WindowsZX86 folder (for 32-bit computers).</span></span>

1. <span data-ttu-id="7556b-168">Doppelklicken Sie auf die Datei „VpnClientSetupxxxxx.exe“ für Ihre Architektur.</span><span class="sxs-lookup"><span data-stu-id="7556b-168">Double-click on the VpnClientSetupxxxxx.exe file, depending on your architecture.</span></span>

1. <span data-ttu-id="7556b-169">Klicken Sie auf dem Bildschirm **Der Computer wurde durch Windows geschützt.** auf **Weitere Informationen** und anschließend auf **Trotzdem ausführen**.</span><span class="sxs-lookup"><span data-stu-id="7556b-169">In the **Windows protected your PC** screen, click **More info**, and then click **Run anyway**.</span></span>

1. <span data-ttu-id="7556b-170">Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="7556b-170">In the **User Account Control** dialog box, click **Yes**.</span></span>

1. <span data-ttu-id="7556b-171">Klicken Sie im Dialogfeld **VNetData** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="7556b-171">In the **VNetData** dialog box, click **Yes**.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="7556b-172">Herstellen einer Verbindung mit Azure</span><span class="sxs-lookup"><span data-stu-id="7556b-172">Connect to Azure</span></span>

1. <span data-ttu-id="7556b-173">Drücken Sie die Windows-Taste, geben Sie **Einstellungen** ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-173">Press the Windows key, type **Settings** and press Enter.</span></span>

1. <span data-ttu-id="7556b-174">Klicken Sie im Fenster **Einstellungen** auf **Netzwerk und Internet**.</span><span class="sxs-lookup"><span data-stu-id="7556b-174">In the **Settings** window, click **Network and Internet**.</span></span>

1. <span data-ttu-id="7556b-175">Klicken Sie im linken Bereich auf **VPN**.</span><span class="sxs-lookup"><span data-stu-id="7556b-175">In the left-hand pane, click **VPN**.</span></span>

1. <span data-ttu-id="7556b-176">Klicken Sie im rechten Bereich auf **VNetData** und anschließend auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="7556b-176">In the right-hand pane, click **VNetData**, and then click **Connect**.</span></span>

1. <span data-ttu-id="7556b-177">Klicken Sie im Fenster „VNetData“ auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="7556b-177">In the VNetData window, click **Connect**.</span></span>

1. <span data-ttu-id="7556b-178">Klicken Sie im nächsten VNetData-Fenster auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="7556b-178">In the next VNetData window, click **Continue**.</span></span>

1. <span data-ttu-id="7556b-179">Klicken Sie in der Meldung der **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="7556b-179">In the **User Account Control** message box, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="7556b-180">Sollten diese Schritte nicht funktionieren, ist möglicherweise ein Neustart des Computers erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7556b-180">If these steps do not work, you may need to restart your computer.</span></span>

## <a name="verify-your-connection"></a><span data-ttu-id="7556b-181">Überprüfen der Verbindung</span><span class="sxs-lookup"><span data-stu-id="7556b-181">Verify your connection</span></span>

1. <span data-ttu-id="7556b-182">Drücken Sie die Windows-Taste, geben Sie **cmd** ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-182">Press the Windows key, type **cmd** and press Enter.</span></span> <span data-ttu-id="7556b-183">Das Fenster **Eingabeaufforderung** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7556b-183">The **Command Prompt** window appears.</span></span>

1. <span data-ttu-id="7556b-184">Geben Sie `IPCONFIG /ALL` ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="7556b-184">Type `IPCONFIG /ALL` and press Enter.</span></span>

1. <span data-ttu-id="7556b-185">Kopieren Sie die IP-Adresse unter dem PPP-Adapter „VNetData“, oder schreiben Sie sich die Adresse auf.</span><span class="sxs-lookup"><span data-stu-id="7556b-185">Copy the IP address under PPP adapter VNetData, or write it down.</span></span>

1. <span data-ttu-id="7556b-186">Vergewissern Sie sich, dass die IP-Adresse im **VPNClientAddressPool-Bereich 172.16.201.0/24** liegt.</span><span class="sxs-lookup"><span data-stu-id="7556b-186">Confirm that IP address is in the **VPNClientAddressPool range of 172.16.201.0/24**.</span></span>

1. <span data-ttu-id="7556b-187">Sie haben erfolgreich eine Verbindung mit dem Azure-VPN-Gateway hergestellt.</span><span class="sxs-lookup"><span data-stu-id="7556b-187">You have successfully made a connection to the Azure VPN gateway.</span></span>

## <a name="summary"></a><span data-ttu-id="7556b-188">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="7556b-188">Summary</span></span>

<span data-ttu-id="7556b-189">Sie haben soeben ein VPN-Gateway eingerichtet, das es Ihnen ermöglicht, eine verschlüsselte Clientverbindung mit einem virtuellen Netzwerk in Azure herzustellen.</span><span class="sxs-lookup"><span data-stu-id="7556b-189">You just set up a VPN gateway, allowing you to make an encrypted client connection to a virtual network in Azure.</span></span> <span data-ttu-id="7556b-190">Dieser Ansatz eignet sich hervorragend für Clientcomputer und kleinere Site-to-Site-Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="7556b-190">This approach is great with client computers and smaller site-to-site connections.</span></span>