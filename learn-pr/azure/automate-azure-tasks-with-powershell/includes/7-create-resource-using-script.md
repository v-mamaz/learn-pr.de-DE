## <a name="motivation"></a><span data-ttu-id="b3b38-101">Motivation</span><span class="sxs-lookup"><span data-stu-id="b3b38-101">Motivation</span></span>
<span data-ttu-id="b3b38-102">Komplexe und wiederkehrende Aufgaben nutzen häufig viel Zeit bei der Verwaltung.</span><span class="sxs-lookup"><span data-stu-id="b3b38-102">Complex or repetitive tasks often take a great deal of administrative time.</span></span> <span data-ttu-id="b3b38-103">Organisationen bevorzugen zur Automatisierung dieser Aufgaben aus, um Kosten zu senken und Fehler zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="b3b38-103">Organizations prefer to automate these tasks to reduce costs and avoid errors.</span></span>

<span data-ttu-id="b3b38-104">Dies ist wichtig, im Beispiel Unternehmen (Customer Relationship Management, CRM).</span><span class="sxs-lookup"><span data-stu-id="b3b38-104">This is important in the Customer Relationship Management (CRM) company example.</span></span> <span data-ttu-id="b3b38-105">Testen Sie Ihre Software auf mehrere virtuelle Linux-Computer (VMs), die Sie kontinuierlich löschen und neu erstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="b3b38-105">There, you test your software on multiple Linux Virtual Machines (VMs) that you need to continuously delete and recreate.</span></span> <span data-ttu-id="b3b38-106">Möchten ein PowerShell-Skript zu verwenden, um die Erstellung der virtuellen Computer zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="b3b38-106">You want to use a PowerShell script to automate the creation of the VMs.</span></span>

<span data-ttu-id="b3b38-107">Über den Basisbetrieb Erstellen eines virtuellen Computers müssen Sie einige zusätzliche Anforderungen für das Skript aus.</span><span class="sxs-lookup"><span data-stu-id="b3b38-107">Beyond the core operation of creating a VM you have a few additional requirements for your script.</span></span> 
- <span data-ttu-id="b3b38-108">Mehrere virtuelle Computer, erstellen Sie daher die Erstellung in einer Schleife aufgenommen werden soll</span><span class="sxs-lookup"><span data-stu-id="b3b38-108">You will create multiple VMs, so you want to put the creation inside a loop</span></span>
- <span data-ttu-id="b3b38-109">Sie müssen in drei verschiedenen Ressourcengruppen, VMs erstellen, damit der Name der Ressourcengruppe an das Skript als Parameter übergeben werden sollen</span><span class="sxs-lookup"><span data-stu-id="b3b38-109">You need to create VMs in three different resource groups, so the name of the resource group should be passed to the script as a parameter</span></span>

<span data-ttu-id="b3b38-110">In diesem Abschnitt sehen Sie, wie Sie schreiben, und führen Sie ein Azure PowerShell-Skript, das diese Anforderungen erfüllt.</span><span class="sxs-lookup"><span data-stu-id="b3b38-110">In this section, you will see how to write and execute an Azure PowerShell script that meets these requirements.</span></span>

## <a name="what-is-a-powershell-script"></a><span data-ttu-id="b3b38-111">Was ist ein PowerShell-Skript?</span><span class="sxs-lookup"><span data-stu-id="b3b38-111">What is a PowerShell script?</span></span>
<span data-ttu-id="b3b38-112">Ein PowerShell-Skript ist eine Textdatei mit Befehlen und Steuerelement erstellt.</span><span class="sxs-lookup"><span data-stu-id="b3b38-112">A PowerShell script is a text file containing commands and control constructs.</span></span> <span data-ttu-id="b3b38-113">Die Befehle sind die Aufrufe der Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b3b38-113">The commands are invocations of cmdlets.</span></span> <span data-ttu-id="b3b38-114">Die Steuerelementkonstrukte sind Funktionen wie Schleifen, Variablen, Parameter, Kommentare, usw., die vom PowerShell Programmierung.</span><span class="sxs-lookup"><span data-stu-id="b3b38-114">The control constructs are programming features like loops, variables, parameters, comments, etc. supplied by PowerShell.</span></span>

