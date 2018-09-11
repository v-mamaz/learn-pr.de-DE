<span data-ttu-id="fb758-101">Angenommen, Sie entwickeln eine Anwendung zur Finanzverwaltung für neue Startupunternehmen.</span><span class="sxs-lookup"><span data-stu-id="fb758-101">Suppose you are developing a financial management application for new business startups.</span></span> <span data-ttu-id="fb758-102">Sie möchten sicherstellen, dass alle ihre Kundendaten geschützt sind, daher haben Sie sich entschieden, ADE durchgängig für alle Betriebssystem- und Daten-Datenträger auf den Servern einzusetzen, auf denen die Anwendung gehostet ist.</span><span class="sxs-lookup"><span data-stu-id="fb758-102">You want to ensure that all your customers' data is secured, so you have decided to implement ADE across all OS and data disks on the servers that will host this application.</span></span> <span data-ttu-id="fb758-103">Im Rahmen Ihrer Complianceanforderungen müssen Sie außerdem selbst für die Verwaltung Ihrer eigenen Verschlüsselungsschlüssel zuständig sein.</span><span class="sxs-lookup"><span data-stu-id="fb758-103">As part of your compliance requirements, you also need to be responsible for your own encryption key management.</span></span>

<span data-ttu-id="fb758-104">In dieser Übungseinheit verschlüsseln Sie Datenträger auf vorhandenen Windows-VMs und verwalten die Verschlüsselungsschlüssel mithilfe Ihres eigenen Azure Key Vaults.</span><span class="sxs-lookup"><span data-stu-id="fb758-104">In this unit you'll encrypt disks on existing Windows VMs, and manage the encryption keys using your own Azure Key Vault.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fb758-105">Bei dieser Übung wird davon ausgegangen, dass Azure PowerShell auf Ihrem Computer installiert ist; Informationen zum Installieren von Azure PowerShell finden Sie unter [Installieren von Azure PowerShell unter Windows mit PowerShellGet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0).</span><span class="sxs-lookup"><span data-stu-id="fb758-105">This exercise assumes that Azure PowerShell is installed on your computer; go to [Install Azure PowerShell on Windows with PowerShellGet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0) for information on how to install Azure PowerShell.</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="fb758-106">Vorbereiten der Umgebung</span><span class="sxs-lookup"><span data-stu-id="fb758-106">Prepare the environment</span></span>

<span data-ttu-id="fb758-107">Wir beginnen, indem wir eine Windows-VM in einer neuen Ressourcengruppe bereitstellen und dann der VM einen Daten-Datenträger hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fb758-107">We'll start by deploying a Windows VM to a new resource group and then add a data disk to the VM.</span></span>

### <a name="deploy-windows-vm-using-azure-portal"></a><span data-ttu-id="fb758-108">Bereitstellen eines virtuellen Windows-Computers über das Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="fb758-108">Deploy Windows VM using Azure portal</span></span>

<span data-ttu-id="fb758-109">Hier verwenden Sie das Azure-Portal, um einen virtuellen Windows-Computer zu erstellen und bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="fb758-109">Here you'll install use the Azure portal to create and deploy a Windows VM.</span></span> <span data-ttu-id="fb758-110">Definieren Sie zunächst die grundlegenden Informationen über den virtuellen Computer:</span><span class="sxs-lookup"><span data-stu-id="fb758-110">Start by defining the basic VM information:</span></span>

1. <span data-ttu-id="fb758-111">Navigieren Sie im Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren normalen Anmeldeinformationen an.</span><span class="sxs-lookup"><span data-stu-id="fb758-111">In a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>

1. <span data-ttu-id="fb758-112">Klicken Sie auf der Randleiste auf **Virtuelle Computer**, und klicken Sie dann auf **Virtuellen Computer erstellen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-112">In the sidebar, click **Virtual machines**, and then click **Create virtual machine**.</span></span>

1. <span data-ttu-id="fb758-113">Klicken Sie auf dem Blatt „Compute“ im Abschnitt **Empfohlen** auf **Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="fb758-113">On the Compute blade, in the **Recommended** section, click **Windows Server**.</span></span>

1. <span data-ttu-id="fb758-114">Klicken Sie auf dem Blatt **Windows Server** auf **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="fb758-114">In the **Windows Server** blade, click **Windows Server 2016 Datacenter**.</span></span>

1. <span data-ttu-id="fb758-115">Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-115">In the **Windows Server 2016 Datacenter** blade, click **Create**.</span></span>

