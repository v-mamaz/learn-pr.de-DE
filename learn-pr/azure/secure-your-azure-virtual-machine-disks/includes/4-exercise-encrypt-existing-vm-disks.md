<span data-ttu-id="d4c5d-101">Angenommen, Sie entwickeln eine Anwendung zur Finanzverwaltung für neue Startupunternehmen.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-101">Suppose you are developing a financial management application for new business startups.</span></span> <span data-ttu-id="d4c5d-102">Sie möchten sicherstellen, dass all ihre Kundendaten geschützt sind. Daher haben Sie sich entschieden, Azure Disk Encryption (ADE) durchgängig für alle (Betriebssystem-)Datenträger auf den Servern einzusetzen, auf denen die Anwendung gehostet ist.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-102">You want to ensure that all your customers' data is secured, so you have decided to implement Azure Disk Encryption (ADE) across all OS and data disks on the servers that will host this application.</span></span> <span data-ttu-id="d4c5d-103">Im Rahmen Ihrer Complianceanforderungen müssen Sie außerdem selbst für die Verwaltung Ihrer eigenen Verschlüsselungsschlüssel zuständig sein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-103">As part of your compliance requirements, you also need to be responsible for your own encryption key management.</span></span>

<span data-ttu-id="d4c5d-104">In dieser Einheit verschlüsseln Sie Datenträger auf vorhandenen Windows-VMs und verwalten die Verschlüsselungsschlüssel mithilfe Ihrer eigenen Azure Key Vault-Instanz.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-104">In this unit, you'll encrypt disks on existing Windows VMs, and manage the encryption keys using your own Azure Key Vault.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d4c5d-105">Bei dieser Übung wird davon ausgegangen, dass Azure PowerShell auf Ihrem Computer installiert ist.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-105">This exercise assumes that Azure PowerShell is installed on your computer.</span></span> <span data-ttu-id="d4c5d-106">Informationen zum Installieren von Azure PowerShell finden Sie unter [Installieren von Azure PowerShell unter Windows mit PowerShellGet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0).</span><span class="sxs-lookup"><span data-stu-id="d4c5d-106">Go to [Install Azure PowerShell on Windows with PowerShellGet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0) for information on how to install Azure PowerShell.</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="d4c5d-107">Vorbereiten der Umgebung</span><span class="sxs-lookup"><span data-stu-id="d4c5d-107">Prepare the environment</span></span>

<span data-ttu-id="d4c5d-108">Wir beginnen, indem wir eine Windows-VM in einer neuen Ressourcengruppe bereitstellen und dann der VM einen Datenträger hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-108">We'll start by deploying a Windows VM to a new resource group, and then add a data disk to the VM.</span></span>

### <a name="deploy-windows-vm-using-the-azure-portal"></a><span data-ttu-id="d4c5d-109">Bereitstellen eines virtuellen Windows-Computers über das Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="d4c5d-109">Deploy Windows VM using the Azure portal</span></span>

<span data-ttu-id="d4c5d-110">Hier verwenden Sie das Azure-Portal, um einen virtuellen Windows-Computer zu erstellen und bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-110">Here you'll use the Azure portal to create and deploy a Windows VM.</span></span> <span data-ttu-id="d4c5d-111">Definieren Sie zunächst die grundlegenden Informationen für den virtuellen Computer:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-111">Start by defining the basic VM information:</span></span>

1. <span data-ttu-id="d4c5d-112">Navigieren Sie im Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren normalen Anmeldeinformationen an.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-112">In a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>

1. <span data-ttu-id="d4c5d-113">Klicken Sie auf der Randleiste auf **Virtuelle Computer**, und klicken Sie dann auf **Virtuellen Computer erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-113">In the sidebar, click **Virtual machines**, and then click **Create virtual machine**.</span></span>

1. <span data-ttu-id="d4c5d-114">Klicken Sie auf dem Blatt „Compute“ im Abschnitt **Empfohlen** auf **Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-114">On the Compute blade, in the **Recommended** section, click **Windows Server**.</span></span>

1. <span data-ttu-id="d4c5d-115">Klicken Sie auf dem Blatt **Windows Server** auf **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-115">In the **Windows Server** blade, click **Windows Server 2016 Datacenter**.</span></span>

1. <span data-ttu-id="d4c5d-116">Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-116">In the **Windows Server 2016 Datacenter** blade, click **Create**.</span></span>

