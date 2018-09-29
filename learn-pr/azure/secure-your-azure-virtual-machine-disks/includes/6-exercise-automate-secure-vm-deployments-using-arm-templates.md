<span data-ttu-id="feb60-101">In dieser Einheit verwenden Sie eine Azure Resource Manager-Vorlage, um den virtuellen Windows-Computer zu entschlüsseln, den Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="feb60-101">In this unit, you'll use an Azure Resource Manager template to decrypt our Windows VM we created earlier.</span></span> <span data-ttu-id="feb60-102">Sie haben das Betriebssystemlaufwerk Ihres virtuellen Windows-Computers verschlüsselt.</span><span class="sxs-lookup"><span data-stu-id="feb60-102">We encrypted the OS drive on our Windows VM.</span></span> <span data-ttu-id="feb60-103">Da sich auf dem Betriebssystemlaufwerk allerdings keine vertraulichen Informationen befinden, können Sie es eigentlich auch unverschlüsselt lassen.</span><span class="sxs-lookup"><span data-stu-id="feb60-103">However, the OS drive won't have any confidential information on it, so we could leave it unencrypted.</span></span> <span data-ttu-id="feb60-104">Sie verwenden daher eine Vorlage, um lediglich das Betriebssystemlaufwerk zu entschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="feb60-104">Let's use a template to decrypt the OS drive.</span></span>

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a><span data-ttu-id="feb60-105">Konfigurieren und Bereitstellen eines neuen virtuellen Computers mithilfe einer Azure Resource Manager-Vorlage</span><span class="sxs-lookup"><span data-stu-id="feb60-105">Configure and deploy a new VM using an Azure Resource Manager template</span></span>

<span data-ttu-id="feb60-106">Mithilfe einer Vorlage, die Microsoft auf Github veröffentlicht hat, erstellen wir einen neuen virtuellen Computer mit standardmäßig aktivierter Verschlüsselung.</span><span class="sxs-lookup"><span data-stu-id="feb60-106">We're going to use a template Microsoft has published on Github to create a new VM with encryption turned on by default.</span></span>

1. <span data-ttu-id="feb60-107">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, mit dem Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="feb60-107">Sign into the [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) with the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="feb60-108">Klicken Sie auf der linken Seitenleiste auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="feb60-108">Click **Create a Resource** in the left sidebar.</span></span>

1. <span data-ttu-id="feb60-109">Geben Sie **Vorlage** in das Suchfeld ein.</span><span class="sxs-lookup"><span data-stu-id="feb60-109">Type **Template** in the search box.</span></span>

1. <span data-ttu-id="feb60-110">Wählen Sie in der Liste mit den Ergebnissen die Option **Vorlagenbereitstellung** aus, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="feb60-110">Select **Template Deployment** from the resulting list and click **Create**.</span></span>

    ![Screenshot, auf dem das Element „Vorlagenbereitstellung“ ausgewählt und die Schaltfläche „Erstellen“ hervorgehoben ist.](../media/6-create-template.png)

1. <span data-ttu-id="feb60-112">Geben Sie „201-decrypt“ in das **Vorlagenauswahlfeld**ein, und wählen Sie die Vorlage „201-decrypt-running-windows-vm-without-aad“ aus.</span><span class="sxs-lookup"><span data-stu-id="feb60-112">In the **Select a template** search box, start typing "201-decrypt" and select the "201-decrypt-running-windows-vm-without-aad" template.</span></span>

    ![Screenshot des Vorlagenauswahlfelds mit automatischer Vervollständigung.](../media/6-custom-deployment.png)

1. <span data-ttu-id="feb60-114">Klicken Sie auf **Vorlage auswählen**, um die Vorlagenausführung zu starten.</span><span class="sxs-lookup"><span data-stu-id="feb60-114">Click **Select Template** to launch the template runner.</span></span>

1. <span data-ttu-id="feb60-115">Geben Sie in der Einstellungsansicht folgende Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="feb60-115">In the settings view, enter the following information:</span></span>
    - <span data-ttu-id="feb60-116">Wählen Sie unter **Abonnement** die Option _Concierge-Abonnement_ aus.</span><span class="sxs-lookup"><span data-stu-id="feb60-116">Select _Concierge Subscription_ for the **Subscription**.</span></span>
    - <span data-ttu-id="feb60-117">Wählen Sie Ihre in der Sandbox erstellte Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="feb60-117">Select your Resource Group, created in the sandbox.</span></span>
    - <span data-ttu-id="feb60-118">Wählen Sie den Standort aus, an dem Sie den virtuellen Computer erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="feb60-118">Select the location you created the VM in.</span></span>
    - <span data-ttu-id="feb60-119">Geben Sie „fmdata-vm01“ als **VM-Namen** ein.</span><span class="sxs-lookup"><span data-stu-id="feb60-119">Enter "fmdata-vm01" for the **VM Name**.</span></span>
    - <span data-ttu-id="feb60-120">Übernehmen Sie für den **Volumetyp** die Einstellung _Alle_.</span><span class="sxs-lookup"><span data-stu-id="feb60-120">Leave the **Volume Type** as _All_.</span></span>

1. <span data-ttu-id="feb60-121">Aktivieren Sie das Kontrollkästchen **I agree to the terms and conditions** (Ich stimme den oben genannten Geschäftsbedingungen zu).</span><span class="sxs-lookup"><span data-stu-id="feb60-121">Select the **I agree to the terms and conditions** check box.</span></span>
1. <span data-ttu-id="feb60-122">Klicken Sie auf **Kaufen**, um die Vorlage auszuführen.</span><span class="sxs-lookup"><span data-stu-id="feb60-122">Click **Purchase** to run the template.</span></span> <span data-ttu-id="feb60-123">Hinweis: Dadurch entstehen Ihnen keine Kosten. Es handelt sich lediglich um eine Standardschaltfläche.</span><span class="sxs-lookup"><span data-stu-id="feb60-123">Note that there is no cost to this - it's a standard button.</span></span>

<span data-ttu-id="feb60-124">Die Bereitstellung kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="feb60-124">The deployment may take a few minutes to complete.</span></span>

## <a name="verify-the-encryption-status-of-the-vm"></a><span data-ttu-id="feb60-125">Überprüfen des Verschlüsselungsstatus des virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="feb60-125">Verify the encryption status of the VM</span></span>

1. <span data-ttu-id="feb60-126">Klicken Sie auf der Seitenleiste im Azure-Portal auf **Virtuelle Computer**, und wählen Sie Ihre VM **fmdata-vm01** aus.</span><span class="sxs-lookup"><span data-stu-id="feb60-126">In the sidebar of the Azure portal, click **Virtual machines** and select your VM **fmdata-vm01**.</span></span> <span data-ttu-id="feb60-127">Alternativ können Sie nach Ihrer VM anhand des Namens in **Alle Ressourcen** suchen.</span><span class="sxs-lookup"><span data-stu-id="feb60-127">Alternatively, you can search for your VM by name from **All Resources**.</span></span>

1. <span data-ttu-id="feb60-128">Klicken Sie auf dem Blatt **Virtueller Computer** unter **EINSTELLUNGEN** auf **Datenträger**.</span><span class="sxs-lookup"><span data-stu-id="feb60-128">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="feb60-129">Wie Sie auf dem Blatt **Datenträger** sehen, hat der Betriebssystemdatenträger nun den Verschlüsselungsstatus **Deaktiviert**.</span><span class="sxs-lookup"><span data-stu-id="feb60-129">On the **Disks** blade, notice the OS disk encryption status is now **Disabled**.</span></span>