<span data-ttu-id="b3b38-115">PowerShell-Skriptdateien haben ein **ps1** Dateierweiterung.</span><span class="sxs-lookup"><span data-stu-id="b3b38-115">PowerShell script files have a **.ps1** file extension.</span></span> <span data-ttu-id="b3b38-116">Sie können zu erstellen und speichern diese Dateien mit einem beliebigen Texteditor.</span><span class="sxs-lookup"><span data-stu-id="b3b38-116">You can create and save these files with any text editor.</span></span> 

> [!TIP] <span data-ttu-id="b3b38-117">Wenn Sie in Windows PowerShell-Skripts schreiben, können Sie die Windows PowerShell Integrated Scripting Environment (ISE) verwenden.</span><span class="sxs-lookup"><span data-stu-id="b3b38-117">If you’re writing PowerShell scripts under Windows, you can use the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="b3b38-118">Dieser Editor bietet es sich um Features wie farbliche syntaxkennzeichnung und eine Liste der verfügbaren Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b3b38-118">This editor provides features such as syntax coloring and a list of available cmdlets.</span></span>
>
>![Der Windows PowerShell ISE](../images/7-windows-powershell-ise-screenshot.png)

<span data-ttu-id="b3b38-120">Nachdem Sie das Skript geschrieben haben, führen Sie es über die PowerShell-Befehlszeile durch Übergeben des Namens der Datei, einem Punkt und ein umgekehrter Schrägstrich vorangestellt:</span><span class="sxs-lookup"><span data-stu-id="b3b38-120">Once you have written the script, execute it from the PowerShell command line by passing the name of the file preceded by a dot and a backslash:</span></span>

    ```powershell
    .\myScript.ps1
    ```

## <a name="powershell-techniques"></a><span data-ttu-id="b3b38-121">PowerShell-Verfahren</span><span class="sxs-lookup"><span data-stu-id="b3b38-121">PowerShell techniques</span></span>
<span data-ttu-id="b3b38-122">PowerShell umfasst viele Features, die in typischen Programmiersprachen gefunden.</span><span class="sxs-lookup"><span data-stu-id="b3b38-122">PowerShell has many features found in typical programming languages.</span></span> <span data-ttu-id="b3b38-123">Sie können definieren Sie Variablen, Verzweigungen und Schleifen, erfassen Befehlszeilenparameter, Schreiben von Funktionen, Hinzufügen von Kommentaren usw. Wir benötigen drei Funktionen für unser Skript: Variablen, Schleifen und Parameter.</span><span class="sxs-lookup"><span data-stu-id="b3b38-123">You can define variables, use branches and loops, capture command-line parameters, write functions, add comments, etc. We will need three features for our script: variables, loops, and parameters.</span></span>

### <a name="variables"></a><span data-ttu-id="b3b38-124">Variables</span><span class="sxs-lookup"><span data-stu-id="b3b38-124">Variables</span></span>
<span data-ttu-id="b3b38-125">PowerShell unterstützt Variablen.</span><span class="sxs-lookup"><span data-stu-id="b3b38-125">PowerShell supports variables.</span></span> <span data-ttu-id="b3b38-126">Verwendung **$** zum Deklarieren einer Variablen und **=** , einen Wert zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="b3b38-126">Use **$** to declare a variable and **=** to assign a value.</span></span> <span data-ttu-id="b3b38-127">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b3b38-127">For example:</span></span>

    ```powershell
    $loc = "East US"
    $iterations = 3
    ```

<span data-ttu-id="b3b38-128">Variablen können Objekte enthalten.</span><span class="sxs-lookup"><span data-stu-id="b3b38-128">Variables can hold objects.</span></span> <span data-ttu-id="b3b38-129">Die folgende Definition legt z. B. die **AdminCredential** -Variable auf das von zurückgegebene Objekt der **Get-Credential** Cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b3b38-129">For example, the following definition sets the **adminCredential** variable to the object returned by the **Get-Credential** cmdlet.</span></span>

    ```powershell
    $adminCredential = Get-Credential
    ```