1. <span data-ttu-id="d4c5d-117">Geben Sie auf dem Blatt **Grundlagen** im Feld **Name** **moneyappsvr01** ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-117">In the **Basics** blade, in the **Name** box, type **moneyappsvr01.**</span></span>

1. <span data-ttu-id="d4c5d-118">Geben Sie in den Feldern **Benutzername** und **Kennwort** einen Namen und ein Kennwort für ein Administratorkonto auf diesem Server ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-118">In the **Username** and **Password boxes**, type a name and password for an administrator account on this server.</span></span>

1. <span data-ttu-id="d4c5d-119">Wählen Sie im Feld **Abonnement** Ihr Azure-Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-119">In the **Subscription** box, select your Azure subscription.</span></span>

1. <span data-ttu-id="d4c5d-120">Klicken Sie unter **Ressourcengruppe** auf die Option **Neu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-120">Under **Resource Group**, select **Create new**.</span></span> <span data-ttu-id="d4c5d-121">Geben Sie im Feld **moneyapprg** ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-121">In the box, type **moneyapprg**.</span></span>

1. <span data-ttu-id="d4c5d-122">Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-122">In the **Location** drop-down list, select a region near you.</span></span>

1. <span data-ttu-id="d4c5d-123">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-123">Click **OK**.</span></span>

### <a name="choose-a-size-for-the-vm-and-start-the-deployment"></a><span data-ttu-id="d4c5d-124">Wählen Sie eine Größe für die VM aus, und beginnen Sie mit der Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-124">Choose a size for the VM, and start the deployment</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4c5d-125">Beachten Sie, dass ADE im Basic-Tarif nicht unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-125">Remember that basic tier VMs do not support ADE.</span></span>

1. <span data-ttu-id="d4c5d-126">Wählen Sie auf dem Blatt **Größe auswählen** eine **Standard**-SKU aus, z.B. **B1s**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-126">On the **Choose a size** blade, select a **Standard** SKU, such as **B1s**.</span></span> <span data-ttu-id="d4c5d-127">Klicken Sie dann auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-127">Then click **Select**.</span></span>

1. <span data-ttu-id="d4c5d-128">Klicken Sie auf dem Blatt **Einstellungen** in der Liste **Öffentliche Eingangsports hinzufügen** auf **RDP**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-128">On the **Settings** blade, in the **Select public inbound ports** list, click **RDP**.</span></span> <span data-ttu-id="d4c5d-129">Scrollen Sie anschließend nach unten, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-129">Then scroll down and click **OK**.</span></span>

1. <span data-ttu-id="d4c5d-130">Klicken Sie auf dem Blatt **Erstellen** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-130">On the **Create** blade, click **Create**.</span></span>

1. <span data-ttu-id="d4c5d-131">Warten Sie die Bereitstellung des virtuellen Computers ab, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-131">Wait until the VM has deployed before continuing with the exercise.</span></span>

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="d4c5d-132">Hinzufügen eines Datenträgers zur VM</span><span class="sxs-lookup"><span data-stu-id="d4c5d-132">Add a data disk to the VM</span></span>

1. <span data-ttu-id="d4c5d-133">Klicken Sie im linken Menü auf **Alle Ressourcen** und dann auf **moneyappsvr01**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-133">In the left menu, click **All resources**, and then click **moneyappsvr01**.</span></span>

1. <span data-ttu-id="d4c5d-134">Klicken Sie auf dem Blatt **Virtueller Computer** unter **EINSTELLUNGEN** auf **Datenträger**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-134">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="d4c5d-135">Beachten Sie auf dem Blatt **Datenträger**, dass der Verschlüsselungsstatus des Betriebssystem-Datenträgers aktuell **Nicht aktiviert** ist, und klicken Sie dann auf **Datenträger hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-135">On the **Disks** blade, note that the OS disk encryption status is currently **Not enabled**, and then click **Add data disk**.</span></span>

1. <span data-ttu-id="d4c5d-136">Klicken Sie in die Liste **Namen**, und klicken Sie dann auf **Datenträger erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-136">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="d4c5d-137">Geben Sie auf dem Blatt **Verwalteten Datenträger erstellen** im Feld **Name** **moneyappsvr01_data** ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-137">In the **Create managed disk** blade, in the **Name** box, type **moneyappsvr01_data**.</span></span>

