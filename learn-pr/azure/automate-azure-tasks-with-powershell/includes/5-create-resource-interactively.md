<span data-ttu-id="8998e-101">Mit PowerShell können Sie Befehle schreiben und diese sofort ausführen.</span><span class="sxs-lookup"><span data-stu-id="8998e-101">PowerShell lets you write commands and execute them immediately.</span></span> <span data-ttu-id="8998e-102">Wird als **interaktiver Modus** bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="8998e-102">This is known as **interactive mode**.</span></span>

<span data-ttu-id="8998e-103">Denken Sie daran, dass das Ziel im CRM-Beispiel (Customer Relationship Management) darin besteht, drei Testumgebungen zu erstellen, die virtuelle Computer enthalten.</span><span class="sxs-lookup"><span data-stu-id="8998e-103">Recall that the overall goal in the Customer Relationship Management (CRM) example is to create three test environments containing VMs.</span></span> <span data-ttu-id="8998e-104">Sie verwenden Ressourcengruppen, um sicherzustellen, dass die virtuellen Computer in separaten Umgebungen organisiert sind: einer für Komponententests, einer für Integrationstests und einer für Benutzerakzeptanztests.</span><span class="sxs-lookup"><span data-stu-id="8998e-104">You will use resource groups to ensure the VMs are organized into separate environments: one for unit testing, one for integration testing, and one for acceptance testing.</span></span> <span data-ttu-id="8998e-105">Da Sie die Ressourcengruppen nur einmal erstellen müssen, ist der interaktive Modus von PowerShell daher eine gute Wahl.</span><span class="sxs-lookup"><span data-stu-id="8998e-105">You only need to create the resource groups once, which means using the interactive mode of PowerShell is a good choice.</span></span>

<span data-ttu-id="8998e-106">Wenn Sie einen Befehl in PowerShell eingeben, wird er einem _Cmdlet_ zugeordnet, mit dem dann die gewünschte Aktion durchgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="8998e-106">When you type a command into PowerShell, it matches it to a _cmdlet_ which then performs the requested action.</span></span> <span data-ttu-id="8998e-107">Wir sehen uns einige allgemeine Befehle an, die Sie verwenden können, und anschließend wird die Installation der Azure-Unterstützung für PowerShell beschrieben.</span><span class="sxs-lookup"><span data-stu-id="8998e-107">We're going to look at some of the common commands you can use, and then look at installing the Azure support for PowerShell.</span></span>

## <a name="what-are-powershell-cmdlets"></a><span data-ttu-id="8998e-108">Was sind PowerShell-Cmdlets?</span><span class="sxs-lookup"><span data-stu-id="8998e-108">What are PowerShell cmdlets?</span></span>
<span data-ttu-id="8998e-109">Ein PowerShell-Befehl wird als **Cmdlet** (ausgesprochen: „Command-let“) bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="8998e-109">A PowerShell command is called a **cmdlet** (pronounced "command-let").</span></span> <span data-ttu-id="8998e-110">Ein Cmdlet ist ein Befehl, der ein einzelnes Feature bearbeitet.</span><span class="sxs-lookup"><span data-stu-id="8998e-110">A cmdlet is a command that manipulates a single feature.</span></span> <span data-ttu-id="8998e-111">Der Begriff **Cmdlet** soll „kleiner Befehl“ heißen.</span><span class="sxs-lookup"><span data-stu-id="8998e-111">The term **cmdlet** is intended to imply "small command".</span></span> <span data-ttu-id="8998e-112">Gemäß der Konvention wird Cmdlet-Autoren empfohlen, Cmdlets einfach zu halten und nur für einen einzigen Zweck zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8998e-112">By convention, cmdlet authors are encouraged to keep cmdlets simple and single-purpose.</span></span>

<span data-ttu-id="8998e-113">Im PowerShell-Basisprodukt sind Cmdlets enthalten, die mit Features wie Sitzungen und Hintergrundaufträgen funktionieren.</span><span class="sxs-lookup"><span data-stu-id="8998e-113">The base PowerShell product ships with cmdlets that work with features such as sessions and background jobs.</span></span> <span data-ttu-id="8998e-114">Fügen Sie Module zu Ihrer PowerShell-Installation hinzu, damit Cmdlets andere Features ändern können.</span><span class="sxs-lookup"><span data-stu-id="8998e-114">You add modules to your PowerShell installation to get cmdlets that manipulate other features.</span></span> <span data-ttu-id="8998e-115">Es gibt z.B. Drittanbietermodule für die Arbeit mit FTP, das Verwalten Ihres Betriebssystems oder das Zugreifen auf das Dateisystem.</span><span class="sxs-lookup"><span data-stu-id="8998e-115">For example, there are third-party modules to work with ftp, administer your operating system, access the file system, and so on.</span></span>

<span data-ttu-id="8998e-116">Die Namenskonvention bei Cmdlets ist „Verb-Substantiv“, z.B. **Get-Process**, **Format-Table**, and **Start-Service**.</span><span class="sxs-lookup"><span data-stu-id="8998e-116">Cmdlets follow a verb-noun naming convention; for example, **Get-Process**, **Format-Table**, and **Start-Service**.</span></span> <span data-ttu-id="8998e-117">Es gibt ebenfalls eine Konvention für die Auswahl des Verbs, z.B. „get“ zum Abrufen von Daten, „set“ zum Einfügen oder Aktualisieren von Daten, „format“ zum Formatieren von Daten oder „out“, um die Ausgabe einem Ziel zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="8998e-117">There is also a convention for verb choice: "get" to retrieve data, "set" to insert or update data, "format" to format data, "out" to direct output to a destination, and so on.</span></span>

