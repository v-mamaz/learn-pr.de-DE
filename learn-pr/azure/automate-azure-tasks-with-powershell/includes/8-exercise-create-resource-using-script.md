<span data-ttu-id="1937c-101">In dieser Einheit machen Sie mit dem Beispiel einer Firma weiter, die Linux-Verwaltungstools herstellt.</span><span class="sxs-lookup"><span data-stu-id="1937c-101">In this unit, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="1937c-102">Wie bereits besprochen planen Sie, Linux-VMs zu verwenden, um potenzielle Kunden Ihre Software testen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="1937c-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="1937c-103">Eine Ressourcengruppe steht bereit, und nun ist es an der Zeit, die VMs zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1937c-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="1937c-104">Ihr Unternehmen hat einen Stand auf einer großen Linux-Messe gebucht.</span><span class="sxs-lookup"><span data-stu-id="1937c-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="1937c-105">Sie planen einen Demobereich mit drei Terminals, die jeweils an eine separate Linux-VM angeschlossen sind.</span><span class="sxs-lookup"><span data-stu-id="1937c-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="1937c-106">Am Ende jedes Tages möchten Sie die VMs löschen und neu erstellen, damit sie jeden Morgen neu starten können.</span><span class="sxs-lookup"><span data-stu-id="1937c-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="1937c-107">Das manuelle Erstellen der VMs nach der Arbeit, wenn Sie erschöpft sind, wäre zu fehleranfällig.</span><span class="sxs-lookup"><span data-stu-id="1937c-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="1937c-108">Sie möchten ein PowerShell-Skript schreiben, um die Erstellung der VMs zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="1937c-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="1937c-109">Schreiben eines Skripts zum Erstellen virtueller Computer</span><span class="sxs-lookup"><span data-stu-id="1937c-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="1937c-110">Gehen Sie in Cloud Shell auf der rechten Seite wie folgt vor, um das Skript zu schreiben:</span><span class="sxs-lookup"><span data-stu-id="1937c-110">Follow these steps in the Cloud Shell on the right to write the script:</span></span>

1. <span data-ttu-id="1937c-111">Wechseln Sie in Cloud Shell zu Ihrem Stammordner.</span><span class="sxs-lookup"><span data-stu-id="1937c-111">Switch to your home folder in the Cloud Shell.</span></span>

    ```powershell
    cd $HOME\clouddrive
    ```

1. <span data-ttu-id="1937c-112">Erstellen Sie eine neue Textdatei namens **ConferenceDailyReset.ps1**.</span><span class="sxs-lookup"><span data-stu-id="1937c-112">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

    ```powershell
    touch "./ConferenceDailyReset.ps1"
    ```

1. <span data-ttu-id="1937c-113">Öffnen Sie den integrierten Editor, und wählen Sie die Datei **ConferenceDailyReset.ps1** aus.</span><span class="sxs-lookup"><span data-stu-id="1937c-113">Open the integrated editor and select the **ConferenceDailyReset.ps1** file.</span></span>

    ```powershell
    code "./ConferenceDailyReset.ps1"
    ```
    > [!TIP]
    > <span data-ttu-id="1937c-114">Die integrierte Cloud Shell-Instanz unterstützt auch Vim, Nano und Emacs, falls Sie lieber einen dieser Editoren verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="1937c-114">The integrated Cloud Shell also supports vim, nano, and emacs if you'd prefer to use one of those editors.</span></span>

1. <span data-ttu-id="1937c-115">Erfassen Sie zunächst die Eingabeparameter in einer Variablen.</span><span class="sxs-lookup"><span data-stu-id="1937c-115">Start by capturing the input parameter in a variable.</span></span> <span data-ttu-id="1937c-116">Fügen Sie Ihrem Skript die folgende Zeile hinzu:</span><span class="sxs-lookup"><span data-stu-id="1937c-116">Add the following line to your script:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

    > [!NOTE]
    > <span data-ttu-id="1937c-117">Normalerweise müssen Sie sich bei Azure unter Verwendung von `Connect-AzureRmAccount` mit Ihren Anmeldeinformationen authentifizieren, was über das Skript erfolgen kann.</span><span class="sxs-lookup"><span data-stu-id="1937c-117">Normally, you'd have to authenticate with Azure using your credentials using `Connect-AzureRmAccount` and this could be done in the script.</span></span> <span data-ttu-id="1937c-118">Da Sie in der Cloud Shell-Umgebung allerdings bereits authentifiziert sind, ist dieser Schritt nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="1937c-118">However, in the Cloud Shell environment you will already be authenticated so this is unnecessary.</span></span>