1. <span data-ttu-id="d4c5d-138">Wählen Sie unter **Ressourcengruppe** **Vorhandene verwenden** aus, und wählen Sie in der Liste **moneyapprg** aus.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-138">Under **Resource Group**, select **Use existing**, and in the list, select **moneyapprg**.</span></span>

1. <span data-ttu-id="d4c5d-139">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-139">Click **Create**.</span></span>

1. <span data-ttu-id="d4c5d-140">Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-140">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="d4c5d-141">Klicken Sie auf dem Blatt **Datenträger** auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-141">On the **Disks** blade, click **Save**.</span></span> <span data-ttu-id="d4c5d-142">Beachten Sie, dass der Verschlüsselungsstatus des Datenträgers aktuell **Nicht aktiviert** ist.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-142">Note that the data disk encryption status is currently **Not enabled**.</span></span>

## <a name="configure-disk-encryption-prerequisites"></a><span data-ttu-id="d4c5d-143">Konfigurieren der erforderlichen Komponenten für die Datenträgerverschlüsselung</span><span class="sxs-lookup"><span data-stu-id="d4c5d-143">Configure disk encryption prerequisites</span></span>

<span data-ttu-id="d4c5d-144">Mit dem Konfigurationsskript konfigurieren Sie im Folgenden alle Komponenten, die für die Datenträgerverschlüsselung mittels Azure Disk Encryption erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-144">You'll now use the Azure Disk Encryption prerequisites configuration script to configure all the disk encryption prerequisites.</span></span> <span data-ttu-id="d4c5d-145">Durch dieses Skript wird ein Schlüsseltresor in der gleichen Region, in der sich auch die VM befindet, erstellt und vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-145">This script will create and prepare a key vault in the same region as your VM.</span></span>

### <a name="prepare-the-azure-disk-encryption-prerequisite-setup-script"></a><span data-ttu-id="d4c5d-146">Vorbereiten des Einrichtungsskripts für erforderliche Komponenten von Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="d4c5d-146">Prepare the Azure Disk Encryption prerequisite setup script</span></span>

1. <span data-ttu-id="d4c5d-147">Navigieren Sie zur GitHub-Seite [Azure Disk Encryption Prerequisite Setup Script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) (Einrichtungsskript für erforderliche Komponenten von Azure Disk Encryption).</span><span class="sxs-lookup"><span data-stu-id="d4c5d-147">Go to the [Azure Disk Encryption prerequisite setup script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) GitHub page.</span></span>

1. <span data-ttu-id="d4c5d-148">Klicken Sie auf der GibHub-Seite auf **Raw** (Unformatiert).</span><span class="sxs-lookup"><span data-stu-id="d4c5d-148">On the GibHub page, click **Raw**.</span></span>

1. <span data-ttu-id="d4c5d-149">Drücken Sie STRG+A, um den gesamten Text auf der Seite auszuwählen, und anschließend STRG+C, um den gesamten Text auf der Seite in die Zwischenablage zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-149">Use Ctrl-A to select all the text on the page, and then use Ctrl-C to copy all the text on the page to the clipboard.</span></span>

1. <span data-ttu-id="d4c5d-150">Klicken Sie auf Ihrem Computer auf **Start**, und suchen Sie dann nach **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-150">On your computer, click **Start**, and then browse to **Windows PowerShell ISE**.</span></span>

1. <span data-ttu-id="d4c5d-151">Klicken Sie mit der rechten Maustaste auf **Windows PowerShell ISE** und anschließend auf **Als Administrator ausführen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-151">Right-click **Windows PowerShell ISE**, and click **Run as administrator**.</span></span>

1. <span data-ttu-id="d4c5d-152">Klicken Sie im Fenster „Administrator: Windows PowerShell ISE“ auf **Ansicht** und anschließend auf **Skriptbereich anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-152">In the Administrator: Windows PowerShell ISE window, click **View**, and then click **Show Script Pane**.</span></span>

1. <span data-ttu-id="d4c5d-153">Fügen Sie den kopierten Text in den Skriptbereich ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-153">Paste the copied text into the script pane.</span></span>