1. <span data-ttu-id="fb758-116">Geben Sie auf dem Blatt **Grundlagen** im Feld **Name** **moneyappsvr01** ein.</span><span class="sxs-lookup"><span data-stu-id="fb758-116">In the **Basics** blade, in the **Name** box, type **moneyappsvr01.**</span></span>

1. <span data-ttu-id="fb758-117">Geben Sie in den Feldern **Benutzername** und **Kennwort** einen Namen und ein Kennwort für ein Administratorkonto auf diesem Server ein.</span><span class="sxs-lookup"><span data-stu-id="fb758-117">In the **Username** and **Password boxes**, type a name and password for an administrator account on this server.</span></span>

1. <span data-ttu-id="fb758-118">Wählen Sie im Feld **Abonnement** Ihr Azure-Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="fb758-118">In the **Subscription** box, select your Azure subscription.</span></span>

1. <span data-ttu-id="fb758-119">Wählen Sie unter **Ressourcengruppe** **Neu erstellen** aus, und geben Sie im Feld **moneyapprg** ein.</span><span class="sxs-lookup"><span data-stu-id="fb758-119">Under **Resource Group**, select **Create new**, and in the box, type **moneyapprg**.</span></span>

1. <span data-ttu-id="fb758-120">Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="fb758-120">In the **Location** drop-down list, select a region near you.</span></span>

1. <span data-ttu-id="fb758-121">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb758-121">Click **OK**.</span></span>

### <a name="choose-a-size-for-the-vm-and-start-the-deployment"></a><span data-ttu-id="fb758-122">Wählen Sie eine Größe für die VM aus, und beginnen Sie mit der Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="fb758-122">Choose a size for the VM, and start the deployment</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb758-123">Beachten Sie, dass ADE im Basic-Tarif nicht unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="fb758-123">Remember that basic tier VMs do not support ADE</span></span>

1. <span data-ttu-id="fb758-124">Wählen Sie auf dem Blatt **Größe auswählen** eine **Standard**-SKU aus, z. B. **B1s**, und klicken Sie dann auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-124">On the **Choose a size** blade, select a **Standard** SKU, such as **B1s**, and then click **Select**.</span></span>

1. <span data-ttu-id="fb758-125">Klicken Sie auf dem Blatt **Einstellungen** in der Liste **Öffentliche Eingangsports hinzufügen** auf **RDP**, scrollen Sie dann nach unten, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb758-125">On the **Settings** blade, in the **Select public inbound ports** list, click **RDP**, and then scroll down and click **OK**.</span></span>

1. <span data-ttu-id="fb758-126">Klicken Sie auf dem Blatt **Erstellen** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-126">On the **Create** blade, click **Create**.</span></span>

1. <span data-ttu-id="fb758-127">Warten Sie die Bereitstellung des virtuellen Computers ab, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="fb758-127">Wait until the VM has deployed before continuing with the exercise.</span></span>

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="fb758-128">Hinzufügen eines Datenträgers zur VM</span><span class="sxs-lookup"><span data-stu-id="fb758-128">Add a data disk to the VM</span></span>

1. <span data-ttu-id="fb758-129">Klicken Sie im linken Menü auf **Alle Ressourcen** und dann auf **moneyappsvr01**.</span><span class="sxs-lookup"><span data-stu-id="fb758-129">In the left menu, click **All resources**, and then click **moneyappsvr01**.</span></span>

1. <span data-ttu-id="fb758-130">Klicken Sie auf dem Blatt **Virtueller Computer** unter **EINSTELLUNGEN** auf **Datenträger**.</span><span class="sxs-lookup"><span data-stu-id="fb758-130">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="fb758-131">Beachten Sie auf dem Blatt **Datenträger**, dass der Verschlüsselungsstatus des Betriebssystem-Datenträgers aktuell **Nicht aktiviert** ist, und klicken Sie dann auf **Datenträger hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-131">On the **Disks** blade, note that the OS disk encryption status is currently **Not enabled**, and then click **Add data disk**.</span></span>

1. <span data-ttu-id="fb758-132">Klicken Sie in die Liste **Namen**, und klicken Sie dann auf **Datenträger erstellen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-132">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="fb758-133">Geben Sie auf dem Blatt **Verwalteten Datenträger erstellen** im Feld **Name** **moneyappsvr01_data** ein.</span><span class="sxs-lookup"><span data-stu-id="fb758-133">In the **Create managed disk** blade, in the **Name** box, type **moneyappsvr01_data**.</span></span>

