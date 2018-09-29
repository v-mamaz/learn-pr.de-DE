<span data-ttu-id="d2546-101">Ihr Webserver ist betriebsbereit und wird ausgeführt, aber Sie erkennen, dass Sie mehr Computeleistung benötigen, um die Erfahrung für Ihre Benutzer noch attraktiver zu machen.</span><span class="sxs-lookup"><span data-stu-id="d2546-101">Your web server is up and running, but you realize you need more computing power to make the experience great for your users.</span></span> <span data-ttu-id="d2546-102">Wie können Sie bewirken, dass Ihr virtueller Computer schneller ausgeführt wird?</span><span class="sxs-lookup"><span data-stu-id="d2546-102">How can you make your VM run faster?</span></span>

<span data-ttu-id="d2546-103">In Ihrem Datencenter können Sie Ihren Webserver auf leistungsfähigere Hardware verlagern, um Leistungsprobleme zu lösen.</span><span class="sxs-lookup"><span data-stu-id="d2546-103">In your data center, you might move your web server to more powerful hardware to solve performance problems.</span></span> <span data-ttu-id="d2546-104">Das Problem ist, dass Sie Ihr neues System kaufen, in Racks einbauen und betreiben müssen.</span><span class="sxs-lookup"><span data-stu-id="d2546-104">The problem is you need to buy, rack, and power your new system.</span></span> <span data-ttu-id="d2546-105">Mit Azure ist die Antwort viel einfacher.</span><span class="sxs-lookup"><span data-stu-id="d2546-105">With Azure, the answer is much simpler.</span></span>

<span data-ttu-id="d2546-106">Erfahren Sie mehr über das Skalieren, bevor Sie Ihren virtuellen Computer auf eine leistungsfähigere Größe zentral hochskalieren.</span><span class="sxs-lookup"><span data-stu-id="d2546-106">Before you scale up your VM to a more powerful size, let's first define what scale means.</span></span>

## <a name="what-is-scale"></a><span data-ttu-id="d2546-107">Was bedeutet „Skalierung“?</span><span class="sxs-lookup"><span data-stu-id="d2546-107">What is scale?</span></span>

<span data-ttu-id="d2546-108">_Skalierung_ bezieht sich auf das Hinzufügen von Netzwerkbandbreite, Arbeitsspeicher, Speicher oder Computeleistung, um eine bessere Leistung zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="d2546-108">_Scale_ refers to adding network bandwidth, memory, storage, or compute power to achieve better performance.</span></span>  

<span data-ttu-id="d2546-109">Möglicherweise haben Sie die Begriffe _zentrales Hochskalieren_ und _horizontales Hochskalieren_ schon einmal gehört.</span><span class="sxs-lookup"><span data-stu-id="d2546-109">You may have heard the terms _scaling up_ and _scaling out_.</span></span>

<span data-ttu-id="d2546-110">Zentrales Hochskalieren oder vertikales Skalieren bedeutet, dass der Arbeitsspeicher, der Speicher oder die Computeleistung auf einem vorhandenen virtuellen Computer erhöht wird.</span><span class="sxs-lookup"><span data-stu-id="d2546-110">Scaling up, or vertical scaling, means to increase the memory, storage, or compute power on an existing virtual machine.</span></span> <span data-ttu-id="d2546-111">Sie können einem Web- oder Datenbankserver z.B. zusätzlichen Arbeitsspeicher hinzufügen, um die Ausführung zu beschleunigen.</span><span class="sxs-lookup"><span data-stu-id="d2546-111">For example, you can add additional memory to a web or database server to make it run faster.</span></span>

<span data-ttu-id="d2546-112">Horizontales Hochskalieren oder horizontales Skalieren bedeutet, dass zusätzliche virtuelle Computer Ihre Anwendung unterstützen.</span><span class="sxs-lookup"><span data-stu-id="d2546-112">Scaling out, or horizontal scaling, means to additional virtual machines to power your application.</span></span> <span data-ttu-id="d2546-113">So können Sie beispielsweise viele virtuelle Computer erstellen, die auf genau die gleiche Weise konfiguriert sind, und einen Lastenausgleich verwenden, um die Arbeit auf sie zu verteilen.</span><span class="sxs-lookup"><span data-stu-id="d2546-113">For example, you might create many virtual machines configured in exactly the same way and use a load balancer to distribute work across them.</span></span>

