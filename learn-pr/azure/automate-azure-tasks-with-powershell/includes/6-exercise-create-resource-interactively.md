<span data-ttu-id="43c1e-101">Nehmen Sie an, Sie arbeiten in einem Unternehmen, das eine Sammlung von Linux-Verwaltungstools entwickelt.</span><span class="sxs-lookup"><span data-stu-id="43c1e-101">Suppose you work at a company that makes a suite of Linux admin tools.</span></span> <span data-ttu-id="43c1e-102">Ihre Aufgabe ist es, potenziellen Kunden vor dem Kauf Ihrer Software bei der Testphase zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="43c1e-102">Your job is to help potential customers try your software before they buy it.</span></span> <span data-ttu-id="43c1e-103">Da die Software Änderungen auf der Stammebene für das Betriebssystem vornimmt, haben Sie sich dazu entschlossen, für jeden Testkunden eine Linux-VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="43c1e-103">Because the software makes root-level changes to the OS, you have decided to create a Linux VM for each trial customer.</span></span> <span data-ttu-id="43c1e-104">Sie erstellen je nach Bedarf die VMs und löschen sie nach Ablauf des Testabonnements.</span><span class="sxs-lookup"><span data-stu-id="43c1e-104">You create the VMs as needed and delete them at the end of the trial subscription.</span></span> <span data-ttu-id="43c1e-105">Auf diese Weise führt jeder Kunde seine ersten Schritte mit einer bereinigten Betriebssystemversion durch.</span><span class="sxs-lookup"><span data-stu-id="43c1e-105">This way, each customer starts with a clean version of the OS.</span></span> 

<span data-ttu-id="43c1e-106">Damit diese VMs für interne Tests separat von den VMs Ihres Unternehmen verwaltet werden, erstellen Sie eine dedizierte Ressourcengruppe, um diese zu hosten.</span><span class="sxs-lookup"><span data-stu-id="43c1e-106">To keep these VMs separate from the VMs your company uses for internal testing, you will create a dedicated resource group to house them.</span></span> <span data-ttu-id="43c1e-107">Sie benötigen nur eine Ressourcengruppe. Daher ist die Verwendung von Azure PowerShell im interaktiven Modus die naheliegende Wahl für diese Aufgabe.</span><span class="sxs-lookup"><span data-stu-id="43c1e-107">You only need one resource group so using Azure PowerShell in interactive mode is a reasonable choice for this task.</span></span>

## <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="43c1e-108">Schritte zum Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="43c1e-108">Steps to create a resource group</span></span>

1. <span data-ttu-id="43c1e-109">Starten Sie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43c1e-109">Launch PowerShell.</span></span>

1. <span data-ttu-id="43c1e-110">Importieren Sie das Modul in die aktuelle Sitzung, damit Sie Zugriff auf die Azure-Cmdlets haben.</span><span class="sxs-lookup"><span data-stu-id="43c1e-110">Import the module into the current session so you have access to the Azure cmdlets.</span></span>

   ```powershell
   Import-Module AzureRM
   ```

1. <span data-ttu-id="43c1e-111">Stellen Sie über den folgenden Befehl eine Verbindung mit Azure her:</span><span class="sxs-lookup"><span data-stu-id="43c1e-111">Connect to Azure using the command shown below.</span></span> <span data-ttu-id="43c1e-112">Authentifizieren Sie sich nach der Eingabe des Befehls durch die Angabe Ihrer Azure-Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="43c1e-112">After entering the command, authenticate by providing your Azure credentials.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

1. <span data-ttu-id="43c1e-113">Erstellen Sie eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="43c1e-113">Create a resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. <span data-ttu-id="43c1e-114">Stellen Sie sicher, dass die Ressourcengruppe erfolgreich erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="43c1e-114">Verify the resource group was created successfully.</span></span>

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
<span data-ttu-id="43c1e-115">Eine weitere Möglichkeit zur Überprüfung, ob die Ressourcengruppe erfolgreich erstellt wurde, ist das Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="43c1e-115">Another way to check whether the resource group was created successfully is to use the Azure Portal.</span></span> <span data-ttu-id="43c1e-116">Melden Sie sich hierfür beim Portal an, und navigieren zum Abschnitt **Ressourcengruppen** (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="43c1e-116">To do this, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="43c1e-117">Die neue Ressourcengruppe sollte in der Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="43c1e-117">The new resource group should be displayed in the list.</span></span>

<span data-ttu-id="43c1e-118">Der folgende Screenshot zeigt den Speicherort der Kategorie „Ressourcengruppen“ im Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="43c1e-118">The following screenshot shows the location of the Resource groups category in the Azure Portal.</span></span>

![Screenshot des Blatts "Azure-Portal-Favoriten" mit der hervorgehobenen Ressourcengruppenkategorie.](../media/6-listing-resource-groups.png)

## <a name="summary"></a><span data-ttu-id="43c1e-120">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="43c1e-120">Summary</span></span>
<span data-ttu-id="43c1e-121">In dieser Übung wird ein allgemeines Muster für eine interaktive PowerShell-Sitzung veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="43c1e-121">This exercise shows a common pattern for an interactive PowerShell session.</span></span> <span data-ttu-id="43c1e-122">Sie haben ein Standard-Cmdlet verwendet, um für die Durchführung einer bestimmten Aufgabe das AzureRM-Modul und dann die Azure PowerShell-Cmdlets zu importieren.</span><span class="sxs-lookup"><span data-stu-id="43c1e-122">You used a standard cmdlet to import the AzureRM module and then the Azure PowerShell cmdlets to perform a specific task.</span></span> <span data-ttu-id="43c1e-123">Nun haben Sie eine Ressourcengruppe in Ihrem Abonnement erstellt und können nun VMs erstellen.</span><span class="sxs-lookup"><span data-stu-id="43c1e-123">You now have a resource group in your subscription and are ready to create VMs.</span></span>