1. <span data-ttu-id="fb758-134">Wählen Sie unter **Ressourcengruppe** **Vorhandene verwenden** aus, und wählen Sie in der Liste **moneyapprg** aus.</span><span class="sxs-lookup"><span data-stu-id="fb758-134">Under **Resource Group**, select **Use existing**, and in the list, select **moneyapprg**.</span></span>

1. <span data-ttu-id="fb758-135">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-135">Click **Create**.</span></span>

1. <span data-ttu-id="fb758-136">Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="fb758-136">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="fb758-137">Klicken Sie auf dem Blatt **Datenträger** auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="fb758-137">On the **Disks** blade, click **Save**.</span></span> <span data-ttu-id="fb758-138">Beachten Sie, dass der Verschlüsselungsstatus des Datenträgers aktuell **_Nicht aktiviert_** ist.</span><span class="sxs-lookup"><span data-stu-id="fb758-138">Note that the data disk encryption status is currently **_Not enabled_**.</span></span>

## <a name="configure-disk-encryption-pre-requisites"></a><span data-ttu-id="fb758-139">Voraussetzungen zum Konfigurieren der Datenträgerverschlüsselung</span><span class="sxs-lookup"><span data-stu-id="fb758-139">Configure disk encryption pre-requisites</span></span>

<span data-ttu-id="fb758-140">Sie verwenden jetzt das Konfigurationsskript für die Voraussetzungen zum Konfigurieren der Azure-Datenträgerverschlüsselung, um alle Voraussetzungen für die Datenträgerverschlüsselung zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="fb758-140">You'll now use the Azure disk encryption prerequisites configuration script to configure all the disk encryption pre-requisites.</span></span> <span data-ttu-id="fb758-141">Durch dieses Skript wird ein Key Vault in der gleichen Region wie Ihre VM erstellt und vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="fb758-141">This script will create and prepare a Key Vault in the same region as your VM.</span></span>

### <a name="prepare-the-azure-disk-encryption-prerequisite-setup-script"></a><span data-ttu-id="fb758-142">Vorbereiten des Setupskripts für Azure Disk Encryption – Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="fb758-142">Prepare the Azure Disk Encryption Prerequisite Setup Script</span></span>

1. <span data-ttu-id="fb758-143">Navigieren Sie zur GitHub-Seite [Azure Disk Encryption Prerequisite Setup Script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) (Setupskript für Azure Disk Encryption – Voraussetzungen).</span><span class="sxs-lookup"><span data-stu-id="fb758-143">Go to the [Azure Disk Encryption Prerequisite Setup Script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)  GitHub page.</span></span>

1. <span data-ttu-id="fb758-144">Klicken Sie auf der GibHub-Seite auf **Raw** (unformatiert).</span><span class="sxs-lookup"><span data-stu-id="fb758-144">On the GibHub page, click **Raw**.</span></span>

1. <span data-ttu-id="fb758-145">Verwenden Sie STRG+A, um den gesamten Text auf der Seite auszuwählen, und anschließend STRG+C, um den gesamten Text auf der Seite in die Zwischenablage zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="fb758-145">Use CTRL-A to select all the text on the page and then use CTRL-C to copy all the text on the page to the clipboard.</span></span>

1. <span data-ttu-id="fb758-146">Klicken Sie auf Ihrem Computer auf **Start**, und suchen Sie dann nach **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="fb758-146">On your computer, click **Start**, then browse to **Windows PowerShell ISE**.</span></span>

1. <span data-ttu-id="fb758-147">Klicken Sie mit der rechten Maustaste auf **Windows PowerShell ISE** und anschließend auf **Als Administrator ausführen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-147">Right click **Windows PowerShell ISE** and click **Run as administrator**.</span></span>

1. <span data-ttu-id="fb758-148">Klicken Sie im Fenster „Administrator: Windows PowerShell ISE“ auf **Ansicht** und anschließend auf **Skriptbereich anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-148">In the Administrator: Windows PowerShell ISE window, click **View** and then click **Show Script Pane**.</span></span>

1. <span data-ttu-id="fb758-149">Fügen Sie den kopierten Text in den Skriptbereich ein.</span><span class="sxs-lookup"><span data-stu-id="fb758-149">Paste the copied text into the script pane.</span></span>

1. <span data-ttu-id="fb758-150">Suchen Sie im Skriptbereich nach dem folgenden Codeblock:</span><span class="sxs-lookup"><span data-stu-id="fb758-150">In the script pane, locate the following block of code:</span></span>

    ```powershell
    [Parameter(Mandatory = $false,
            HelpMessage="Name of the AAD application that will be used to write secrets to KeyVault. A new application with this name will be created if one doesn't exist. If this app already exists, pass aadClientSecret parameter to the script")]
    [ValidateNotNullOrEmpty()]
    [string]$aadAppName,
    ```