1. <span data-ttu-id="1937c-119">Fordern Sie zur Eingabe eines Benutzernamens und Kennworts für das Administratorkonto des virtuellen Computers auf, und erfassen Sie das Ergebnis in einer Variablen:</span><span class="sxs-lookup"><span data-stu-id="1937c-119">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. <span data-ttu-id="1937c-120">Erstellen Sie eine Schleife, die dreimal ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="1937c-120">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

1. <span data-ttu-id="1937c-121">Erstellen Sie im Schleifentext einen Namen für jeden virtuellen Computer, speichern Sie ihn in einer Variablen, und geben Sie ihn in der Konsole aus:</span><span class="sxs-lookup"><span data-stu-id="1937c-121">In the loop body, create a name for each VM and store it in a variable and output it to the console:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    ```

1. <span data-ttu-id="1937c-122">Erstellen Sie als Nächstes einen virtuellen Computer unter Verwendung der Variablen `$vmName`:</span><span class="sxs-lookup"><span data-stu-id="1937c-122">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
   ```

1. <span data-ttu-id="1937c-123">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1937c-123">Save the file.</span></span> <span data-ttu-id="1937c-124">Dazu können Sie das Menü „...“ rechts oben im Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="1937c-124">You can use the "..." menu at the top right corner of the editor.</span></span> <span data-ttu-id="1937c-125">Zum Speichern können aber auch die gängigen Zugriffstasten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1937c-125">There are also common accelerator keys for Save.</span></span>

<span data-ttu-id="1937c-126">Das fertige Skript sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="1937c-126">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="1937c-127">Ausführen des Skripts</span><span class="sxs-lookup"><span data-stu-id="1937c-127">Execute the script</span></span>

<span data-ttu-id="1937c-128">Schließen Sie den Editor über das Kontextmenü „...“.</span><span class="sxs-lookup"><span data-stu-id="1937c-128">Close the editor through the "..." context menu.</span></span>

1. <span data-ttu-id="1937c-129">Führen Sie das Skript aus.</span><span class="sxs-lookup"><span data-stu-id="1937c-129">Execute the script.</span></span>

    ```powershell
    .\ConferenceDailyReset.ps1 <rgn>[sandbox resource group name]</rgn>
    ```
    
<span data-ttu-id="1937c-130">Die Skriptausführung dauert ein paar Minuten.</span><span class="sxs-lookup"><span data-stu-id="1937c-130">The script will take several minutes to complete.</span></span> <span data-ttu-id="1937c-131">Vergewissern Sie sich anschließend, dass es erfolgreich ausgeführt wurde. Sehen Sie sich dazu die Ressourcen an, die nun in Ihrer Ressourcengruppe zur Verfügung stehen:</span><span class="sxs-lookup"><span data-stu-id="1937c-131">When it is finished, verify that it ran successfully by looking at the resources you now have in your resource group:</span></span>

```powershell
Get-AzureRmResource -ResourceType Microsoft.Compute/virtualMachines
```

<span data-ttu-id="1937c-132">Es sollten drei virtuelle Computer mit jeweils eindeutigem Namen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1937c-132">You should see three VMs, each with a unique name.</span></span>

<span data-ttu-id="1937c-133">Sie haben ein Skript geschrieben, das die Erstellung dreier virtueller Computer in der durch einen Skriptparameter angegebenen Ressourcengruppe automatisiert.</span><span class="sxs-lookup"><span data-stu-id="1937c-133">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="1937c-134">Das Skript ist kurz und einfach, automatisiert aber einen Prozess, der im Portal viel Zeit in Anspruch nehmen würde.</span><span class="sxs-lookup"><span data-stu-id="1937c-134">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>