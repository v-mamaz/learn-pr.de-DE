<span data-ttu-id="88305-101">Das Azure-Portal ist der einfachste Weg, um anfangs Ressourcen wie VMs zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="88305-101">The Azure portal is the easiest way to create resources such as VMs when you are getting started.</span></span> <span data-ttu-id="88305-102">Allerdings stellt Azure nicht unbedingt die effizienteste oder schnellste Möglichkeit dar, insbesondere wenn Sie mehrere Ressourcen gleichzeitig erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="88305-102">However, it's not necessarily the most efficient or quickest way to work with Azure, particularly if you need to create several resources together.</span></span> <span data-ttu-id="88305-103">In unserem Fall werden wir Dutzende von VMs erstellen, um verschiedene Aufgaben zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="88305-103">In our case, we will eventually be creating dozens of VMs to handle different tasks.</span></span> <span data-ttu-id="88305-104">Es wäre umständlich und lästig, sie manuell im Azure-Portal zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="88305-104">Creating them manually in the Azure portal wouldn't be a fun task!</span></span>

<span data-ttu-id="88305-105">Betrachten wir einige andere Methoden, um Ressourcen in Azure zu erstellen und zu verwalten:</span><span class="sxs-lookup"><span data-stu-id="88305-105">Let's look at some other ways to create and administer resources in Azure:</span></span>