1. <span data-ttu-id="fb758-151">Ändern Sie im Codeblock `$false` in `$true`.</span><span class="sxs-lookup"><span data-stu-id="fb758-151">In the code block, change `$false` to `$true`.</span></span>

1. <span data-ttu-id="fb758-152">Klicken Sie auf **Datei**, klicken Sie dann auf **Speichern**, und navigieren Sie zu dem Ordner, den Sie zum Speichern des Skripts verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="fb758-152">Click **File**, then click **Save As**, and navigate to the folder you'd like to use to save the script.</span></span>

1. <span data-ttu-id="fb758-153">Geben Sie im Feld **Dateiname** **ADEPrereqScript.ps1** ein, und klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="fb758-153">In the **File name** box, type **ADEPrereqScript.ps1**, and click **Save**.</span></span>

### <a name="run-the-azure-disk-encryption-prerequisite-setup-script"></a><span data-ttu-id="fb758-154">Ausführen des Setupskripts für Azure Disk Encryption – Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="fb758-154">Run the Azure Disk Encryption Prerequisite Setup Script</span></span>

1. <span data-ttu-id="fb758-155">Geben Sie im Bereich der PowerShell ISE-Konsole den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="fb758-155">In the  PowerShell ISE console pane, type the following command, and press **ENTER**:</span></span>

   ```console
   cd <path to your folder containing ADEPrereqScript.ps1>
   ```

1. <span data-ttu-id="fb758-156">Geben Sie im Bereich der PowerShell ISE-Konsole den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="fb758-156">In the PowerShell ISE console pane, type the following command, and press **ENTER**:</span></span>

   ```powershell
   Set-ExecutionPolicy Unrestricted
   ```

   <span data-ttu-id="fb758-157">Wenn ein Dialogfeld **Ausführungsrichtlinie ändern** angezeigt wird, klicken Sie entweder auf **Alle ja** oder auf **Ja** (wenn die Option _Alle ja_ nicht angezeigt wird).</span><span class="sxs-lookup"><span data-stu-id="fb758-157">If you get an **Execution Policy Change** dialog box, click either **Yes to all** or **Yes** (if you do not get a _Yes to all_ option).</span></span>

1. <span data-ttu-id="fb758-158">Geben Sie im Bereich der PowerShell ISE-Konsole den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="fb758-158">In the  PowerShell ISE console pane, type the following command, and press **ENTER**:</span></span>

   ```powershell
   Login-AzureRmAccount
   ```

1. <span data-ttu-id="fb758-159">Geben Sie Ihre Azure-Anmeldeinformationen ein.</span><span class="sxs-lookup"><span data-stu-id="fb758-159">Enter your Azure credentials.</span></span>

1. <span data-ttu-id="fb758-160">Wählen Sie Ihre **Abonnement-ID**-Zeichenfolge aus, und kopieren Sie sie in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="fb758-160">Select your **SubscriptionId** string, and copy it to the clipboard.</span></span>

1. <span data-ttu-id="fb758-161">Klicken Sie in der PowerShell ISE auf **Datei** und dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="fb758-161">In the  PowerShell ISE, click **File**, and then click **Run**.</span></span>

1. <span data-ttu-id="fb758-162">Geben Sie im Konsolenfenster an der Aufforderung **resourceGroupName:** **moneyapprg** ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="fb758-162">In the console pane, at the **resourceGroupName:** prompt, type  **moneyapprg**, and press **ENTER**.</span></span>

1. <span data-ttu-id="fb758-163">Geben Sie im Konsolenfenster an der Aufforderung **keyVaultName:** **moneyappkv** ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="fb758-163">In the console pane, at the **keyVaultName:** prompt, type **moneyappkv**, and press **ENTER**.</span></span>

1. <span data-ttu-id="fb758-164">Geben Sie im Konsolenfenster an der Aufforderung **location:** den Speicherort ein, den Sie beim Erstellen Ihrer VM verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="fb758-164">In the console pane, at the **location:** prompt, type the location you used when creating your VM.</span></span>

1. <span data-ttu-id="fb758-165">Fügen Sie im Konsolenfenster an der Aufforderung **subscriptionId:** Ihre Abonnement-ID ein.</span><span class="sxs-lookup"><span data-stu-id="fb758-165">In the console pane, at the **subscriptionId:** prompt, paste your subscription ID.</span></span>