<span data-ttu-id="b3b38-130">Verwenden Sie zum Abrufen des in einer Variablen gespeicherten Wertes dem **$** Präfix und den Namen, wie unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="b3b38-130">To obtain the value stored in a variable, use the **$** prefix and its name as shown below:</span></span> 

    ```powershell
    $loc = "East US"
    New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
    ```

### <a name="loops"></a><span data-ttu-id="b3b38-131">Schleifen</span><span class="sxs-lookup"><span data-stu-id="b3b38-131">Loops</span></span>
<span data-ttu-id="b3b38-132">PowerShell verfügt über mehrere Schleifen: **für**, **tun... Während**, **für... Jede**usw. Die **für** Schleife ist die beste Übereinstimmung für unsere Anforderungen, da wir ein Cmdlet eine feste Anzahl von ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b3b38-132">PowerShell has several loops: **For**, **Do...While**, **For...Each**, etc. The **For** loop is the best match for our needs because we will execute a cmdlet a fixed number of times.</span></span>

<span data-ttu-id="b3b38-133">Die Core-Syntax ist unten dargestellt; In diesem Beispiel wird für zwei Iterationen ausgeführt und den Wert des **ich** jedes Mal.</span><span class="sxs-lookup"><span data-stu-id="b3b38-133">The core syntax is shown below; the example runs for two iterations and prints the value of **i** each time.</span></span> <span data-ttu-id="b3b38-134">Die Vergleichsoperatoren werden geschrieben, **- Lt** für "kleiner als" **-le** für "kleiner als oder gleich" **Eq** für "gleich" **Ne** für "nicht gleich", usw.</span><span class="sxs-lookup"><span data-stu-id="b3b38-134">The comparison operators are written **-lt** for "less than", **-le** for "less than or equal", **eq** for "equal", **ne** for "not equal", etc.</span></span>

    ```powershell
    For ($i = 1; $i -lt 3; $i++)
    {
        $i
    }
    ```

### <a name="parameters"></a><span data-ttu-id="b3b38-135">Parameter</span><span class="sxs-lookup"><span data-stu-id="b3b38-135">Parameters</span></span>
<span data-ttu-id="b3b38-136">Wenn Sie ein Skript ausführen, können Sie Argumente in der Befehlszeile übergeben.</span><span class="sxs-lookup"><span data-stu-id="b3b38-136">When you execute a script, you can pass arguments on the command line.</span></span> <span data-ttu-id="b3b38-137">Sie können Namen für jeden Parameter können Sie das Skript die Werte zu extrahieren, bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="b3b38-137">You can provide names for each parameter to help the script extract the values.</span></span> <span data-ttu-id="b3b38-138">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b3b38-138">For example:</span></span>

    ```powershell
    .\setupEnvironment.ps1 -size 5 -location "East US"
    ```

<span data-ttu-id="b3b38-139">Innerhalb des Skripts erfassen Sie die Werte in Variablen an.</span><span class="sxs-lookup"><span data-stu-id="b3b38-139">Inside the script, you capture the values into variables.</span></span> <span data-ttu-id="b3b38-140">In diesem Beispiel werden die Parameter nach Namen abgeglichen:</span><span class="sxs-lookup"><span data-stu-id="b3b38-140">In this example, the parameters are matched by name:</span></span>

    ```powershell
    param([string]$location, [int]$size)
    ```

<span data-ttu-id="b3b38-141">Sie können die Namen über die Befehlszeile weglassen.</span><span class="sxs-lookup"><span data-stu-id="b3b38-141">You can omit the names from the command line.</span></span> <span data-ttu-id="b3b38-142">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b3b38-142">For example:</span></span>

    ```powershell
    .\setupEnvironment.ps1 5 "East US"
    ```

<span data-ttu-id="b3b38-143">Verwenden Sie innerhalb des Skripts Position für den Abgleich, wenn der Parameter unbenannt sind:</span><span class="sxs-lookup"><span data-stu-id="b3b38-143">Inside the script, you rely on position for matching when the parameters are unnamed:</span></span>

    ```powershell
    param([int]$size, [string]$location)
    ```