1. <span data-ttu-id="d4c5d-154">Suchen Sie im Skriptbereich nach dem folgenden Codeblock:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-154">In the script pane, locate the following block of code:</span></span>

    ```powershell
    [Parameter(Mandatory = $false,
            HelpMessage="Name of the AAD application that will be used to write secrets to KeyVault. A new application with this name will be created if one doesn't exist. If this app already exists, pass aadClientSecret parameter to the script")]
    [ValidateNotNullOrEmpty()]
    [string]$aadAppName,
    ```
1. <span data-ttu-id="d4c5d-155">Ändern Sie im Codeblock `$false` in `$true`.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-155">In the code block, change `$false` to `$true`.</span></span>

1. <span data-ttu-id="d4c5d-156">Klicken Sie auf **Datei**, klicken Sie dann auf **Speichern**, und navigieren Sie zu dem Ordner, den Sie zum Speichern des Skripts verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-156">Click **File**, then click **Save As**, and navigate to the folder you'd like to use to save the script.</span></span>

1. <span data-ttu-id="d4c5d-157">Geben Sie im Feld **Dateiname** **ADEPrereqScript.ps1** ein, und klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-157">In the **File name** box, type **ADEPrereqScript.ps1**, and click **Save**.</span></span>

### <a name="run-the-azure-disk-encryption-prerequisite-setup-script"></a><span data-ttu-id="d4c5d-158">Ausführen des Einrichtungsskripts für die erforderlichen Komponenten von Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="d4c5d-158">Run the Azure Disk Encryption prerequisite setup script</span></span>

1. <span data-ttu-id="d4c5d-159">Geben Sie im PowerShell ISE-Konsolenbereich den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-159">In the  PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

   ```console
   cd <path to your folder containing ADEPrereqScript.ps1>
   ```

1. <span data-ttu-id="d4c5d-160">Geben Sie im PowerShell ISE-Konsolenbereich den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-160">In the PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

   ```powershell
   Set-ExecutionPolicy Unrestricted
   ```

   <span data-ttu-id="d4c5d-161">Wenn das Dialogfeld **Ausführungsrichtlinie ändern** angezeigt wird, klicken Sie entweder auf **Ja, alle** oder auf **Ja** (wenn die Option _Ja, alle_ nicht angezeigt wird).</span><span class="sxs-lookup"><span data-stu-id="d4c5d-161">If you get an **Execution Policy Change** dialog box, click either **Yes to all** or **Yes** (if you do not get a _Yes to all_ option).</span></span>

1. <span data-ttu-id="d4c5d-162">Geben Sie im PowerShell ISE-Konsolenbereich den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-162">In the  PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

   ```powershell
   Login-AzureRmAccount
   ```

1. <span data-ttu-id="d4c5d-163">Geben Sie Ihre Azure-Anmeldeinformationen ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-163">Enter your Azure credentials.</span></span>

1. <span data-ttu-id="d4c5d-164">Wählen Sie Ihre **Abonnement-ID**-Zeichenfolge aus, und kopieren Sie sie in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-164">Select your **SubscriptionId** string, and copy it to the clipboard.</span></span>

1. <span data-ttu-id="d4c5d-165">Klicken Sie in der PowerShell ISE auf **Datei** und dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-165">In the PowerShell ISE, click **File**, and then click **Run**.</span></span>

1. <span data-ttu-id="d4c5d-166">Geben Sie im Konsolenbereich nach der Eingabeaufforderung **resourceGroupName:** **moneyapprg** ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-166">In the console pane, at the **resourceGroupName:** prompt, type  **moneyapprg**.</span></span> <span data-ttu-id="d4c5d-167">Drücken Sie anschließend die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-167">Then press **Enter**.</span></span>

1. <span data-ttu-id="d4c5d-168">Geben Sie im Konsolenfenster nach der Eingabeaufforderung **keyVaultName:** **moneyappkv** ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-168">In the console pane, at the **keyVaultName:** prompt, type **moneyappkv**.</span></span> <span data-ttu-id="d4c5d-169">Drücken Sie anschließend die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-169">Then press **Enter**.</span></span>

1. <span data-ttu-id="d4c5d-170">Geben Sie im Konsolenfenster nach der Eingabeaufforderung **location:** den Speicherort ein, den Sie beim Erstellen Ihrer VM verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-170">In the console pane, at the **location:** prompt, type the location you used when creating your VM.</span></span>