1. <span data-ttu-id="fb758-166">Der **moneyappkv**-Schlüsseltresor wird jetzt erstellt.</span><span class="sxs-lookup"><span data-stu-id="fb758-166">The **moneyappkv** key vault will now be created.</span></span> <span data-ttu-id="fb758-167">Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in Editor.</span><span class="sxs-lookup"><span data-stu-id="fb758-167">When this has completed, select the summary text (in green), and copy it to Notepad.</span></span>

1. <span data-ttu-id="fb758-168">Drücken Sie die **EINGABETASTE**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="fb758-168">Press **ENTER** to continue.</span></span>

1. <span data-ttu-id="fb758-169">Geben Sie im Konsolenfenster an der Aufforderung **aadAppName:** **moneyapp** ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="fb758-169">In the console pane, at the **aadAppName:**  prompt, type **moneyapp**, and press **ENTER**.</span></span>

1. <span data-ttu-id="fb758-170">Die Azure AD-Anwendung **moneyapp** wird jetzt erstellt.</span><span class="sxs-lookup"><span data-stu-id="fb758-170">The **moneyapp** Azure AD application will now be created.</span></span> <span data-ttu-id="fb758-171">Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in Editor.</span><span class="sxs-lookup"><span data-stu-id="fb758-171">When this has completed, select the summary text (in green), and copy it to Notepad.</span></span>

1. <span data-ttu-id="fb758-172">Drücken Sie die **EINGABETASTE**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="fb758-172">Press **ENTER** to continue.</span></span>

### <a name="encrypt-your-vm-disks-with-powershell"></a><span data-ttu-id="fb758-173">Verschlüsseln Ihrer VM-Datenträger mit PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb758-173">Encrypt your VM disks with PowerShell</span></span>

<span data-ttu-id="fb758-174">Überprüfen Sie den Verschlüsselungsstatus der Betriebssystem- und Daten-Datenträger:</span><span class="sxs-lookup"><span data-stu-id="fb758-174">Verify the encryption status of the OS and data disks:</span></span>

1. <span data-ttu-id="fb758-175">Geben Sie im PowerShell ISE-Konsolenfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="fb758-175">In the PowerShell ISE console pane, type the following command, and press ENTER:</span></span>

    ```powershell
    $vmName = 'moneyappsvr01'
    ```

    > [!NOTE]
    > <span data-ttu-id="fb758-176">Der Name der VM muss in einfache Anführungszeichen eingeschlossen sein.</span><span class="sxs-lookup"><span data-stu-id="fb758-176">The VM name must be enclosed in single quotes.</span></span>

1. <span data-ttu-id="fb758-177">Geben Sie im PowerShell ISE-Skriptfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="fb758-177">In the PowerShell ISE script pane, enter the following command, and press ENTER:</span></span>

    ```powershell
    Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
    ```

1. <span data-ttu-id="fb758-178">Klicken Sie im Dialogfeld **Enable AzureDiskEncryption on the VM** (Azure-Datenträgerverschlüsselung für die VM aktivieren) auf **Ja**, und achten Sie auf die Nachricht, dass der Abschluss der Verschlüsselung 10–15 Minuten in Anspruch nehmen kann.</span><span class="sxs-lookup"><span data-stu-id="fb758-178">In the **Enable AzureDiskEncryption on the VM** dialog box, click **Yes**, and note the message that encryption may take 10-15 minutes to complete.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="fb758-179">Warten Sie auf den Abschluss des Befehls, bevor Sie mit dieser Übung fortfahren</span><span class="sxs-lookup"><span data-stu-id="fb758-179">Wait until the command has completed before continuing with this exercise</span></span>

### <a name="verify-the-encryption-status-of-your-vm-disks"></a><span data-ttu-id="fb758-180">Überprüfen des Verschlüsselungsstatus Ihrer VM-Datenträger</span><span class="sxs-lookup"><span data-stu-id="fb758-180">Verify the encryption status of your VM disks</span></span>

<span data-ttu-id="fb758-181">Wechseln Sie zum Azure-Portal, und beachten Sie auf dem Blatt **Datenträger** für **moneyappsvr01**, dass der Datenträger-Verschlüsselungsstatus für die Betriebssystem- und Daten-Datenträger jetzt **Aktiviert** ist.</span><span class="sxs-lookup"><span data-stu-id="fb758-181">Switch to the Azure portal, and on the **Disks** blade for **moneyappsvr01**, note that the disk encryption status for the OS and Data disks is now **Enabled**.</span></span>