## <a name="how-to-create-a-linux-virtual-machine"></a><span data-ttu-id="b3b38-144">Vorgehensweise: Erstellen einer Linux-VM</span><span class="sxs-lookup"><span data-stu-id="b3b38-144">How to create a Linux Virtual Machine</span></span>
<span data-ttu-id="b3b38-145">Azure PowerShell bietet die **New-AzureRmVm** -Cmdlet zum Erstellen eines virtuellen Computers.</span><span class="sxs-lookup"><span data-stu-id="b3b38-145">Azure PowerShell provides the **New-AzureRmVm** cmdlet to create a Virtual Machine.</span></span> <span data-ttu-id="b3b38-146">Das Cmdlet verfügt über viele Parameter, damit es die große Anzahl von VM-Konfigurationseinstellungen verarbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="b3b38-146">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="b3b38-147">Die meisten Parameter haben sinnvolle Standardwerte, daher wir nur fünf Dinge anzugeben müssen:</span><span class="sxs-lookup"><span data-stu-id="b3b38-147">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>
- <span data-ttu-id="b3b38-148">**ResourceGroupName**: die Ressourcengruppe, in dem der neue virtuelle Computer platziert werden.</span><span class="sxs-lookup"><span data-stu-id="b3b38-148">**ResourceGroupName**: the resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="b3b38-149">**Namen**: der Name des virtuellen Computers in Azure.</span><span class="sxs-lookup"><span data-stu-id="b3b38-149">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="b3b38-150">**Speicherort**: geografischen Standort, in dem der virtuelle Computer bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="b3b38-150">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="b3b38-151">**Anmeldeinformationen**: ein Objekt mit dem Benutzernamen und Kennwort für das Administratorkonto des virtuellen Computers.</span><span class="sxs-lookup"><span data-stu-id="b3b38-151">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="b3b38-152">Wir verwenden die **Get-Credential** Cmdlet zur Eingabe eines Benutzernamens und Kennworts auffordert.</span><span class="sxs-lookup"><span data-stu-id="b3b38-152">We will use the **Get-Credential** cmdlet to prompt for a username and password.</span></span> <span data-ttu-id="b3b38-153">**Get-Credential** Pakete des Benutzernamens und Kennworts in ein Objekt mit Anmeldeinformationen der als Ergebnis zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="b3b38-153">**Get-Credential** packages the username and password into a credential object which it returns as its result.</span></span>
- <span data-ttu-id="b3b38-154">**Image**: Identität des Betriebssystems für den virtuellen Computer verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b3b38-154">**Image**: Identity of the operating system to use for the VM.</span></span> <span data-ttu-id="b3b38-155">Wir verwenden "UbuntuLTS".</span><span class="sxs-lookup"><span data-stu-id="b3b38-155">We will use "UbuntuLTS".</span></span>

<span data-ttu-id="b3b38-156">Die Syntax für das Cmdlet ist unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="b3b38-156">The syntax for the cmdlet is shown below:</span></span>

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a><span data-ttu-id="b3b38-157">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="b3b38-157">Summary</span></span>
<span data-ttu-id="b3b38-158">Die Kombination von PowerShell und Azure PowerShell bietet Ihnen die Tools, die für die Sie benötigen, Automatisieren von Azure.</span><span class="sxs-lookup"><span data-stu-id="b3b38-158">The combination of PowerShell and Azure PowerShell gives you all the tools you need to automate Azure.</span></span> <span data-ttu-id="b3b38-159">In unserem Beispiel CRM werden wir erstellen mehrere Linux-VMs, die mit einem Parameter, um das Skript generische zu halten und einer Schleife, um wiederholte Code zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="b3b38-159">In our CRM example, we will be able to create multiple Linux VMs using a parameter to keep the script generic and a loop to avoid repeated code.</span></span> <span data-ttu-id="b3b38-160">Dies bedeutet, dass ein ehemals komplexer Vorgang jetzt in einem einzigen Schritt ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="b3b38-160">This means that a formerly complex operation can now be executed in a single step.</span></span>