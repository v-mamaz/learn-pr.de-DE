
<span data-ttu-id="701d9-101">In dieser Übung wird das Beispiel für ein Unternehmen fortgesetzt werden, mit der Linux-Verwaltungstools.</span><span class="sxs-lookup"><span data-stu-id="701d9-101">In this exercise, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="701d9-102">Denken Sie daran, dass Sie virtuelle Linux-Computer zu verwenden, um potenzielle Kunden das Testen Ihrer Software ermöglichen möchten.</span><span class="sxs-lookup"><span data-stu-id="701d9-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="701d9-103">Sie haben eine Ressourcengruppe bereit, und nun ist es Zeit, um die virtuellen Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="701d9-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="701d9-104">Ihr Unternehmen hat für einen Stand auf einer großen Linux Messe bezahlt.</span><span class="sxs-lookup"><span data-stu-id="701d9-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="701d9-105">Einen Demo-Bereich, enthält jede drei Terminals mit einer separaten Linux-VM verbunden werden sollen.</span><span class="sxs-lookup"><span data-stu-id="701d9-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="701d9-106">Am Ende des Tages möchten Sie die virtuellen Computer löschen und neu erstellen, sodass sie neue jeden Morgen beginnen.</span><span class="sxs-lookup"><span data-stu-id="701d9-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="701d9-107">Erstellen die virtuellen Computer manuell aus, nachdem die Arbeit, wenn Sie es vielleicht leid, sind unter Umständen Fehler unterlaufen würde.</span><span class="sxs-lookup"><span data-stu-id="701d9-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="701d9-108">Ein PowerShell-Skript zur Automatisierung des Erstellungsprozesses des virtuellen Computers schreiben möchten.</span><span class="sxs-lookup"><span data-stu-id="701d9-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="701d9-109">Schreiben Sie ein Skript, virtuelle Computer erstellt.</span><span class="sxs-lookup"><span data-stu-id="701d9-109">Write a Script that Creates Virtual Machines</span></span>

<span data-ttu-id="701d9-110">Um das Skript zu erstellen, gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="701d9-110">Follow these steps to write the script:</span></span>

1. <span data-ttu-id="701d9-111">Erstellen Sie eine neue Textdatei mit dem Namen **ConferenceDailyReset.ps1**.</span><span class="sxs-lookup"><span data-stu-id="701d9-111">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

1. <span data-ttu-id="701d9-112">Erfassen Sie den Parameter in einer Variablen:</span><span class="sxs-lookup"><span data-stu-id="701d9-112">Capture the parameter in a variable:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

1. <span data-ttu-id="701d9-113">Authentifizieren Sie bei Azure, die mit Ihren Anmeldeinformationen:</span><span class="sxs-lookup"><span data-stu-id="701d9-113">Authenticate with Azure using your credentials:</span></span>

    ```powershell
    Connect-AzureRmAccount
    ```

1. <span data-ttu-id="701d9-114">Zum Angeben eines Benutzernamens und Kennworts für die VM Administratorkonto aufgefordert, und das Ergebnis in einer Variablen zu erfassen:</span><span class="sxs-lookup"><span data-stu-id="701d9-114">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. <span data-ttu-id="701d9-115">Erstellen Sie eine Schleife, die drei Mal ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="701d9-115">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) {
    ```

1. <span data-ttu-id="701d9-116">Erstellen Sie einen Namen für jeden virtuellen Computer aus, und speichern Sie es in einer Variablen:</span><span class="sxs-lookup"><span data-stu-id="701d9-116">Create a name for each VM and store it in a variable:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

1. <span data-ttu-id="701d9-117">Erstellen eines virtuellen Computers:</span><span class="sxs-lookup"><span data-stu-id="701d9-117">Create a VM:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

1. <span data-ttu-id="701d9-118">Schließen Sie den Text der Schleife:</span><span class="sxs-lookup"><span data-stu-id="701d9-118">Close the body of the loop:</span></span>

    ```powershell
    }
    ```

1. <span data-ttu-id="701d9-119">Speichern Sie die Datei .</span><span class="sxs-lookup"><span data-stu-id="701d9-119">Save the file.</span></span>

<span data-ttu-id="701d9-120">Das fertiggestellte Skript sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="701d9-120">The completed script should look like this:</span></span>

    ```powershell
    param([string]$resourceGroup)

    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

    Connect-AzureRmAccount

    For ($i = 1; $i -le 3; $i++)
    {
        $vmName = "ConferenceDemo" + $i

        New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
    }
    ```

## <a name="execute-the-script"></a><span data-ttu-id="701d9-121">Führen Sie das Skript</span><span class="sxs-lookup"><span data-stu-id="701d9-121">Execute the Script</span></span>

<span data-ttu-id="701d9-122">Starten Sie PowerShell, und wechseln Sie zum Verzeichnis, in dem Sie die Skriptdatei gespeichert.</span><span class="sxs-lookup"><span data-stu-id="701d9-122">Launch PowerShell and change to the directory where you saved the script file.</span></span> <span data-ttu-id="701d9-123">Um das Skript auszuführen, führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="701d9-123">To run the script, execute the following command:</span></span>

    ```powershell
    .\ConferenceDailyReset.ps1 TrialsResourceGroup
    ```

<span data-ttu-id="701d9-124">Das Skript kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="701d9-124">The script may take a few minutes to complete.</span></span> <span data-ttu-id="701d9-125">Wenn sie abgeschlossen ist, stellen Sie sicher, dass es erfolgreich ausgeführt wurde:</span><span class="sxs-lookup"><span data-stu-id="701d9-125">When it is finished, verify that it ran successfully:</span></span>

1. <span data-ttu-id="701d9-126">Melden Sie sich im Azure-Portal, in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="701d9-126">In a browser, sign into the Azure portal.</span></span>
1. <span data-ttu-id="701d9-127">Klicken Sie im Navigationsbereich auf der linken Seite auf **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="701d9-127">In the navigation on the left, click **Resource Groups**.</span></span>
1. <span data-ttu-id="701d9-128">In der Liste der Ressourcengruppen anzuzeigen, klicken Sie auf **TrialsResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="701d9-128">In the list of resource groups, click **TrialsResourceGroup**.</span></span> <span data-ttu-id="701d9-129">In der Liste der Ressourcen sollte die neu erstellten virtuellen Computer und den zugehörigen Ressourcen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="701d9-129">In the list of resources, you should see the newly created VMs and their associated resources.</span></span>

## <a name="summary"></a><span data-ttu-id="701d9-130">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="701d9-130">Summary</span></span>
<span data-ttu-id="701d9-131">Sie schrieb ein Skript, das die Erstellung von drei virtuellen Computer in der Ressourcengruppe, die durch ein Script-Parameter angegebenen automatisiert.</span><span class="sxs-lookup"><span data-stu-id="701d9-131">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="701d9-132">Das Skript ist kurz und einfach aber automatisiert den Prozess, der eine lange manuell über das Portal akzeptieren würde.</span><span class="sxs-lookup"><span data-stu-id="701d9-132">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>