<span data-ttu-id="8998e-118">Cmdlet-Autoren wird empfohlen, eine Hilfedatei für jedes Cmdlet einzufügen.</span><span class="sxs-lookup"><span data-stu-id="8998e-118">Cmdlet authors are encouraged to include a help file for each cmdlet.</span></span> <span data-ttu-id="8998e-119">Das Cmdlet **Get-Help** zeigt jeweils die Hilfedatei für ein Cmdlet an.</span><span class="sxs-lookup"><span data-stu-id="8998e-119">The **Get-Help** cmdlet displays the help file for any cmdlet.</span></span> <span data-ttu-id="8998e-120">Beispielsweise können wir mit der folgenden Anweisung die Hilfe zum Cmdlet `Get-ChildItem` anzeigen:</span><span class="sxs-lookup"><span data-stu-id="8998e-120">For example, we could get help on the `Get-ChildItem` cmdlet with the following statement:</span></span>

```powershell
Get-Help Get-ChildItem -detailed
```

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="8998e-121">Was ist ein PowerShell-Modul?</span><span class="sxs-lookup"><span data-stu-id="8998e-121">What is a PowerShell module?</span></span>

<span data-ttu-id="8998e-122">Cmdlets werden als Teile von _Modulen_ bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="8998e-122">Cmdlets are shipped in _modules_.</span></span> <span data-ttu-id="8998e-123">Ein PowerShell-Modul ist eine DLL, die den Code zum Verarbeiten der einzelnen verfügbaren Cmdlets enthält.</span><span class="sxs-lookup"><span data-stu-id="8998e-123">A PowerShell Module is a DLL that includes the code to proces each available cmdlet.</span></span> <span data-ttu-id="8998e-124">Sie können Cmdlets in PowerShell laden, indem Sie das Modul laden, in dem diese enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="8998e-124">You load cmdlets into PowerShell by loading the module they are contained in.</span></span> <span data-ttu-id="8998e-125">Eine Liste mit den geladenen Modulen können Sie mit dem Befehl `Get-Module` anzeigen:</span><span class="sxs-lookup"><span data-stu-id="8998e-125">You can get a list of loaded modules using the `Get-Module` command:</span></span>

```powershell
Get-Module
```

<span data-ttu-id="8998e-126">Die Ausgabe sieht in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="8998e-126">This will output something like:</span></span>

```output
ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Manifest   3.1.0.0    Microsoft.PowerShell.Utility        {Add-Member, Add-Type, Clear-Variable, Compare-Object...}
Binary     1.0.0.1    PackageManagement                   {Find-Package, Find-PackageProvider, Get-Package, Get-Pack...
Script     1.0.0.1    PowerShellGet                       {Find-Command, Find-DscResource, Find-Module, Find-RoleCap...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
```