1. <span data-ttu-id="d4c5d-171">Fügen Sie im Konsolenfenster an der Aufforderung **subscriptionId:** Ihre Abonnement-ID ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-171">In the console pane, at the **subscriptionId:** prompt, paste your subscription ID.</span></span>

1. <span data-ttu-id="d4c5d-172">Der **moneyappkv**-Schlüsseltresor wird jetzt erstellt.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-172">The **moneyappkv** key vault will now be created.</span></span> <span data-ttu-id="d4c5d-173">Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in den Editor.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-173">When this has completed, select the summary text (in green), and copy it to Notepad.</span></span>

1. <span data-ttu-id="d4c5d-174">Drücken Sie die **EINGABETASTE**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-174">Press **Enter** to continue.</span></span>

1. <span data-ttu-id="d4c5d-175">Geben Sie im Konsolenbereich nach der Eingabeaufforderung **aadAppName:** **moneyapp** ein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-175">In the console pane, at the **aadAppName:**  prompt, type **moneyapp**.</span></span> <span data-ttu-id="d4c5d-176">Drücken Sie anschließend die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-176">Then press **Enter**.</span></span>

1. <span data-ttu-id="d4c5d-177">Die Azure AD-Anwendung **moneyapp** wird jetzt erstellt.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-177">The **moneyapp** Azure AD application will now be created.</span></span> <span data-ttu-id="d4c5d-178">Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in den Editor.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-178">When this has completed, select the summary text (in green), and copy it to Notepad.</span></span>

1. <span data-ttu-id="d4c5d-179">Drücken Sie die **EINGABETASTE**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-179">Press **Enter** to continue.</span></span>

### <a name="encrypt-your-vm-disks-with-powershell"></a><span data-ttu-id="d4c5d-180">Verschlüsseln Ihrer VM-Datenträger mit PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4c5d-180">Encrypt your VM disks with PowerShell</span></span>

<span data-ttu-id="d4c5d-181">Überprüfen Sie den Verschlüsselungsstatus der (Betriebssystem-)Datenträger wie folgt:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-181">Verify the encryption status of the OS and data disks:</span></span>

1. <span data-ttu-id="d4c5d-182">Geben Sie im PowerShell ISE-Konsolenbereich den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-182">In the PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

    ```powershell
    $vmName = 'moneyappsvr01'
    ```

    > [!NOTE]
    > <span data-ttu-id="d4c5d-183">Der Name der VM muss in einfache Anführungszeichen eingeschlossen sein.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-183">The VM name must be enclosed in single quotes.</span></span>

1. <span data-ttu-id="d4c5d-184">Geben Sie im PowerShell ISE-Skriptbereich den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="d4c5d-184">In the PowerShell ISE script pane, enter the following command, and press **Enter**:</span></span>

    ```powershell
    Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
    ```

1. <span data-ttu-id="d4c5d-185">Klicken Sie im Dialogfeld **Enable AzureDiskEncryption on the VM** (Azure-Datenträgerverschlüsselung für die VM aktivieren) auf **Ja**. Sie werden in einer Nachricht darauf hingewiesen, dass der Abschluss der Verschlüsselung 10 bis 15 Minuten in Anspruch nehmen kann.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-185">In the **Enable AzureDiskEncryption on the VM** dialog box, click **Yes**, and note the message that encryption may take 10-15 minutes to complete.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="d4c5d-186">Warten Sie auf den Abschluss des Befehls, bevor Sie mit dieser Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-186">Wait until the command has completed before continuing with this exercise.</span></span>

### <a name="verify-the-encryption-status-of-your-vm-disks"></a><span data-ttu-id="d4c5d-187">Überprüfen des Verschlüsselungsstatus Ihrer VM-Datenträger</span><span class="sxs-lookup"><span data-stu-id="d4c5d-187">Verify the encryption status of your VM disks</span></span>

<span data-ttu-id="d4c5d-188">Wechseln Sie zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-188">Switch to the Azure portal.</span></span> <span data-ttu-id="d4c5d-189">Beachten Sie auf dem Blatt **Datenträger** für **moneyappsvr01**, dass als Verschlüsselungsstatus für die (Betriebssystem-)Datenträger jetzt **Aktiviert** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="d4c5d-189">On the **Disks** blade for **moneyappsvr01**, note that the disk encryption status for the OS and Data disks is now **Enabled**.</span></span>
