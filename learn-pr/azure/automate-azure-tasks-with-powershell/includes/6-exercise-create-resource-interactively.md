
<span data-ttu-id="c1469-101">Angenommen Sie, Sie in einem Unternehmen arbeiten, mit der eine Sammlung von Linux-Verwaltungstools.</span><span class="sxs-lookup"><span data-stu-id="c1469-101">Suppose you work at a company that makes a suite of Linux admin tools.</span></span> <span data-ttu-id="c1469-102">Ihre Aufgabe ist, können Sie potenzielle Kunden, die vor dem Kauf es zum Testen Ihrer Software.</span><span class="sxs-lookup"><span data-stu-id="c1469-102">Your job is to help potential customers try your software before they buy it.</span></span> <span data-ttu-id="c1469-103">Da die Software auf der Stammebene-Änderungen für das Betriebssystem vornimmt, haben Sie sich entschieden, zum Erstellen einer Linux-VM für jeden Kunden Testversion.</span><span class="sxs-lookup"><span data-stu-id="c1469-103">Because the software makes root-level changes to the OS, you have decided to create a Linux VM for each trial customer.</span></span> <span data-ttu-id="c1469-104">Sie erstellen die virtuellen Computer aus, je nach Bedarf und am Ende des Test-Abonnements löschen.</span><span class="sxs-lookup"><span data-stu-id="c1469-104">You create the VMs as needed and delete them at the end of the trial subscription.</span></span> <span data-ttu-id="c1469-105">Auf diese Weise wird jeder Kunde mit einer sauberen Version des Betriebssystems gestartet.</span><span class="sxs-lookup"><span data-stu-id="c1469-105">This way, each customer starts with a clean version of the OS.</span></span> 

<span data-ttu-id="c1469-106">Damit diese virtuellen Computer getrennt von den virtuellen Computern bleibt Ihr Unternehmen für interne Tests verwendet, erstellen Sie eine dedizierte Ressourcengruppe, deren aufnehmen soll.</span><span class="sxs-lookup"><span data-stu-id="c1469-106">To keep these VMs separate from the VMs your company uses for internal testing, you will create a dedicated resource group to house them.</span></span> <span data-ttu-id="c1469-107">Sie benötigen nur eine Ressourcengruppe, damit mithilfe von Azure PowerShell im interaktiven Modus eine vernünftige Wahl für diese Aufgabe ist.</span><span class="sxs-lookup"><span data-stu-id="c1469-107">You only need one resource group so using Azure PowerShell in interactive mode is a reasonable choice for this task.</span></span>

## <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="c1469-108">Schritte zum Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="c1469-108">Steps to create a resource group</span></span>

1. <span data-ttu-id="c1469-109">Starten Sie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1469-109">Launch PowerShell.</span></span>

1. <span data-ttu-id="c1469-110">Importieren Sie das Modul in die aktuelle Sitzung, damit Sie Zugriff auf den Azure-Cmdlets haben.</span><span class="sxs-lookup"><span data-stu-id="c1469-110">Import the module into the current session so you have access to the Azure cmdlets.</span></span>

   ```powershell
   Import-Module AzureRM
   ```

1. <span data-ttu-id="c1469-111">Verbinden Sie mit Azure mit dem unten gezeigten Befehl.</span><span class="sxs-lookup"><span data-stu-id="c1469-111">Connect to Azure using the command shown below.</span></span> <span data-ttu-id="c1469-112">Nach Eingabe des Befehls, durch die Bereitstellung Ihrer Azure-Anmeldeinformationen zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="c1469-112">After entering the command, authenticate by providing your Azure credentials.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

1. <span data-ttu-id="c1469-113">Erstellen Sie eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="c1469-113">Create a resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. <span data-ttu-id="c1469-114">Stellen Sie sicher, dass die Ressourcengruppe erfolgreich erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="c1469-114">Verify the resource group was created successfully.</span></span>

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
<span data-ttu-id="c1469-115">Eine weitere Möglichkeit zum Überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde, ist im Azure-Portal verwenden.</span><span class="sxs-lookup"><span data-stu-id="c1469-115">Another way to check whether the resource group was created successfully is to use the Azure Portal.</span></span> <span data-ttu-id="c1469-116">Hierfür Anmelden beim Portal, und navigieren zu der **Ressourcengruppen** Abschnitt (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="c1469-116">To do this, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="c1469-117">Die neue Ressourcengruppe sollte in der Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c1469-117">The new resource group should be displayed in the list.</span></span>

![Verwenden des Portals zum Auflisten von Ressourcengruppen](../images/6-listing-resource-groups.png)

## <a name="summary"></a><span data-ttu-id="c1469-119">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c1469-119">Summary</span></span>
<span data-ttu-id="c1469-120">Diese Übung zeigt ein allgemeines Muster für eine interaktive PowerShell-Sitzung.</span><span class="sxs-lookup"><span data-stu-id="c1469-120">This exercise shows a common pattern for an interactive PowerShell session.</span></span> <span data-ttu-id="c1469-121">Sie verwendet ein standard-Cmdlet zum Importieren des AzureRM-Moduls, und klicken Sie dann Azure-PowerShell-Cmdlets für eine bestimmte Aufgabe durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="c1469-121">You used a standard cmdlet to import the AzureRM module and then the Azure PowerShell cmdlets to perform a specific task.</span></span> <span data-ttu-id="c1469-122">Klicken Sie jetzt haben eine Ressourcengruppe in Ihrem Abonnement und zum Erstellen von VMs bereit sind.</span><span class="sxs-lookup"><span data-stu-id="c1469-122">You now have a resource group in your subscription and are ready to create VMs.</span></span>