> [!TIP]
> <span data-ttu-id="d2546-114">Die Cloud ist elastisch.</span><span class="sxs-lookup"><span data-stu-id="d2546-114">The cloud is elastic.</span></span> <span data-ttu-id="d2546-115">Sie können Ihre Bereitstellung _zentral herunter-_ oder _horizontal herunterskalieren_, wenn Sie nur vorübergehend zentral hoch- oder horizontal hochskalieren müssen.</span><span class="sxs-lookup"><span data-stu-id="d2546-115">You can _scale down_ or _scale in_ your deployment if you needed to scale up or scale out only temporarily.</span></span> <span data-ttu-id="d2546-116">Durch zentrales oder horizontales Herunterskalieren können Sie Kosten einsparen.</span><span class="sxs-lookup"><span data-stu-id="d2546-116">Scaling down or scaling in can help you save money.</span></span><br><br><span data-ttu-id="d2546-117">Ihre Cloudausgaben optimieren Sie mit **Azure Advisor** und **Azure Cost Management**.</span><span class="sxs-lookup"><span data-stu-id="d2546-117">**Azure Advisor** and **Azure Cost Management** are two services that help you optimize cloud spend.</span></span> <span data-ttu-id="d2546-118">Mit diesen beiden Diensten können Sie einen unnötigen Verbrauch identifizieren und anschließend eine Skalierung auf die tatsächlich verwendete Kapazität vornehmen.</span><span class="sxs-lookup"><span data-stu-id="d2546-118">You can use these services to identify where you're using more than you need, and then scale back to the capacity you're actually using.</span></span>

## <a name="scale-up-your-vm"></a><span data-ttu-id="d2546-119">Zentrales Hochskalieren des virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="d2546-119">Scale up your VM</span></span>

<span data-ttu-id="d2546-120">Erinnern Sie sich daran, dass Sie die Größe **Standard_DS2_v2** bei der Erstellung Ihres virtuellen Computers angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="d2546-120">Recall that you specified the size **Standard_DS2_v2** when you created your VM.</span></span> <span data-ttu-id="d2546-121">Ihr virtueller Computer verfügt zurzeit über zwei virtuelle CPUs und 7 GB Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="d2546-121">Your VM currently has two virtual CPUs and 7 GB of memory.</span></span>

<span data-ttu-id="d2546-122">Wechseln Sie zur nächsten Größe **Standard_DS3_v2**.</span><span class="sxs-lookup"><span data-stu-id="d2546-122">Let's bump up to the next size, **Standard_DS3_v2**.</span></span> <span data-ttu-id="d2546-123">Ihr virtueller Computer verfügt dann über vier virtuelle CPUs und 14 GB Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="d2546-123">Your VM will then have four virtual CPUs and 14 GB of memory.</span></span>

<span data-ttu-id="d2546-124">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="d2546-124">::: zone pivot="windows-cloud"</span></span>

1. <span data-ttu-id="d2546-125">Führen Sie `az vm resize` in Cloud Shell aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="d2546-125">From Cloud Shell, run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="d2546-126">Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="d2546-126">The update process takes about a minute.</span></span> <span data-ttu-id="d2546-127">Ihr virtueller Computer wird während des Vorgangs neu gestartet.</span><span class="sxs-lookup"><span data-stu-id="d2546-127">Your VM restarts during the process.</span></span>

1. <span data-ttu-id="d2546-128">Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="d2546-128">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="d2546-129">Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d2546-129">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```output
    Standard_DS3_v2
    ```

<span data-ttu-id="d2546-130">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="d2546-130">::: zone-end</span></span>

<span data-ttu-id="d2546-131">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="d2546-131">::: zone pivot="linux-cloud"</span></span>

1. <span data-ttu-id="d2546-132">Führen Sie `az vm resize` in Cloud Shell aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="d2546-132">From Cloud Shell, run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="d2546-133">Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="d2546-133">The update process takes about a minute.</span></span> <span data-ttu-id="d2546-134">Ihr virtueller Computer wird während des Vorgangs neu gestartet.</span><span class="sxs-lookup"><span data-stu-id="d2546-134">Your VM restarts during the process.</span></span>

1. <span data-ttu-id="d2546-135">Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="d2546-135">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="d2546-136">Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d2546-136">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```output
    Standard_DS3_v2
    ```

<span data-ttu-id="d2546-137">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="d2546-137">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="d2546-138">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="d2546-138">Summary</span></span>

<span data-ttu-id="d2546-139">Gut gemacht!</span><span class="sxs-lookup"><span data-stu-id="d2546-139">Nice job!</span></span> <span data-ttu-id="d2546-140">Mit nur einem Befehl ist Ihr virtueller Computer jetzt doppelt so leistungsfähig.</span><span class="sxs-lookup"><span data-stu-id="d2546-140">With just one command, your VM is now twice as powerful.</span></span>

<span data-ttu-id="d2546-141">Zentrales und horizontales Hochskalieren sind zwei Möglichkeiten zur Leistungsverbesserung.</span><span class="sxs-lookup"><span data-stu-id="d2546-141">Scaling up and scaling out are two ways to increase performance.</span></span> <span data-ttu-id="d2546-142">Hier haben Sie Ihren virtuellen Computer zentral hochskaliert, um seine Computeleistung zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="d2546-142">Here you scaled up your VM to increase its compute power.</span></span>