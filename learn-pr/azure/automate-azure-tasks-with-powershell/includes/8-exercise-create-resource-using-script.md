<span data-ttu-id="abb31-101">In dieser Übung fahren Sie mit dem Beispiel einer Firma fort, die Linux-Verwaltungstools herstellt.</span><span class="sxs-lookup"><span data-stu-id="abb31-101">In this exercise, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="abb31-102">Rufen Sie sich in Erinnerung, dass Sie planen, Linux-VMs zu verwenden, um potenzielle Kunden Ihre Software testen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="abb31-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="abb31-103">Eine Ressourcengruppe steht bereit, und nun ist es an der Zeit, die VMs zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="abb31-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="abb31-104">Ihr Unternehmen hat einen Stand auf einer großen Linux-Messe gebucht.</span><span class="sxs-lookup"><span data-stu-id="abb31-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="abb31-105">Sie planen einen Demobereich mit drei Terminals, die jeweils an eine separate Linux-VM angeschlossen sind.</span><span class="sxs-lookup"><span data-stu-id="abb31-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="abb31-106">Am Ende jedes Tages möchten Sie die VMs löschen und neu erstellen, damit sie jeden Morgen neu starten können.</span><span class="sxs-lookup"><span data-stu-id="abb31-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="abb31-107">Das manuelle Erstellen der VMs nach der Arbeit, wenn Sie erschöpft sind, wäre zu fehleranfällig.</span><span class="sxs-lookup"><span data-stu-id="abb31-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="abb31-108">Sie möchten ein PowerShell-Skript schreiben, um die Erstellung der VMs zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="abb31-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="abb31-109">Schreiben eines Skripts zum Erstellen virtueller Computer</span><span class="sxs-lookup"><span data-stu-id="abb31-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="abb31-110">Gehen Sie folgendermaßen vor, um das Skript zu schreiben:</span><span class="sxs-lookup"><span data-stu-id="abb31-110">Follow these steps to write the script:</span></span>

1. <span data-ttu-id="abb31-111">Erstellen Sie eine neue Textdatei mit dem Namen **ConferenceDailyReset.ps1**.</span><span class="sxs-lookup"><span data-stu-id="abb31-111">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

2. <span data-ttu-id="abb31-112">Erfassen Sie den Parameter in einer Variablen:</span><span class="sxs-lookup"><span data-stu-id="abb31-112">Capture the parameter in a variable:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

3. <span data-ttu-id="abb31-113">Authentifizieren Sie sich bei Azure mit Ihren Anmeldeinformationen:</span><span class="sxs-lookup"><span data-stu-id="abb31-113">Authenticate with Azure using your credentials:</span></span>

    ```powershell
    Connect-AzureRmAccount
    ```

4. <span data-ttu-id="abb31-114">Fordern Sie einen Benutzernamen und ein Kennwort für das Administratorkonto der VM an, und erfassen Sie das Ergebnis in einer Variablen:</span><span class="sxs-lookup"><span data-stu-id="abb31-114">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. <span data-ttu-id="abb31-115">Erstellen Sie eine Schleife, die dreimal ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="abb31-115">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. <span data-ttu-id="abb31-116">Erstellen Sie im Schleifentext einen Namen für jede VM, und speichern Sie ihn in einer Variablen:</span><span class="sxs-lookup"><span data-stu-id="abb31-116">In the loop body, create a name for each VM and store it in a variable:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. <span data-ttu-id="abb31-117">Erstellen Sie als Nächstes eine VM mithilfe der Variablen `$vmName`:</span><span class="sxs-lookup"><span data-stu-id="abb31-117">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
   ```

8. <span data-ttu-id="abb31-118">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="abb31-118">Save the file.</span></span>

<span data-ttu-id="abb31-119">Die fertige Skript sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="abb31-119">The completed script should look like this:</span></span>

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

## <a name="execute-the-script"></a><span data-ttu-id="abb31-120">Ausführen des Skripts</span><span class="sxs-lookup"><span data-stu-id="abb31-120">Execute the script</span></span>

<span data-ttu-id="abb31-121">Starten Sie PowerShell, und wechseln Sie zum Verzeichnis, in dem Sie die Skriptdatei gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="abb31-121">Launch PowerShell and change to the directory where you saved the script file.</span></span> <span data-ttu-id="abb31-122">Geben Sie den folgenden Befehl ein, um das Skript auszuführen:</span><span class="sxs-lookup"><span data-stu-id="abb31-122">To run the script, execute the following command:</span></span>

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

<span data-ttu-id="abb31-123">Die Ausführung des Skripts kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="abb31-123">The script may take a few minutes to complete.</span></span> <span data-ttu-id="abb31-124">Wenn sie abgeschlossen ist, stellen Sie sicher, dass es erfolgreich ausgeführt wurde:</span><span class="sxs-lookup"><span data-stu-id="abb31-124">When it is finished, verify that it ran successfully:</span></span>

1. <span data-ttu-id="abb31-125">Melden Sie sich in einem Browser beim Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="abb31-125">In a browser, sign into the Azure portal.</span></span>
2. <span data-ttu-id="abb31-126">Klicken Sie im linken Navigationsbereich auf **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="abb31-126">In the navigation on the left, click **Resource Groups**.</span></span>
3. <span data-ttu-id="abb31-127">Klicken Sie in der Liste der Ressourcengruppen auf **TrialsResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="abb31-127">In the list of resource groups, click **TrialsResourceGroup**.</span></span> <span data-ttu-id="abb31-128">In der Liste der Ressourcen sollten Sie die neu erstellten VMs und die zugehörigen Ressourcen vorfinden.</span><span class="sxs-lookup"><span data-stu-id="abb31-128">In the list of resources, you should see the newly created VMs and their associated resources.</span></span>

## <a name="summary"></a><span data-ttu-id="abb31-129">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="abb31-129">Summary</span></span>
<span data-ttu-id="abb31-130">Sie haben ein Skript geschrieben, das die Erstellung dreier VMs in der von einem Skriptparameter angegebenen Ressourcengruppe automatisiert.</span><span class="sxs-lookup"><span data-stu-id="abb31-130">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="abb31-131">Das Skript ist kurz und einfach, automatisiert aber einen Prozess, der im Portal viel Zeit in Anspruch nehmen würde.</span><span class="sxs-lookup"><span data-stu-id="abb31-131">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>