## <a name="what-is-azurerm"></a><span data-ttu-id="8998e-127">Was ist AzureRM?</span><span class="sxs-lookup"><span data-stu-id="8998e-127">What is AzureRM?</span></span>
<span data-ttu-id="8998e-128">**AzureRM** ist der formelle Name des Azure PowerShell-Moduls, das die Cmdlets enthält, die mit den Azure-Features zusammenarbeiten sollen (das **RM** im Namen steht für **Resource Manager**).</span><span class="sxs-lookup"><span data-stu-id="8998e-128">**AzureRM** is the formal name for the Azure PowerShell module containing cmdlets to work with Azure features (the **RM** in the name stands for **Resource Manager**).</span></span> <span data-ttu-id="8998e-129">Es enthält hunderte Cmdlets, mit denen Sie nahezu jeden Aspekt jeder Azure-Ressource regulieren können.</span><span class="sxs-lookup"><span data-stu-id="8998e-129">It contains hundreds of cmdlets that let you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="8998e-130">Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory, Containern, Machine Learning usw. arbeiten.</span><span class="sxs-lookup"><span data-stu-id="8998e-130">You can work with resource groups, storage, virtual machines, Azure Active Directory, containers, machine learning, and so on.</span></span> <span data-ttu-id="8998e-131">Dieses Modul ist eine Open-Source-Komponente, die [auf GitHub verfügbar](https://github.com/Azure/azure-powershell) ist.</span><span class="sxs-lookup"><span data-stu-id="8998e-131">This module is an open source component [available on GitHub](https://github.com/Azure/azure-powershell).</span></span>

> [!NOTE]
> <span data-ttu-id="8998e-132">Das Azure PowerShell-Modul kann optional installiert werden. Die Cmdlets stehen erst zur Verfügung, nachdem Sie das Modul importiert haben.</span><span class="sxs-lookup"><span data-stu-id="8998e-132">The Azure PowerShell module is an optional install - the cmdlets aren't available until you import the module.</span></span>

### <a name="install-the-azurerm-module"></a><span data-ttu-id="8998e-133">Installieren des AzureRM-Moduls</span><span class="sxs-lookup"><span data-stu-id="8998e-133">Install the AzureRM module</span></span>

<span data-ttu-id="8998e-134">Das AzureRM-Modul ist über ein globales Repository mit dem Namen „PowerShell-Katalog“ verfügbar.</span><span class="sxs-lookup"><span data-stu-id="8998e-134">The AzureRM module is available from a global repository called the PowerShell Gallery.</span></span> <span data-ttu-id="8998e-135">Sie können das Modul mit dem Befehl `Install-Module` auf Ihrem lokalen Computer installieren.</span><span class="sxs-lookup"><span data-stu-id="8998e-135">You can install the module onto your local machine through the `Install-Module` command.</span></span> <span data-ttu-id="8998e-136">Sie benötigen eine PowerShell-Instanz mit erhöhten Rechten, um Module aus dem PowerShell-Katalog zu installieren.</span><span class="sxs-lookup"><span data-stu-id="8998e-136">You need an elevated PowerShell shell to install modules from the PowerShell Gallery.</span></span> 

<span data-ttu-id="8998e-137">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="8998e-137">::: zone pivot="windows"</span></span>

<span data-ttu-id="8998e-138">Führen Sie die folgenden Befehle aus, um das aktuelle Azure PowerShell-Modul zu installieren:</span><span class="sxs-lookup"><span data-stu-id="8998e-138">To install the latest Azure PowerShell module, run the following commands:</span></span>

1. <span data-ttu-id="8998e-139">Öffnen Sie das **Startmenü**, und geben Sie **Windows PowerShell** ein.</span><span class="sxs-lookup"><span data-stu-id="8998e-139">Open the **Start** menu and type **Windows PowerShell**.</span></span>

1. <span data-ttu-id="8998e-140">Klicken Sie mit der rechten Maustaste auf das Symbol **Windows PowerShell**, und wählen Sie **Als Administrator ausführen** aus.</span><span class="sxs-lookup"><span data-stu-id="8998e-140">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>

1. <span data-ttu-id="8998e-141">Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="8998e-141">In the **User Account Control** dialog, select **Yes**.</span></span>

1. <span data-ttu-id="8998e-142">Geben Sie den folgenden Befehl ein, und drücken Sie die Eingabetaste:</span><span class="sxs-lookup"><span data-stu-id="8998e-142">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```

<span data-ttu-id="8998e-143">Das Modul wird standardmäßig für alle Benutzer installiert (über den Bereichsparameter gesteuert).</span><span class="sxs-lookup"><span data-stu-id="8998e-143">This installs the module for all users by default (controlled by the scope parameter).</span></span> 

<span data-ttu-id="8998e-144">Der Befehl nutzt NuGet zum Abrufen von Komponenten. Je nach der bei Ihnen installierten NuGet-Version wird ggf. ein Dialogfeld angezeigt, über das Sie die aktuelle Version von NuGet herunterladen und installieren können.</span><span class="sxs-lookup"><span data-stu-id="8998e-144">The command relies on NuGet to retrieve components, depending on the version of NuGet you have installed you might get a prompt to download and install the latest version of NuGet.</span></span>

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files (x86)\PackageManagement\ProviderAssemblies' or
'C:\Users\<username>\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import
 the NuGet provider now?
```

<span data-ttu-id="8998e-145">Standardmäßig ist der PowerShell-Katalog nicht als vertrauenswürdiges Repository für PowerShellGet konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="8998e-145">By default, the PowerShell gallery isn't configured as a trusted repository for PowerShellGet.</span></span> <span data-ttu-id="8998e-146">Bei der ersten Verwendung des PowerShell-Katalogs wird die folgende Meldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="8998e-146">The first time you use the PSGallery you see the following prompt:</span></span>

```output
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
```

#### <a name="script-execution-failed"></a><span data-ttu-id="8998e-147">Fehler bei der Skriptausführung</span><span class="sxs-lookup"><span data-stu-id="8998e-147">Script execution failed</span></span>
<span data-ttu-id="8998e-148">Je nach Ihrer Sicherheitskonfiguration tritt für `Import-Module` unter Umständen ein Fehler der folgenden Art auf.</span><span class="sxs-lookup"><span data-stu-id="8998e-148">Depending on your security configuration, `Import-Module` might fail with something like the following.</span></span>

```output
import-module : File C:\Program Files (x86)\WindowsPowerShell\Modules\azurerm\6.8.1\AzureRM.psm1 cannot be loaded
because running scripts is disabled on this system. For more information, see about_Execution_Policies at
https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1
+ import-module azurerm
+ ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [Import-Module], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess,Microsoft.PowerShell.Commands.ImportModuleCommand
```

<span data-ttu-id="8998e-149">Hiermit wird normalerweise angegeben, dass die Ausführungsrichtlinie „eingeschränkt“ ist. Dies bedeutet, dass Sie keine Module ausführen können, die Sie von einer externen Quelle herunterladen, einschließlich des PowerShell-Katalogs.</span><span class="sxs-lookup"><span data-stu-id="8998e-149">This normally indicates that the execution policy is "restricted", meaning you can't execute modules you download from an external source - including the PowerShell gallery.</span></span> <span data-ttu-id="8998e-150">Sie können überprüfen, ob dies der Fall ist, indem Sie den Befehl `Get-ExecutionPolicy` ausführen.</span><span class="sxs-lookup"><span data-stu-id="8998e-150">You can check whether this is the case by executing the command `Get-ExecutionPolicy`.</span></span> <span data-ttu-id="8998e-151">Gehen Sie wie folgt vor, falls „Eingeschränkt“ zurückgegeben wird:</span><span class="sxs-lookup"><span data-stu-id="8998e-151">If it returns "Restricted", then do the following:</span></span>

1. <span data-ttu-id="8998e-152">Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.</span><span class="sxs-lookup"><span data-stu-id="8998e-152">Open an elevated PowerShell command prompt.</span></span>
1. <span data-ttu-id="8998e-153">Verwenden Sie das Cmdlet `SetExecutionPolicy`, um die Richtlinie in „RemoteSigned“ zu ändern:</span><span class="sxs-lookup"><span data-stu-id="8998e-153">Use the `SetExecutionPolicy` cmdlet to change the policy to "RemoteSigned":</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<span data-ttu-id="8998e-154">Ihre Berechtigung wird abgefragt:</span><span class="sxs-lookup"><span data-stu-id="8998e-154">This will prompt you for permission:</span></span>

```output
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```

<span data-ttu-id="8998e-155">Sie sollten dann `Import-Module` verwenden können, um die Cmdlets zu laden.</span><span class="sxs-lookup"><span data-stu-id="8998e-155">You should then be able to use `Import-Module` to load the cmdlets.</span></span>

<span data-ttu-id="8998e-156">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="8998e-156">:::zone-end</span></span>

<span data-ttu-id="8998e-157">::: zone pivot="linux,macos"</span><span class="sxs-lookup"><span data-stu-id="8998e-157">::: zone pivot="linux,macos"</span></span>

<span data-ttu-id="8998e-158">Zum Installieren von Azure PowerShell unter Linux oder macOS verwenden wir die gleichen Befehle.</span><span class="sxs-lookup"><span data-stu-id="8998e-158">We use the same commands to install the Azure PowerShell on either Linux or macOS.</span></span>

1. <span data-ttu-id="8998e-159">Geben Sie auf einem Terminal den folgenden Befehl ein, um PowerShell Core mit erhöhten Rechten zu starten.</span><span class="sxs-lookup"><span data-stu-id="8998e-159">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="8998e-160">Um Azure PowerShell zu installieren, führen Sie an der PowerShell Core-Eingabeaufforderung den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="8998e-160">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="8998e-161">Wenn Sie gefragt werden, ob Sie Modulen von **PSGallery** vertrauen, antworten Sie **Ja** oder **Ja, alle**.</span><span class="sxs-lookup"><span data-stu-id="8998e-161">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

<span data-ttu-id="8998e-162">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="8998e-162">:::zone-end</span></span>

### <a name="update-a-module"></a><span data-ttu-id="8998e-163">Aktualisieren eines Moduls</span><span class="sxs-lookup"><span data-stu-id="8998e-163">Update a module</span></span>

<span data-ttu-id="8998e-164">Wenn Sie in einer Warnung oder Fehlermeldung darauf hingewiesen werden, dass bereits eine Version des Azure PowerShell-Moduls installiert ist, können Sie diese mit dem folgenden Befehl auf die _neueste_ Version aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="8998e-164">If you get a warning or error message indicating that a version of the Azure PowerShell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>

<span data-ttu-id="8998e-165">:::zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="8998e-165">:::zone pivot="windows"</span></span>

```powershell
Update-Module -Name AzureRM
```

<span data-ttu-id="8998e-166">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="8998e-166">:::zone-end</span></span>

<span data-ttu-id="8998e-167">::: zone pivot="linux,macos"</span><span class="sxs-lookup"><span data-stu-id="8998e-167">::: zone pivot="linux,macos"</span></span>

```powershell
Update-Module -Name AzureRM.NetCore
```

<span data-ttu-id="8998e-168">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="8998e-168">:::zone-end</span></span>

<span data-ttu-id="8998e-169">Antworten Sie ebenso wie beim Befehl `Install-Module` auf die Frage, ob Sie dem Modul vertrauen, mit **Ja** oder **Ja, alle**.</span><span class="sxs-lookup"><span data-stu-id="8998e-169">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span> <span data-ttu-id="8998e-170">Sie können auch den Befehl `Update-Module` verwenden, um ein Modul neu zu installieren, falls dafür Probleme auftreten.</span><span class="sxs-lookup"><span data-stu-id="8998e-170">You can also use the `Update-Module` command to re-install a module if you are having trouble with it.</span></span>

## <a name="example-how-to-create-a-resource-group-with-azure-powershell"></a><span data-ttu-id="8998e-171">Beispiel: Erstellen einer Ressourcengruppe mit Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8998e-171">Example: How to create a resource group with Azure PowerShell</span></span>
<span data-ttu-id="8998e-172">Nachdem Sie das Azure-Modul geladen haben, können Sie mit der Verwendung von Azure beginnen.</span><span class="sxs-lookup"><span data-stu-id="8998e-172">Once you have the Azure module loaded, you can begin working with Azure.</span></span> <span data-ttu-id="8998e-173">Wir führen eine häufige Aufgabe durch: das Erstellen einer Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="8998e-173">Let's do a common task - create a Resource Group.</span></span> <span data-ttu-id="8998e-174">Wie Sie wissen, verwenden wir Ressourcengruppen, um zusammengehörige Ressourcen gemeinsam zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="8998e-174">As you know, we use resource groups to administer related resources together.</span></span> <span data-ttu-id="8998e-175">Die Erstellung einer neuen Ressourcengruppe ist eine der ersten Aufgaben, die Sie beim Starten einer neuen Azure-Lösung durchführen.</span><span class="sxs-lookup"><span data-stu-id="8998e-175">Creating a new resource group is one of the first tasks you'll do when starting a new Azure solution.</span></span>

<span data-ttu-id="8998e-176">Es müssen vier Schritte ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="8998e-176">There are four steps we need to perform:</span></span>

1. <span data-ttu-id="8998e-177">Importieren Sie die Azure-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8998e-177">Import the Azure cmdlets.</span></span>

1. <span data-ttu-id="8998e-178">Stellen Sie eine Verbindung mit Ihrem Azure-Abonnement her.</span><span class="sxs-lookup"><span data-stu-id="8998e-178">Connect to your Azure subscription.</span></span>

1. <span data-ttu-id="8998e-179">Erstellen Sie die Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="8998e-179">Create the resource group.</span></span>

1. <span data-ttu-id="8998e-180">Stellen Sie sicher, dass das Erstellen erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="8998e-180">Verify that creation was successful (see below).</span></span>

<span data-ttu-id="8998e-181">Die folgende Abbildung zeigt eine Übersicht dieser Schritte.</span><span class="sxs-lookup"><span data-stu-id="8998e-181">The following illustration shows an overview of these steps.</span></span>

![Eine Abbildung, die die Schritte zum Erstellen einer Ressourcengruppe zeigt.](../media/5-create-resource-overview.png)

<span data-ttu-id="8998e-183">Jeder Schritt entspricht einem anderen Cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8998e-183">Each step corresponds to a different cmdlet.</span></span>

### <a name="import-the-azure-cmdlets"></a><span data-ttu-id="8998e-184">Importieren der Azure-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="8998e-184">Import the Azure cmdlets</span></span>
<span data-ttu-id="8998e-185">PowerShell lädt beim Start standardmäßig nur die wichtigsten Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8998e-185">At startup, PowerShell loads only the core cmdlets by default.</span></span> <span data-ttu-id="8998e-186">Das bedeutet, dass das Cmdlet, dass mit Azure arbeiten muss, nicht geladen wird.</span><span class="sxs-lookup"><span data-stu-id="8998e-186">This means the cmdlets you need to work with Azure won't be loaded.</span></span> <span data-ttu-id="8998e-187">Die zuverlässigste Option zum Laden der benötigten Cmdlets besteht darin, diese manuell zu Beginn der PowerShell-Sitzung zu importieren.</span><span class="sxs-lookup"><span data-stu-id="8998e-187">The most reliable way to load the cmdlets you need is to import them manually at the start of your PowerShell session.</span></span>

<span data-ttu-id="8998e-188">Sie verwenden das Cmdlet **Import-Module** zum Laden von Modulen.</span><span class="sxs-lookup"><span data-stu-id="8998e-188">You use the **Import-Module** cmdlet to load modules.</span></span> <span data-ttu-id="8998e-189">Dieses Cmdlet verfügt über viele Parameter, die für unterschiedliche Situationen geeignet sind.</span><span class="sxs-lookup"><span data-stu-id="8998e-189">This cmdlet has many parameters to handle a variety of situations.</span></span> <span data-ttu-id="8998e-190">Beispielsweise kann es mehrere Module, eine bestimmte Modulversion, Teile eines Moduls usw. laden.</span><span class="sxs-lookup"><span data-stu-id="8998e-190">For example, it can load multiple modules, a specific module version, part of a module, and so on.</span></span>

<span data-ttu-id="8998e-191">Beispielsweise können wir alle Cmdlets für AzureRM mit dem folgenden Befehl **in einer PowerShell-Sitzung mit erhöhten Rechten** laden:</span><span class="sxs-lookup"><span data-stu-id="8998e-191">For example, we can load all the cmdlets for AzureRM with the following command **in an elevated PowerShell session**:</span></span>

<span data-ttu-id="8998e-192">:::zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="8998e-192">:::zone pivot="windows"</span></span>

```powershell
Import-Module AzureRM
```

<span data-ttu-id="8998e-193">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="8998e-193">:::zone-end</span></span>

<span data-ttu-id="8998e-194">::: zone pivot="linux,macos"</span><span class="sxs-lookup"><span data-stu-id="8998e-194">::: zone pivot="linux,macos"</span></span>

```powershell
Import-Module AzureRM.NetCore
```

<span data-ttu-id="8998e-195">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="8998e-195">:::zone-end</span></span>

> [!TIP]
> <span data-ttu-id="8998e-196">Wenn Sie häufig mit Azure PowerShell arbeiten, haben Sie zwei Möglichkeiten, um den Modulladeprozess zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="8998e-196">If you find that you work with Azure PowerShell frequently, there are two ways you can automate the module-loading process.</span></span> <span data-ttu-id="8998e-197">Sie können Ihrem PowerShell-Profil einen Eintrag hinzufügen, um das Azure-Modul beim Start zu importieren, oder die aktuellste Versionen von PowerShell verwenden, die das enthaltende Modul automatisch lädt, wenn Sie das Cmdlet verwenden.</span><span class="sxs-lookup"><span data-stu-id="8998e-197">You can add an entry to your PowerShell profile to import the Azure module at startup or use the latest versions of PowerShell, which loads the containing module automatically when you use a cmdlet.</span></span>

### <a name="connect"></a><span data-ttu-id="8998e-198">Verbinden</span><span class="sxs-lookup"><span data-stu-id="8998e-198">Connect</span></span>
<span data-ttu-id="8998e-199">Wenn Sie mit einer lokalen Installation von Azure PowerShell arbeiten, müssen Sie sich zunächst authentifizieren, um Azure-Befehle ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="8998e-199">When you are working with a local install of Azure PowerShell, you will need to authenticate before you can execute Azure commands.</span></span> <span data-ttu-id="8998e-200">Das Cmdlet **Connect-AzureRmAccount** ruft Ihre Azure-Anmeldeinformationen ab und stellt dann eine Verbindung mit Ihrem Azure-Abonnement her.</span><span class="sxs-lookup"><span data-stu-id="8998e-200">The **Connect-AzureRmAccount** cmdlet prompts for your Azure credentials and then connects to your Azure subscription.</span></span> <span data-ttu-id="8998e-201">Es hat viele optionale Parameter. Aber wenn Sie nur eine interaktive Eingabeaufforderung benötigen, sind keine Parameter erforderlich:</span><span class="sxs-lookup"><span data-stu-id="8998e-201">It has many optional parameters, but if all you need is an interactive prompt, no parameters are needed:</span></span>

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="8998e-202">Sie müssen diese Schritte für jede neue PowerShell-Sitzung wiederholen, die Sie starten, da dieses Modul nicht Teil des Kernsatzes ist.</span><span class="sxs-lookup"><span data-stu-id="8998e-202">You'll need to repeat these steps for every new PowerShell session you start since this module is not part of the core set.</span></span>


### <a name="working-with-subscriptions"></a><span data-ttu-id="8998e-203">Arbeiten mit Abonnements</span><span class="sxs-lookup"><span data-stu-id="8998e-203">Working with subscriptions</span></span>
<span data-ttu-id="8998e-204">Falls Sie noch keine Erfahrung mit Azure haben, verfügen Sie wahrscheinlich nur über ein einzelnes Abonnement.</span><span class="sxs-lookup"><span data-stu-id="8998e-204">If you are new to Azure, you probably only have a single subscription.</span></span> <span data-ttu-id="8998e-205">Wenn Sie Azure hingegen schon eine Weile verwenden, haben Sie unter Umständen bereits mehrere Azure-Abonnements erstellt.</span><span class="sxs-lookup"><span data-stu-id="8998e-205">But if you have been using Azure for a while, you may have created multiple Azure subscriptions.</span></span> <span data-ttu-id="8998e-206">Sie können Azure PowerShell so konfigurieren, dass Befehle für ein bestimmtes Abonnement ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="8998e-206">You can configure Azure PowerShell to execute commands against a particular subscription.</span></span>

<span data-ttu-id="8998e-207">Hierfür kann nur jeweils ein Abonnement verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8998e-207">You can only be in one subscription at a time.</span></span> <span data-ttu-id="8998e-208">Verwenden Sie das Cmdlet `Get-AzureRmContext`, um zu ermitteln, welches Abonnement aktiv ist.</span><span class="sxs-lookup"><span data-stu-id="8998e-208">Use the `Get-AzureRmContext` cmdlet to determine which subscription is active.</span></span> <span data-ttu-id="8998e-209">Falls es nicht das richtige Abonnement ist, können Sie es ändern.</span><span class="sxs-lookup"><span data-stu-id="8998e-209">If it's not the correct one, you can change it.</span></span>

1. <span data-ttu-id="8998e-210">Rufen Sie mit dem Befehl `Get-AzureRmSubscription` eine Liste mit allen Abonnementnamen Ihres Kontos ab.</span><span class="sxs-lookup"><span data-stu-id="8998e-210">Get a list of all subscription names in your account with the `Get-AzureRmSubscription` command.</span></span> 

2. <span data-ttu-id="8998e-211">Ändern Sie das Abonnement, indem Sie den Namen des gewünschten Abonnements übergeben.</span><span class="sxs-lookup"><span data-stu-id="8998e-211">Change the subscription by passing the name of the one to select.</span></span>

```powershell
Select-AzureRmSubscription -Subscription "Visual Studio Enterprise"
```

### <a name="get-a-list-of-all-resource-groups"></a><span data-ttu-id="8998e-212">Abrufen einer Liste mit allen Ressourcengruppen</span><span class="sxs-lookup"><span data-stu-id="8998e-212">Get a list of all Resource Groups</span></span>

<span data-ttu-id="8998e-213">Sie können eine Liste mit allen Ressourcengruppen des aktiven Abonnements abrufen:</span><span class="sxs-lookup"><span data-stu-id="8998e-213">You can retrieve a list of all Resource Groups in the active subscription:</span></span>

```powershell
Get-AzureRmResourceGroup
```

<span data-ttu-id="8998e-214">Wenn Sie eine kürzere Übersicht erhalten möchten, können Sie die Ausgabe von `Get-AzureRmResourceGroup` per Pipezeichen („|“) an das Cmdlet `Format-Table` senden.</span><span class="sxs-lookup"><span data-stu-id="8998e-214">To get a more concise view, you can send the output from the `Get-AzureRmResourceGroup` to the `Format-Table` cmdlet using a pipe '|'.</span></span>

```powershell
Get-AzureRmResourceGroup | Format-Table
```

<span data-ttu-id="8998e-215">Die Ausgabe sieht in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="8998e-215">This will output something like:</span></span>

```output
ResourceGroupName                  Location       ProvisioningState Tags TagsTable ResourceId
-----------------                  --------       ----------------- ---- --------- ----------
cloud-shell-storage-southcentralus southcentralus Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
ExerciseResources                  eastus         Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
```

### <a name="create-a-resource-group"></a><span data-ttu-id="8998e-216">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="8998e-216">Create a Resource Group</span></span>

<span data-ttu-id="8998e-217">Wie Sie wissen, ordnen Sie die Ressourcen bei ihrer Erstellung in Azure zu Verwaltungszwecken immer in einer Ressourcengruppe an.</span><span class="sxs-lookup"><span data-stu-id="8998e-217">As you know, when you are creating resources in Azure, you will always place them into a resource group for management purposes.</span></span> <span data-ttu-id="8998e-218">Eine Ressourcengruppe ist häufig eines der ersten Dinge, die Sie beim Starten einer neuen Anwendung erstellen.</span><span class="sxs-lookup"><span data-stu-id="8998e-218">A resource group is often one of the first things you will create when starting a new application.</span></span>

<span data-ttu-id="8998e-219">Sie können Ressourcengruppen mit dem Cmdlet `New-AzureRmResourceGroup` erstellen.</span><span class="sxs-lookup"><span data-stu-id="8998e-219">You can create resource groups with the `New-AzureRmResourceGroup` cmdlet.</span></span> <span data-ttu-id="8998e-220">Sie müssen einen Namen und einen Standort angeben.</span><span class="sxs-lookup"><span data-stu-id="8998e-220">You must specify a name and location.</span></span> <span data-ttu-id="8998e-221">Der Name muss innerhalb Ihres Abonnements eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="8998e-221">The name must be unique within your subscription.</span></span> <span data-ttu-id="8998e-222">Der Standort bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden (was für Sie aus Konformitätsgründen wichtig sein kann).</span><span class="sxs-lookup"><span data-stu-id="8998e-222">The location determines where the metadata for your resource group will be stored (which may be important to you for compliance reasons).</span></span> <span data-ttu-id="8998e-223">Verwenden Sie Zeichenfolgen wie „USA, Westen“, „Europa, Norden“ oder „Indien, Westen“, um den Standort anzugeben.</span><span class="sxs-lookup"><span data-stu-id="8998e-223">You use strings like "West US", "North Europe", or "West India" to specify the location.</span></span> <span data-ttu-id="8998e-224">Wie die meisten Azure-Cmdlets verfügt auch `New-AzureRmResourceGroup` über viele optionale Parameter. Die grundlegende Syntax lautet:</span><span class="sxs-lookup"><span data-stu-id="8998e-224">As with most of the Azure cmdlets, `New-AzureRmResourceGroup` has many optional parameters; however, the core syntax is:</span></span>

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

> [!NOTE]
> <span data-ttu-id="8998e-225">Zur Erinnerung: Wir arbeiten in der Azure-Sandbox, mit der die Ressourcengruppe für Sie erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="8998e-225">Remember, we will be working in the Azure sandbox which creates the Resource Group for you.</span></span> <span data-ttu-id="8998e-226">Der obige Befehl wird verwendet, wenn Sie in Ihrem eigenen Abonnement arbeiten.</span><span class="sxs-lookup"><span data-stu-id="8998e-226">The above command would be used if you work in your own subscription.</span></span>

### <a name="verify-the-resources"></a><span data-ttu-id="8998e-227">Überprüfen der Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8998e-227">Verify the resources</span></span>
<span data-ttu-id="8998e-228">Mit `Get-AzureRmResource` werden Ihre Azure-Ressourcen aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="8998e-228">The `Get-AzureRmResource` lists your Azure resources.</span></span> <span data-ttu-id="8998e-229">So können wir hier überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="8998e-229">This is useful here to verify whether creation of the resource group was successful.</span></span>

```powershell
Get-AzureRmResource
```

<span data-ttu-id="8998e-230">Wie beim Befehl `Get-AzureRmResourceGroup` auch, können Sie mit dem Cmdlet `Format-Table` eine kürzere Übersicht erhalten.</span><span class="sxs-lookup"><span data-stu-id="8998e-230">Like the `Get-AzureRmResourceGroup` command, you can get a more concise view through the `Format-Table` cmdlet.</span></span> <span data-ttu-id="8998e-231">Hier nutzen wir eine Kurzform von `ft`:</span><span class="sxs-lookup"><span data-stu-id="8998e-231">Here we will use a shorthand version `ft`:</span></span>

```powershell
Get-AzureRmResource | ft
```

<span data-ttu-id="8998e-232">Sie können auch nach bestimmten Ressourcengruppen filtern, um nur die Ressourcen aufzulisten, die dieser Gruppe zugeordnet sind:</span><span class="sxs-lookup"><span data-stu-id="8998e-232">You can also filter it to specific resource groups to only list resources associated with that group:</span></span>

```powershell
Get-AzureRmResource -ResourceGroup ExerciseResources
```

### <a name="creating-an-azure-virtual-machine"></a><span data-ttu-id="8998e-233">Erstellen eines virtuellen Azure-Computers</span><span class="sxs-lookup"><span data-stu-id="8998e-233">Creating an Azure Virtual Machine</span></span>

<span data-ttu-id="8998e-234">Eine weitere häufige Aufgabe, die mit PowerShell durchgeführt werden kann, ist die Erstellung von VMs.</span><span class="sxs-lookup"><span data-stu-id="8998e-234">Another common task that could be done with PowerShell is to create VMs.</span></span>

<span data-ttu-id="8998e-235">Azure PowerShell stellt das Cmdlet `New-AzureRmVm` bereit, um einen virtuellen Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8998e-235">Azure PowerShell provides the `New-AzureRmVm` cmdlet to create a virtual machine.</span></span> <span data-ttu-id="8998e-236">Das Cmdlet hat viele Parameter, um die große Anzahl von Konfigurationseinstellungen für virtuelle Computer zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="8998e-236">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="8998e-237">Die meisten Parameter haben sinnvolle Standardwerte, deshalb müssen Sie nur fünf Werte angeben:</span><span class="sxs-lookup"><span data-stu-id="8998e-237">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>

- <span data-ttu-id="8998e-238">**ResourceGroupName:** Die Ressourcengruppe, in der der neue virtuelle Computer platziert wird.</span><span class="sxs-lookup"><span data-stu-id="8998e-238">**ResourceGroupName**: The resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="8998e-239">**Name:** Der Name des virtuellen Computers in Azure.</span><span class="sxs-lookup"><span data-stu-id="8998e-239">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="8998e-240">**Location:** Der geografische Standort, in dem der virtuelle Computer bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="8998e-240">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="8998e-241">**Credential:** Ein Objekt, das den Benutzernamen und das Kennwort für das Administratorkonto des virtuellen Computers enthält.</span><span class="sxs-lookup"><span data-stu-id="8998e-241">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="8998e-242">Wir verwenden das Cmdlet `Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="8998e-242">We will use the `Get-Credential` cmdlet.</span></span> <span data-ttu-id="8998e-243">Bei diesem Cmdlet werden ein Benutzername und ein Kennwort abgefragt und in einem Objekt für Anmeldeinformationen verpackt.</span><span class="sxs-lookup"><span data-stu-id="8998e-243">This cmdlet will prompt for a username and password and package it into a credential object.</span></span>
- <span data-ttu-id="8998e-244">**Image**: Das Betriebssystemimage, das für den virtuellen Computer verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="8998e-244">**Image**: The operating system image to use for the VM.</span></span> <span data-ttu-id="8998e-245">Dies ist häufig eine Linux-Distribution oder Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8998e-245">This is often a Linux distribution, or Windows Server.</span></span>

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

<span data-ttu-id="8998e-246">Sie können diese Parameter direkt für das obige Cmdlet bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="8998e-246">You can supply these parameters directly to the cmdlet as shown above.</span></span> <span data-ttu-id="8998e-247">Alternativ hierzu können auch andere Cmdlets verwendet werden, um den virtuellen Computer zu konfigurieren, z.B. `Set-AzureRmVMOperatingSystem`, `Set-AzureRmVMSourceImage`, `Add-AzureRmVMNetworkInterface` und `Set-AzureRmVMOSDisk`.</span><span class="sxs-lookup"><span data-stu-id="8998e-247">Alternatively, other cmdlets can be used to configure the virtual machine, such as `Set-AzureRmVMOperatingSystem`, `Set-AzureRmVMSourceImage`, `Add-AzureRmVMNetworkInterface`, and `Set-AzureRmVMOSDisk`.</span></span>

<span data-ttu-id="8998e-248">Hier ist ein Beispiel angegeben, in dem das Cmdlet `Get-Credential` mit dem Parameter `-Credential` verknüpft wird:</span><span class="sxs-lookup"><span data-stu-id="8998e-248">Here's an example that strings the `Get-Credential` cmdlet together with the `-Credential` parameter:</span></span>

```powershell
New-AzureRmVM -Name MyVm -ResourceGroupName ExerciseResources -Credential (Get-Credential) ...
```

<span data-ttu-id="8998e-249">Das Suffix `AzureRmVM` gilt speziell für VM-basierte Befehle in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8998e-249">The `AzureRmVM` suffix is specific to VM-based commands in PowerShell.</span></span> <span data-ttu-id="8998e-250">Es gibt noch mehrere andere, die Sie verwenden können:</span><span class="sxs-lookup"><span data-stu-id="8998e-250">There are several others you can use:</span></span>

| <span data-ttu-id="8998e-251">Befehl</span><span class="sxs-lookup"><span data-stu-id="8998e-251">Command</span></span> | <span data-ttu-id="8998e-252">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8998e-252">Description</span></span> |
|---------|-------------|
| `Remove-AzureRmVM` | <span data-ttu-id="8998e-253">Löscht eine Azure-VM.</span><span class="sxs-lookup"><span data-stu-id="8998e-253">Deletes an Azure VM.</span></span> |
| `Start-AzureRmVM` | <span data-ttu-id="8998e-254">Startet eine angehaltene VM.</span><span class="sxs-lookup"><span data-stu-id="8998e-254">Start a stopped VM.</span></span> |
| `Stop-AzureRmVM` | <span data-ttu-id="8998e-255">Beendet die Ausführung einer VM.</span><span class="sxs-lookup"><span data-stu-id="8998e-255">Stop a running VM.</span></span> |
| `Restart-AzureRmVM` | <span data-ttu-id="8998e-256">Startet eine VM neu.</span><span class="sxs-lookup"><span data-stu-id="8998e-256">Restart a VM.</span></span> |
| `Update-AzureRmVM` | <span data-ttu-id="8998e-257">Aktualisiert die Konfiguration für eine VM.</span><span class="sxs-lookup"><span data-stu-id="8998e-257">Updates the configuration for a VM.</span></span> |

#### <a name="example-getting-the-information-for-a-vm"></a><span data-ttu-id="8998e-258">Beispiel: Abrufen der Informationen für eine VM</span><span class="sxs-lookup"><span data-stu-id="8998e-258">Example: getting the information for a VM</span></span>

<span data-ttu-id="8998e-259">Sie können die Liste mit den VMs in Ihrem Abonnement mit dem Befehl `Get-AzureRmVM -Status` auflisten.</span><span class="sxs-lookup"><span data-stu-id="8998e-259">You can list the VMs in your subscription with the `Get-AzureRmVM -Status` command.</span></span> <span data-ttu-id="8998e-260">Hiermit kann auch eine VM mit der `-Name`-Eigenschaft angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="8998e-260">This can also specify a VM with the `-Name` property.</span></span> <span data-ttu-id="8998e-261">Hier erfolgt die Zuweisung zu einer PowerShell-Variablen:</span><span class="sxs-lookup"><span data-stu-id="8998e-261">Here we assign it to a PowerShell variable:</span></span>

```powershell
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName ExerciseResources
```

<span data-ttu-id="8998e-262">Hierbei ist interessant, dass es sich um ein _Objekt_ handelt, mit dem Sie interagieren können.</span><span class="sxs-lookup"><span data-stu-id="8998e-262">The interesting thing is this is an _object_ you can interact with.</span></span> <span data-ttu-id="8998e-263">Beispielsweise können Sie dieses Objekt verwenden, Änderungen daran vornehmen und die Änderungen dann mit dem Befehl `Update-AzureRmVM` mithilfe eines Pushvorgangs zurück an Azure übertragen:</span><span class="sxs-lookup"><span data-stu-id="8998e-263">For example, you can take that object, make changes and then push changes back to Azure with the `Update-AzureRmVM` command:</span></span>

```powershell
$ResourceGroupName = "ExerciseResources"
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName $ResourceGroupName
$vm.HardwareProfile.vmSize = "Standard_DS3_v2"

Update-AzureRmVM -ResourceGroupName $ResourceGroupName  -VM $vm
```

<span data-ttu-id="8998e-264">Der interaktive Modus von PowerShell eignet sich für einmalige Aufgaben.</span><span class="sxs-lookup"><span data-stu-id="8998e-264">PowerShell's interactive mode is appropriate for one-off tasks.</span></span> <span data-ttu-id="8998e-265">In unserem Beispiel verwenden wir voraussichtlich die gleiche Ressourcengruppe für das gesamte Projekt, weshalb es sinnvoll ist, sie als interaktive Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8998e-265">In our example, we'll likely use the same resource group for the lifetime of the project, which means creating it interactively is reasonable.</span></span> <span data-ttu-id="8998e-266">Der interaktive Modus erweist sich für diese Aufgabe oft als schneller und einfacher als das Schreiben eines Skripts, das Sie dann nur einmal ausführen.</span><span class="sxs-lookup"><span data-stu-id="8998e-266">Interactive mode is often quicker and easier for this task than writing a script and executing that script exactly once.</span></span>