- [<span data-ttu-id="88305-106">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88305-106">Azure Resource Manager</span></span>](#Azure_RM)
- [<span data-ttu-id="88305-107">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="88305-107">Azure PowerShell</span></span>](#Azure_PowerShell)
- [<span data-ttu-id="88305-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="88305-108">Azure CLI</span></span>](#Azure_CLI)
- [<span data-ttu-id="88305-109">Azure-REST-API</span><span class="sxs-lookup"><span data-stu-id="88305-109">Azure REST API</span></span>](#Azure_REST_API)
- [<span data-ttu-id="88305-110">Azure-Client SDK</span><span class="sxs-lookup"><span data-stu-id="88305-110">Azure Client SDK</span></span>](#Azure_Client_SDK)
- [<span data-ttu-id="88305-111">Azure-VM-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="88305-111">Azure VM Extensions</span></span>](#Azure_VMExtensions)
- [<span data-ttu-id="88305-112">Azure Automation-Dienste</span><span class="sxs-lookup"><span data-stu-id="88305-112">Azure Automation Services</span></span>](#Azure_Automation)

<a name="Azure_RM" />

## <a name="azure-resource-manager"></a><span data-ttu-id="88305-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88305-113">Azure Resource Manager</span></span>

<span data-ttu-id="88305-114">Angenommen, Sie wollen eine Kopie einer VM mit den gleichen Einstellungen erstellen.</span><span class="sxs-lookup"><span data-stu-id="88305-114">Let's assume you want to create a copy of a VM with the same settings.</span></span> <span data-ttu-id="88305-115">Sie können ein VM-Image erstellen, es in Azure hochladen und als Grundlage für Ihre neue VM verwenden.</span><span class="sxs-lookup"><span data-stu-id="88305-115">You could create a VM image, upload it to Azure and reference it as the basis for your new VM.</span></span> <span data-ttu-id="88305-116">Dieses Vorgehen ist ineffizient und zeitaufwändig.</span><span class="sxs-lookup"><span data-stu-id="88305-116">This process is inefficient and time-consuming.</span></span> <span data-ttu-id="88305-117">Azure bietet Ihnen die Möglichkeit, eine Vorlage zu erstellen, aus der Sie eine genaue Kopie einer VM erstellen können.</span><span class="sxs-lookup"><span data-stu-id="88305-117">Azure provides you with the option to create a template from which to create an exact copy of a VM.</span></span>

<span data-ttu-id="88305-118">In der Regel enthält Ihre Azure-Infrastruktur viele Ressourcen, von denen viele in irgendeiner Weise miteinander verbunden sind.</span><span class="sxs-lookup"><span data-stu-id="88305-118">Typically, your Azure infrastructure will contain many resources, many of them related to one another in some way.</span></span> <span data-ttu-id="88305-119">Beispielsweise verfügt die von uns erstellte VM über den virtuellen Computer selbst, Speicher, Netzwerkschnittstelle, Webserver und eine Datenbank – allesamt erstellt, um die WordPress-Website auszuführen.</span><span class="sxs-lookup"><span data-stu-id="88305-119">For example, the VM we created has the virtual machine itself, storage, network interface, web server, and a database - all created together to run the WordPress site.</span></span> <span data-ttu-id="88305-120">**Azure Resource Manager** gestaltet die Arbeit mit diesen zugehörigen Ressourcen effizienter.</span><span class="sxs-lookup"><span data-stu-id="88305-120">**Azure Resource Manager** makes working with these related resources more efficient.</span></span> <span data-ttu-id="88305-121">Er organisiert Ressourcen in benannten **Ressourcengruppen**, mit denen Sie alle Ressourcen gleichzeitig bereitstellen, aktualisieren oder löschen können.</span><span class="sxs-lookup"><span data-stu-id="88305-121">It organizes resources into named **Resource Groups** that let you deploy, update, or delete all of the resources together.</span></span> <span data-ttu-id="88305-122">Beim Erstellen der WordPress-Website haben wir die Ressourcengruppe als Teil der VM-Erstellung identifiziert, und der Resource Manager hat die zugehörigen Ressourcen in derselben Gruppe platziert.</span><span class="sxs-lookup"><span data-stu-id="88305-122">When we created the WordPress site, we identified the Resource Group as part of the VM creation, and Resource Manager placed the associated resources into the same group.</span></span>

<span data-ttu-id="88305-123">Resource Manager ermöglicht Ihnen auch, _Vorlagen_ zu erstellen, mit denen Sie bestimmte Konfigurationen erstellen und bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="88305-123">Resource Manager also allows you to create _templates_ which can be used to create and deploy specific configurations.</span></span>

### <a name="what-are-resource-manager-templates"></a><span data-ttu-id="88305-124">Was sind Resource Manager-Vorlagen?</span><span class="sxs-lookup"><span data-stu-id="88305-124">What are Resource Manager templates?</span></span>

<span data-ttu-id="88305-125">**Resource Manager-Vorlagen** sind JSON-Dateien, mit denen die Ressourcen definiert werden, die Sie für Ihre Lösung bereitstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="88305-125">**Resource Manager templates** are JSON files that define the resources you need to deploy for your solution.</span></span>

<span data-ttu-id="88305-126">Sie können diese Vorlagen im Abschnitt **Einstellungen** für eine bestimmte VM erstellen, indem Sie die Option „Automatisierungsskript“ auswählen.</span><span class="sxs-lookup"><span data-stu-id="88305-126">You can create resource templates from the **Settings** section for a specific VM by selecting the Automation script option.</span></span>

![Automatisierungsskript für die VM](../media-draft/4-automation-script.png)

<span data-ttu-id="88305-128">Sie haben die Möglichkeit, die Resource Manager-Vorlage für die spätere Verwendung zu speichern oder direkt eine neue VM auf Basis dieser Vorlage bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="88305-128">You have the option to save the resource template for later use or immediately deploy a new VM based on this template.</span></span> <span data-ttu-id="88305-129">Sie können beispielsweise eine VM aus einer Vorlage in einer Testumgebung erstellen und feststellen, dass sie Ihren lokalen Computer nicht ganz ersetzt.</span><span class="sxs-lookup"><span data-stu-id="88305-129">For example, you might create a VM from a template in a test environment and find it doesn’t quite work to replace your on-premise machine.</span></span> <span data-ttu-id="88305-130">Sie können die Ressourcengruppe löschen, wodurch alle Ressourcen gelöscht werden, die Vorlage optimieren und es dann erneut versuchen.</span><span class="sxs-lookup"><span data-stu-id="88305-130">You can delete the resource group, which deletes all of the resources, tweak the template and try again.</span></span> <span data-ttu-id="88305-131">Wenn Sie nur Änderungen an den vorhandenen, bereitgestellten Ressourcen vornehmen möchten, können Sie die Vorlage, mit der sie erstellt wurden, ändern und erneut bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="88305-131">If you only want to make changes to the existing deployed resources, you can change the template used to create it and deploy it again.</span></span> <span data-ttu-id="88305-132">Resource Manager ändert die Ressourcen entsprechend der neuen Vorlage.</span><span class="sxs-lookup"><span data-stu-id="88305-132">Resource Manager will change the resources to match the new template.</span></span>

<span data-ttu-id="88305-133">Sobald alles Ihren Vorstellungen entspricht, können Sie mit dieser Vorlage mehrere Versionen Ihrer Infrastruktur erstellen, z.B. für das Staging und die Produktion.</span><span class="sxs-lookup"><span data-stu-id="88305-133">Once you have it working the way you want it, you can take that template and easily re-create multiple versions of your infrastructure, such as staging and production.</span></span> <span data-ttu-id="88305-134">Sie können Felder wie VM-Name, Netzwerkname, Speicherkontoname parametrisieren und die Vorlage mit verschiedenen Parametern wiederholt laden, um jede Umgebung anzupassen.</span><span class="sxs-lookup"><span data-stu-id="88305-134">You can parameterize fields such as the VM name, network name, storage account name, etc., and load the template repeatedly, using different parameters to customize each environment.</span></span>

<span data-ttu-id="88305-135">Mit Automatisierungsskripttools wie Azure CLI, Azure PowerShell oder den Azure-REST-APIs mit Ihrer bevorzugten Programmiersprache lassen sich Resource Manager-Vorlagen verarbeiten. Das macht Azure Resource Manager zu einem leistungsstarken Tool für das schnelle Erstellen Ihrer Infrastruktur.</span><span class="sxs-lookup"><span data-stu-id="88305-135">You can use automation scripting tools such as the Azure CLI, Azure PowerShell, or even the Azure REST APIs with your favorite programming language to process resource templates making this a powerful tool for quickly spinning up your infrastructure.</span></span>

<a name="Azure_PowerShell" />

## <a name="azure-powershell"></a><span data-ttu-id="88305-136">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="88305-136">Azure PowerShell</span></span>

<span data-ttu-id="88305-137">Das Erstellen von Verwaltungsskripts ist eine leistungsstarke Möglichkeit, um Ihren Workflow zu optimieren. Sie können alltägliche, sich wiederholende Aufgaben automatisieren. Sobald ein Skript verifiziert wurde, wird es konsistent ausgeführt, wodurch Fehler reduziert werden.</span><span class="sxs-lookup"><span data-stu-id="88305-137">Creating administration scripts is a powerful way to optimize your workflow, you can automate everyday, repetitive tasks, and once a script has been verified, it will run consistently, likely reducing errors.</span></span> <span data-ttu-id="88305-138">**Azure PowerShell** eignet sich ideal für einmalige interaktive Aufgaben und das Automatisieren sich wiederholender Aufgaben.</span><span class="sxs-lookup"><span data-stu-id="88305-138">**Azure PowerShell** is ideal for one-off interactive tasks and or the automate of repeated tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="88305-139">PowerShell ist eine plattformübergreifende Shell, die Dienste wie Shellfenster und Befehlsanalysen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="88305-139">PowerShell is a cross-platform shell that provides services like the shell window and command parsing.</span></span> <span data-ttu-id="88305-140">Azure PowerShell ist ein optionales Add-On-Paket, das die Azure-spezifischen Befehle hinzufügt – die sogenannten **Cmdlets**.</span><span class="sxs-lookup"><span data-stu-id="88305-140">Azure PowerShell is an optional add-on package which adds the Azure-specific commands (referred to as **cmdlets**).</span></span> <span data-ttu-id="88305-141">Weitere Informationen zur Installation und Verwendung von Azure PowerShell bietet ein separates Schulungsmodul.</span><span class="sxs-lookup"><span data-stu-id="88305-141">You can learn more about installing and using Azure PowerShell in a separate training module.</span></span>

<span data-ttu-id="88305-142">Beispielsweise können Sie mit dem `New-AzureRmVM`-Cmdlet eine neue Azure-VM erstellen.</span><span class="sxs-lookup"><span data-stu-id="88305-142">For example, you can use the `New-AzureRmVM` cmdlet to create a new Azure Virtual Machine.</span></span> 

```powershell
New-AzureRmVm `
    -ResourceGroupName "TestResourceGroup" `
    -Name "test-wp1-eus-vm" `
    -Location "East US" `
    -VirtualNetworkName "test-wp1-eus-network" `
    -SubnetName "default" `
    -SecurityGroupName "test-wp1-eus-nsg" `
    -PublicIpAddressName "test-wp1-eus-pubip" `
    -OpenPorts 80,3389
```

<span data-ttu-id="88305-143">Wie hier gezeigt, geben Sie verschiedene Parameter an, um die zahlreichen verfügbaren VM-Konfigurationseinstellungen zu behandeln.</span><span class="sxs-lookup"><span data-stu-id="88305-143">As shown here, you supply various parameters to handle the large number of VM configuration settings available.</span></span> <span data-ttu-id="88305-144">Die meisten Parameter haben sinnvolle Werte – Sie müssen nur die erforderlichen Parameter angeben.</span><span class="sxs-lookup"><span data-stu-id="88305-144">Most of the parameters have reasonable values; you only need to specify the required parameters.</span></span> <span data-ttu-id="88305-145">Weitere Informationen zum Erstellen und Verwalten von VMs mit Azure PowerShell finden Sie im Modul **Automatisieren von Azure-Aufgaben mithilfe von Skripts mit PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="88305-145">Learn more about creating and managing VMs with Azure PowerShell in the **Automate Azure tasks using scripts with PowerShell** module.</span></span>
<a name="Azure_CLI" />

## <a name="azure-cli"></a><span data-ttu-id="88305-146">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="88305-146">Azure CLI</span></span>

<span data-ttu-id="88305-147">Eine weitere Option für das Erstellen von Skripts und Verwenden von Befehlszeilen in Azure ist die **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="88305-147">Another option for scripting and command-line Azure interaction is the **Azure CLI**.</span></span>

<span data-ttu-id="88305-148">Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen wie VMs und Dateiträgern über die Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="88305-148">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources such as virtual machines and disks from the command line.</span></span> <span data-ttu-id="88305-149">Sie steht für macOS, Linux und Windows sowie unter Verwendung von Cloud Shell im Browser zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="88305-149">It's available for macOS, Linux, and Windows, or in the browser using the Cloud Shell.</span></span> <span data-ttu-id="88305-150">Wie Azure PowerShell ist auch die Azure CLI eine leistungsstarke Option, Ihren Verwaltungsworkflow zu optimieren.</span><span class="sxs-lookup"><span data-stu-id="88305-150">Like Azure PowerShell, the Azure CLI is a powerful way to streamline your administrative workflow.</span></span> <span data-ttu-id="88305-151">Im Gegensatz zu Azure PowerShell benötigt die Azure CLI PowerShell nicht.</span><span class="sxs-lookup"><span data-stu-id="88305-151">Unlike Azure PowerShell, the Azure CLI does not need PowerShell to function.</span></span>

<span data-ttu-id="88305-152">Sie können beispielsweise eine Azure-VM mit dem Befehl `az vm create` erstellen.</span><span class="sxs-lookup"><span data-stu-id="88305-152">For example, you can create an Azure VM with the `az vm create` command.</span></span>

```bash
az vm create \
    --resource-group TestResourceGroup \
    --name test-wp1-eus-vm \
    --image win2016datacenter \
    --admin-username jonc \
    --admin-password aReallyGoodPasswordHere
```

<span data-ttu-id="88305-153">Die Azure CLI kann mit anderen Skriptsprachen verwendet werden, z.B. mit Ruby und Python.</span><span class="sxs-lookup"><span data-stu-id="88305-153">The Azure CLI can be used with other scripting languages, for example, Ruby and Python.</span></span> <span data-ttu-id="88305-154">Beide Sprachen werden häufig auf Computern verwendet, die nicht auf Windows basieren, und auf denen der Entwickler möglicherweise nicht mit PowerShell vertraut ist.</span><span class="sxs-lookup"><span data-stu-id="88305-154">Both languages are commonly used on non-windows based machines where the developer may not be familiar with PowerShell.</span></span>

<span data-ttu-id="88305-155">Weitere Informationen zum Erstellen und Verwalten von VMs finden Sie im Modul **Verwalten von VMs mit der Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="88305-155">Learn more about creating and managing VMs in the **Manage virtual machines with the Azure CLI tool** module.</span></span>

## <a name="programmatic-apis"></a><span data-ttu-id="88305-156">Programmgesteuert (APIs)</span><span class="sxs-lookup"><span data-stu-id="88305-156">Programmatic (APIs)</span></span>

<span data-ttu-id="88305-157">Im Allgemeinen sind sowohl Azure PowerShell als auch Azure CLI gute Optionen, wenn Sie einfache Skripts ausführen und Befehlszeilentools verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="88305-157">Generally speaking, both Azure PowerShell and Azure CLI are good options if you have simple scripts to run and want to stick to command-line tools.</span></span> <span data-ttu-id="88305-158">Bei komplexeren Szenarien, in denen das Erstellen und Verwalten von VMs Teil einer größeren Anwendung mit komplexer Logik ist, ist ein anderer Ansatz erforderlich.</span><span class="sxs-lookup"><span data-stu-id="88305-158">When it comes to more complex scenarios where the creation and management of VM form part of a larger application with complex logic, another approach is needed.</span></span>

<span data-ttu-id="88305-159">Sie können mit jeder Art von Ressource in Azure programmgesteuert interagieren.</span><span class="sxs-lookup"><span data-stu-id="88305-159">You can interact with every type of resource in Azure programmatically.</span></span>

<a name="Azure_REST_API" />

### <a name="azure-rest-api"></a><span data-ttu-id="88305-160">Azure-REST-API</span><span class="sxs-lookup"><span data-stu-id="88305-160">Azure REST API</span></span>

<span data-ttu-id="88305-161">Die Azure-REST-API bietet Entwicklern nach Ressourcen geordnete Vorgänge und die Möglichkeit, VMs zu erstellen und zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="88305-161">The Azure REST API provides developers operations categorized by resource as well as the ability to create and manage VMs.</span></span> <span data-ttu-id="88305-162">Vorgänge werden als URIs mit entsprechenden HTTP-Methoden (`GET`, `PUT`, `POST`, `DELETE` und `PATCH`) und einer entsprechenden Antwort verfügbar gemacht.</span><span class="sxs-lookup"><span data-stu-id="88305-162">Operations are exposed as URIs with corresponding HTTP methods (`GET`, `PUT`, `POST`, `DELETE`, and `PATCH`) and a corresponding response.</span></span>

<span data-ttu-id="88305-163">Die Azure Compute-APIs ermöglichen Ihnen den programmgesteuerten Zugriff auf virtuelle Computer und die zugehörigen unterstützenden Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="88305-163">The Azure Compute APIs give you programmatic access to virtual machines and their supporting resources.</span></span> <span data-ttu-id="88305-164">Diese API unterstützt die folgenden Vorgänge:</span><span class="sxs-lookup"><span data-stu-id="88305-164">With this API, you have operations to:</span></span>

- <span data-ttu-id="88305-165">Erstellen und Verwalten von Verfügbarkeitsgruppen</span><span class="sxs-lookup"><span data-stu-id="88305-165">Create and manage availability sets</span></span>
- <span data-ttu-id="88305-166">Hinzufügen und Verwalten von VM-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="88305-166">Add and manage virtual machine extensions</span></span>
- <span data-ttu-id="88305-167">Erstellen und Verwalten von verwalteten Datenträgern, Momentaufnahmen und Images</span><span class="sxs-lookup"><span data-stu-id="88305-167">Create and manage managed disks, snapshots, and images</span></span>
- <span data-ttu-id="88305-168">Zugreifen auf die in Azure verfügbaren Plattformimages</span><span class="sxs-lookup"><span data-stu-id="88305-168">Access the platform images available in Azure</span></span>
- <span data-ttu-id="88305-169">Abrufen von Nutzungsinformationen von Ressourcen</span><span class="sxs-lookup"><span data-stu-id="88305-169">Retrieve usage information of your resources</span></span>
- <span data-ttu-id="88305-170">Erstellen und Verwalten von VMs</span><span class="sxs-lookup"><span data-stu-id="88305-170">Create and manage virtual machines</span></span>
- <span data-ttu-id="88305-171">Erstellen und Verwalten von VM-Skalierungsgruppen</span><span class="sxs-lookup"><span data-stu-id="88305-171">Create and manage virtual machine scale sets</span></span>

<a name="Azure_Client_SDK" />

### <a name="azure-client-sdk"></a><span data-ttu-id="88305-172">Azure-Client SDK</span><span class="sxs-lookup"><span data-stu-id="88305-172">Azure Client SDK</span></span>

<span data-ttu-id="88305-173">Obwohl die REST-API plattform- und sprachunabhängig ist, achten Entwickler meist auf eine höhere Abstraktionsebene.</span><span class="sxs-lookup"><span data-stu-id="88305-173">Even though the REST API is platform and language agnostic, most often developers will look towards a higher level of abstraction.</span></span> <span data-ttu-id="88305-174">Das Azure-Client SDK kapselt die Azure-REST-API und erleichtert Entwicklern die Interaktion mit Azure erheblich.</span><span class="sxs-lookup"><span data-stu-id="88305-174">The Azure Client SDK encapsulates the Azure REST API making it much easier for developers to interact with Azure.</span></span>

<span data-ttu-id="88305-175">Die Azure-Client SDKs sind für zahlreiche Sprachen und Frameworks verfügbar, einschließlich .NET-basierter Sprachen wie C#, Java, Node.js, PHP, Python, Ruby und Go.</span><span class="sxs-lookup"><span data-stu-id="88305-175">The Azure Client SDKs are available for a variety of languages and frameworks including .NET based languages such as C#, Java, Node.js, PHP, Python, Ruby, and Go.</span></span>

<span data-ttu-id="88305-176">Hier ist ein Beispielausschnitt aus einem C#-Code, um eine Azure-VM mit dem `Microsoft.Azure.Management.Fluent`-NuGet-Paket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="88305-176">Here's an example snippet of C# code to create an Azure VM using the `Microsoft.Azure.Management.Fluent` NuGet package:</span></span>

```csharp
var azure = Azure
    .Configure()
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
// ...
var vmName = "test-wp1-eus-vm";

azure.VirtualMachines.Define(vmName)
    .WithRegion(Region.USEast)
    .WithExistingResourceGroup("TestResourceGroup")
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("jonc")
    .WithAdminPassword("aReallyGoodPasswordHere")
    .WithComputerName(vmName)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

<span data-ttu-id="88305-177">Hier ist der gleiche Ausschnitt in Java unter Verwendung von **Azure-Java SDK**:</span><span class="sxs-lookup"><span data-stu-id="88305-177">Here's the same snippet in Java using the **Azure Java SDK**:</span></span>

```java
String vmName = "test-wp1-eus-vm";
// ...
VirtualMachine virtualMachine = azure.virtualMachines()
    .define(vmName)
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("TestResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("jonc")
    .withAdminPassword("aReallyGoodPasswordHere")
    .withComputerName(vmName)
    .withSize("Standard_DS1")
    .create();
```

<a name="Azure_VMExtensions" />

## <a name="azure-vm-extensions"></a><span data-ttu-id="88305-178">Azure-VM-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="88305-178">Azure VM Extensions</span></span>

<span data-ttu-id="88305-179">Angenommen, Sie möchten nach der ersten Bereitstellung zusätzliche Software auf Ihrer VM konfigurieren und installieren.</span><span class="sxs-lookup"><span data-stu-id="88305-179">Let's assume you want to configure and install additional software on your virtual machine after the initial deployment.</span></span> <span data-ttu-id="88305-180">Sie möchten, dass diese Aufgabe eine bestimmte Konfiguration verwendet, die automatisch überwacht und ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="88305-180">You want this task to use a specific configuration, monitored and executed automatically.</span></span>

<span data-ttu-id="88305-181">**Azure-VM-Erweiterungen** sind kleine Anwendungen, mit denen Sie Aufgaben auf Azure-VMs nach der erstmaligen Bereitstellung konfigurieren und automatisieren können.</span><span class="sxs-lookup"><span data-stu-id="88305-181">**Azure VM extensions** are small applications that allow you to configure and automate tasks on Azure VMs after initial deployment.</span></span> <span data-ttu-id="88305-182">**Azure-VM-Erweiterungen** können über die Azure CLI, PowerShell, Azure Resource Manager-Vorlagen und das Azure-Portal ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="88305-182">**Azure VM extensions** can be run with the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span>

<span data-ttu-id="88305-183">Sie bündeln Erweiterungen mit einer neuen VM-Bereitstellung oder führen sie für ein bestehendes System aus.</span><span class="sxs-lookup"><span data-stu-id="88305-183">You bundle extensions with a new VM deployment or run them against an existing system.</span></span>

<a name="Azure_Automation" />

## <a name="azure-automation-services"></a><span data-ttu-id="88305-184">Azure Automation-Dienste</span><span class="sxs-lookup"><span data-stu-id="88305-184">Azure Automation Services</span></span>

<span data-ttu-id="88305-185">Zeitersparnis, Fehlerreduktion und Effizienzsteigerung sind einige der größten Herausforderungen beim Verwalten von Remoteinfrastrukturen.</span><span class="sxs-lookup"><span data-stu-id="88305-185">Saving time, reducing errors, and increasing efficiency are some of the most significant operational management challenges faced when managing remote infrastructure.</span></span> <span data-ttu-id="88305-186">Wenn Sie viele Infrastrukturdienste haben, sollten Sie in Betracht ziehen, Azure-Dienste auf einer höheren Ebene für die Ausführung auf einer höheren Ebene zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="88305-186">If you have a lot of infrastructure services, you might want to consider using higher-level services in Azure to help you operate from a higher level.</span></span>

<span data-ttu-id="88305-187">Mit **Azure Automation** können Sie Dienste zum einfachen Automatisieren häufiger, zeitaufwändiger und fehleranfälliger Verwaltungsaufgaben integrieren.</span><span class="sxs-lookup"><span data-stu-id="88305-187">**Azure Automation** allows you to integrate services that allow you to automate frequent, time-consuming and error-prone management tasks with ease.</span></span> <span data-ttu-id="88305-188">Zu diesen Diensten gehören **Prozessautomatisierung**, \*\*Konfigurationsverwaltung und **Updateverwaltung**.</span><span class="sxs-lookup"><span data-stu-id="88305-188">These services include **process automation**, \*\*configuration management, and **update management**.</span></span>

- <span data-ttu-id="88305-189">**Prozessverwaltung**.</span><span class="sxs-lookup"><span data-stu-id="88305-189">**Process Management**.</span></span> <span data-ttu-id="88305-190">Angenommen, Sie haben eine VM, die auf ein bestimmtes Fehlerereignis überwacht wird.</span><span class="sxs-lookup"><span data-stu-id="88305-190">Let's assume you have a VM that is monitored for a specific error event.</span></span> <span data-ttu-id="88305-191">Sie möchten Maßnahmen ergreifen und das Problem beheben, sobald es gemeldet wird.</span><span class="sxs-lookup"><span data-stu-id="88305-191">You want to take action and fix the problem as soon as it's reported.</span></span> <span data-ttu-id="88305-192">Mit der Prozessautomatisierung können Sie Watchertasks einrichten, die auf Ereignisse reagieren, die ggf. in Ihrem Rechenzentrum auftreten.</span><span class="sxs-lookup"><span data-stu-id="88305-192">Process automation allows you to set up watcher tasks that can respond to events that may occur in your datacenter.</span></span>

- <span data-ttu-id="88305-193">**Konfigurationsverwaltung**.</span><span class="sxs-lookup"><span data-stu-id="88305-193">**Configuration Management**.</span></span>  <span data-ttu-id="88305-194">Möglicherweise möchten Sie Softwareupdates nachverfolgen, die für das Betriebssystem verfügbar sind, das auf Ihrer VM ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="88305-194">Perhaps you want to track software updates that become available for the operating system that runs on your VM.</span></span> <span data-ttu-id="88305-195">Vielleicht möchten Sie bestimmte Updates ein- oder ausschließen.</span><span class="sxs-lookup"><span data-stu-id="88305-195">There are specific updates you may want to include or exclude.</span></span> <span data-ttu-id="88305-196">Mit der Konfigurationsverwaltung können Sie diese Updates nachverfolgen und bei Bedarf Maßnahmen ergreifen.</span><span class="sxs-lookup"><span data-stu-id="88305-196">Configuration management allows you to track these updates and take action as required.</span></span> <span data-ttu-id="88305-197">Mit dem **System Center Configuration Manager** lassen sich die PCs Ihres Unternehmens sowie Server und mobile Geräte verwalten.</span><span class="sxs-lookup"><span data-stu-id="88305-197">You use **System Center Configuration Manager** to manage your company's PC, servers, and mobile devices.</span></span> <span data-ttu-id="88305-198">Mit dem Configuration Manager können Sie diese Unterstützung auf Ihre Azure-VMs erweitern.</span><span class="sxs-lookup"><span data-stu-id="88305-198">You can extend this support to your Azure VMs with Configuration Manager.</span></span>

- <span data-ttu-id="88305-199">**Updateverwaltung**.</span><span class="sxs-lookup"><span data-stu-id="88305-199">**Update Management**.</span></span> <span data-ttu-id="88305-200">Mit der Updateverwaltung können Sie Updates und Patches für Ihre VMs verwalten.</span><span class="sxs-lookup"><span data-stu-id="88305-200">This is used to manage updates and patches for your VMs.</span></span> <span data-ttu-id="88305-201">Mit diesem Dienst haben Sie die Möglichkeit, den Status verfügbarer Updates zu bewerten, Installationen zu planen und Bereitstellungsergebnisse zu überprüfen, um sicherzustellen, dass Updates erfolgreich angewendet wurden.</span><span class="sxs-lookup"><span data-stu-id="88305-201">With this service, you're able to assess the status of available updates, schedule installation, and review deployment results to verify updates applied successfully.</span></span> <span data-ttu-id="88305-202">Die Updateverwaltung umfasst Dienste, die Prozess- und Konfigurationsverwaltung bieten.</span><span class="sxs-lookup"><span data-stu-id="88305-202">Update management incorporates services that provide process and configuration management.</span></span> <span data-ttu-id="88305-203">Sie aktivieren die Updateverwaltung für eine VM direkt über Ihr **Azure Automation**-Konto.</span><span class="sxs-lookup"><span data-stu-id="88305-203">You enable update management for a VM directly from your **Azure Automation** account.</span></span> <span data-ttu-id="88305-204">Sie können die Updateverwaltung auch für eine einzelne VM über das Blatt „Virtueller Computer“ aktivieren.</span><span class="sxs-lookup"><span data-stu-id="88305-204">You can also allow update management for a single virtual machine from the virtual machine blade in the portal.</span></span>

<span data-ttu-id="88305-205">Wie Sie sehen können, bietet Azure zahlreiche Tools zum Erstellen und Verwalten von Ressourcen. So können Sie Verwaltungsvorgänge in Prozesse integrieren, um _Ihre Workflows zu optimieren_.</span><span class="sxs-lookup"><span data-stu-id="88305-205">As you can see, Azure provides a variety of tools to create and administer resources so you can integrate management operations into a process _that works for you_.</span></span> <span data-ttu-id="88305-206">Betrachten wir nun einige andere Azure-Dienste, um zu überprüfen, ob Ihre Infrastrukturressourcen optimal ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="88305-206">Let's examine some of the other services Azure to make sure your infrastructure resources are running smoothly.</span></span>
