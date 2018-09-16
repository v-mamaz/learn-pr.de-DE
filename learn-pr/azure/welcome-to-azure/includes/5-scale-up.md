<span data-ttu-id="8eac2-101">Ihr Webserver ist betriebsbereit und wird ausgeführt, aber Sie erkennen, dass Sie mehr Computeleistung benötigen, um die Erfahrung für Ihre Benutzer noch attraktiver zu machen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-101">Your web server is up and running, but you realize you need more computing power to make the experience great for your users.</span></span> <span data-ttu-id="8eac2-102">Wie können Sie bewirken, dass Ihr virtueller Computer schneller ausgeführt wird?</span><span class="sxs-lookup"><span data-stu-id="8eac2-102">How can you make your VM run faster?</span></span>

<span data-ttu-id="8eac2-103">In Ihrem Datencenter können Sie Ihren Webserver auf leistungsfähigere Hardware verlagern, um Leistungsprobleme zu lösen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-103">In your data center, you might move your web server to more powerful hardware to solve performance problems.</span></span> <span data-ttu-id="8eac2-104">Das Problem ist, dass Sie Ihr neues System kaufen, in Racks einbauen und betreiben müssen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-104">The problem is you need to buy, rack, and power your new system.</span></span> <span data-ttu-id="8eac2-105">Mit Azure ist die Antwort viel einfacher.</span><span class="sxs-lookup"><span data-stu-id="8eac2-105">With Azure, the answer is much simpler.</span></span>

<span data-ttu-id="8eac2-106">Sie müssen Ihren virtuellen Computer nur auf eine leistungsfähigere Größe zentral hochskalieren.</span><span class="sxs-lookup"><span data-stu-id="8eac2-106">Now you'll scale up your VM to a more powerful size.</span></span> <span data-ttu-id="8eac2-107">Bevor Sie die Größe Ihres virtuellen Computers ändern, müssen Sie ihn herunterfahren oder seine Zuordnung aufheben.</span><span class="sxs-lookup"><span data-stu-id="8eac2-107">Before you change your VM's size, you must shut it down, or deallocate it.</span></span>

<span data-ttu-id="8eac2-108">Definieren wir zunächst, was „Skalierung“ bedeutet und was geschieht, wenn Sie die Zuordnung Ihres virtuellen Computers aufheben.</span><span class="sxs-lookup"><span data-stu-id="8eac2-108">First, let's define what scale means and what happens when you deallocate your VM.</span></span>

## <a name="what-is-scale"></a><span data-ttu-id="8eac2-109">Was bedeutet „Skalierung“?</span><span class="sxs-lookup"><span data-stu-id="8eac2-109">What is scale?</span></span>

<span data-ttu-id="8eac2-110">_Skalierung_ bezieht sich auf das Hinzufügen von Netzwerkbandbreite, Arbeitsspeicher, Speicher oder Computeleistung, um eine bessere Leistung zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-110">_Scale_ refers to adding network bandwidth, memory, storage, or compute power to achieve better performance.</span></span>  

<span data-ttu-id="8eac2-111">Möglicherweise haben Sie die Begriffe _zentrales Hochskalieren_ und _horizontales Hochskalieren_ schon einmal gehört.</span><span class="sxs-lookup"><span data-stu-id="8eac2-111">You may have heard the terms _scale up_ and _scale out_.</span></span>

<span data-ttu-id="8eac2-112">Zentrales Hochskalieren oder vertikales Skalieren bedeutet, dass der Arbeitsspeicher, der Speicher oder die Computeleistung auf einem vorhandenen virtuellen Computer erhöht wird.</span><span class="sxs-lookup"><span data-stu-id="8eac2-112">Scaling up, or vertical scaling, means to increase the memory, storage, or compute power on an existing virtual machine.</span></span> <span data-ttu-id="8eac2-113">Sie können einem Web- oder Datenbankserver z.B. zusätzlichen Arbeitsspeicher hinzufügen, um die Ausführung zu beschleunigen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-113">For example, you can add additional memory to a web or database server to make it run faster.</span></span>

> [!TIP]
> <span data-ttu-id="8eac2-114">Sie können Ihr System auch _zentral herunterskalieren_, wenn Sie es nur vorübergehend zentral hochskalieren mussten.</span><span class="sxs-lookup"><span data-stu-id="8eac2-114">You can also _scale down_ your system if you needed to scale up only temporarily.</span></span>

<span data-ttu-id="8eac2-115">Horizontales Hochskalieren oder horizontales Skalieren bedeutet, dass zusätzliche virtuelle Computer Ihre Anwendung unterstützen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-115">Scaling out, or horizontal scaling, means to additional virtual machines to power your application.</span></span> <span data-ttu-id="8eac2-116">So können Sie beispielsweise viele virtuelle Computer erstellen, die auf genau die gleiche Weise konfiguriert sind, und Lastenausgleich verwenden, um die Arbeit auf sie zu verteilen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-116">For example, you might create many virtual machines configured in exactly the same way and use a load balancer to distribute work across them.</span></span>

## <a name="what-is-deallocation"></a><span data-ttu-id="8eac2-117">Was bedeutet „Aufhebung der Zuordnung“?</span><span class="sxs-lookup"><span data-stu-id="8eac2-117">What is deallocation?</span></span>

<span data-ttu-id="8eac2-118">Die Aufhebung der Zuordnung ist der Vorgang, bei dem Ihr virtueller Computer heruntergefahren wird und seine Computeressourcen freigibt.</span><span class="sxs-lookup"><span data-stu-id="8eac2-118">Deallocation is the process that shuts down your VM and releases its compute resources.</span></span>

<span data-ttu-id="8eac2-119">Wenn Sie Ihren PC am Arbeitsplatz oder zu Hause herunterfahren, schließt das Betriebssystem alle Programme und weist dann die Energieverwaltungshardware an, den Computer auszuschalten.</span><span class="sxs-lookup"><span data-stu-id="8eac2-119">When you shut down your PC at work or at home, the operating system closes your programs and then notifies the power management hardware to turn off power.</span></span>

<span data-ttu-id="8eac2-120">Das Aufheben der Zuordnung eines virtuellen Computers ist ähnlich.</span><span class="sxs-lookup"><span data-stu-id="8eac2-120">Deallocating a virtual machine is similar.</span></span> <span data-ttu-id="8eac2-121">Nachdem Ihr virtueller Computer heruntergefahren wurde, gibt Azure die Hardware erneut frei, die für ihn verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="8eac2-121">After your VM shuts down, Azure reclaims the hardware used to power it.</span></span> <span data-ttu-id="8eac2-122">Ihre Datenträger und Ihr Speicher bleiben intakt.</span><span class="sxs-lookup"><span data-stu-id="8eac2-122">Your data disks and storage remain intact.</span></span> <span data-ttu-id="8eac2-123">Wenn Sie Ihren virtuellen Computer erneut starten, setzen Sie dort an, wo Sie aufgehört haben, genau wie bei Ihrem PC.</span><span class="sxs-lookup"><span data-stu-id="8eac2-123">When you start your VM back up, you pick up where you left off, just like with your PC.</span></span>

<span data-ttu-id="8eac2-124">Wenn die Zuordnung aufgehoben ist, zahlen Sie nicht für die Compute- und Netzwerkressourcen, die der virtuelle Computer verwendet.</span><span class="sxs-lookup"><span data-stu-id="8eac2-124">When deallocated, you are not billed for the compute and network resources that your virtual machine uses.</span></span> <span data-ttu-id="8eac2-125">Sie zahlen zwar weiterhin für alle zugehörigen Datenträger, die sich im Speicher befinden, aber die Gesamtkosten sind wesentlich geringer als für einen ausgeführten virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="8eac2-125">You still pay for any associated disks to sit in storage, but the overall cost is much lower than it would be if the VM were running.</span></span>

<span data-ttu-id="8eac2-126">Hier heben Sie die Zuordnung Ihres virtuellen Computers kurz auf, damit Sie seine Größe ändern können.</span><span class="sxs-lookup"><span data-stu-id="8eac2-126">Here, you'll deallocate your VM briefly so that you can resize it.</span></span> <span data-ttu-id="8eac2-127">Sie können die Zuordnung Ihrer virtuellen Computer aber auch über einen längeren Zeitraum hinweg aufheben, um Kosten zu sparen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-127">But you can also deallocate your VMs for a longer period to save cost.</span></span> <span data-ttu-id="8eac2-128">Angenommen, Sie nutzen eine Reihe von virtuellen Computern während der Arbeitszeiten zu Testzwecken.</span><span class="sxs-lookup"><span data-stu-id="8eac2-128">Say you have a bank of VMs that you use for testing during work hours.</span></span> <span data-ttu-id="8eac2-129">Sie können planen, dass die Zuordnung Ihrer virtuellen Computer Nachts und an den Wochenenden aufgehoben wird.</span><span class="sxs-lookup"><span data-stu-id="8eac2-129">You can schedule your VMs to be automatically deallocated on nights and weekends.</span></span> <span data-ttu-id="8eac2-130">Wenn Sie Überstunden machen müssen, können Sie diese virtuellen Computer manuell erneut starten.</span><span class="sxs-lookup"><span data-stu-id="8eac2-130">If you need to stay late, you can manually restart them.</span></span>

## <a name="scale-up-your-vm"></a><span data-ttu-id="8eac2-131">Zentrales Hochskalieren des virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="8eac2-131">Scale up your VM</span></span>

<span data-ttu-id="8eac2-132">Erinnern Sie sich daran, dass Sie die Größe **Standard_DS2_v2** bei der Erstellung Ihres virtuellen Computers angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="8eac2-132">Recall that you specified the size **Standard_DS2_v2** when you created your VM.</span></span> <span data-ttu-id="8eac2-133">Ihr virtueller Computer verfügt zurzeit über zwei virtuelle CPUs und 7 GB Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="8eac2-133">Your VM currently has two virtual CPUs and 7 GB of memory.</span></span>

<span data-ttu-id="8eac2-134">Wechseln Sie zur nächsten Größe **Standard_DS3_v2**.</span><span class="sxs-lookup"><span data-stu-id="8eac2-134">Let's bump up to the next size, **Standard_DS3_v2**.</span></span> <span data-ttu-id="8eac2-135">Ihr virtueller Computer verfügt dann über vier virtuelle CPUs und 14 GB Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="8eac2-135">Your VM will then have four virtual CPUs and 14 GB of memory.</span></span>

<span data-ttu-id="8eac2-136">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="8eac2-136">::: zone pivot="windows-cloud"</span></span>

1. <span data-ttu-id="8eac2-137">Führen Sie `az vm deallocate` in Cloud Shell aus, um die Zuordnung Ihres virtuellen Computers aufzuheben oder ihn zu beenden.</span><span class="sxs-lookup"><span data-stu-id="8eac2-137">From Cloud Shell, run `az vm deallocate` to deallocate, or stop, your VM.</span></span>

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    <span data-ttu-id="8eac2-138">Dieser Vorgang nimmt einige Minuten in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="8eac2-138">The process takes a couple of minutes to complete.</span></span>
1. <span data-ttu-id="8eac2-139">Führen Sie `az vm resize` aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-139">Run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="8eac2-140">Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="8eac2-140">The update process takes about a minute.</span></span>
1. <span data-ttu-id="8eac2-141">Führen Sie `az vm start` aus, um Ihren virtuellen Computer neu zu starten.</span><span class="sxs-lookup"><span data-stu-id="8eac2-141">Run `az vm start` to restart your VM.</span></span>

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    <span data-ttu-id="8eac2-142">Der Vorgang nimmt etwa eine Minute in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="8eac2-142">The process takes about a minute.</span></span>
1. <span data-ttu-id="8eac2-143">Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="8eac2-143">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="8eac2-144">Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8eac2-144">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```console
    Standard_DS3_v2
    ```

<span data-ttu-id="8eac2-145">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="8eac2-145">::: zone-end</span></span>

<span data-ttu-id="8eac2-146">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="8eac2-146">::: zone pivot="linux-cloud"</span></span>

1. <span data-ttu-id="8eac2-147">Führen Sie `az vm deallocate` in Cloud Shell aus, um die Zuordnung Ihres virtuellen Computers aufzuheben oder ihn zu beenden.</span><span class="sxs-lookup"><span data-stu-id="8eac2-147">From Cloud Shell, run `az vm deallocate` to deallocate, or stop, your VM.</span></span>

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    <span data-ttu-id="8eac2-148">Dieser Vorgang nimmt einige Minuten in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="8eac2-148">The process takes a couple of minutes to complete.</span></span>
1. <span data-ttu-id="8eac2-149">Führen Sie `az vm resize` aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-149">Run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="8eac2-150">Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="8eac2-150">The update process takes about a minute.</span></span>
1. <span data-ttu-id="8eac2-151">Führen Sie `az vm start` aus, um Ihren virtuellen Computer neu zu starten.</span><span class="sxs-lookup"><span data-stu-id="8eac2-151">Run `az vm start` to restart your VM.</span></span>

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    <span data-ttu-id="8eac2-152">Der Vorgang nimmt etwa eine Minute in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="8eac2-152">The process takes about a minute.</span></span>
1. <span data-ttu-id="8eac2-153">Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="8eac2-153">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="8eac2-154">Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8eac2-154">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```console
    Standard_DS3_v2
    ```

<span data-ttu-id="8eac2-155">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="8eac2-155">::: zone-end</span></span>

> [!NOTE]
> <span data-ttu-id="8eac2-156">Standardmäßig weist Azure Ihrem virtuellen Computer beim Beenden und Neustarten eine neue öffentliche IP-Adresse zu.</span><span class="sxs-lookup"><span data-stu-id="8eac2-156">By default, Azure assigns a new public IP address to your VM when you stop and restart it.</span></span> <span data-ttu-id="8eac2-157">Dies ist zu Lernzwecken vertretbar.</span><span class="sxs-lookup"><span data-stu-id="8eac2-157">This is OK for learning purposes.</span></span> <span data-ttu-id="8eac2-158">In der Praxis können Sie eine öffentliche IP-Adresse reservieren, die Ihrem virtuellen Computer selbst dann zugeordnet bleibt, wenn Ihr virtueller Computer neu gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="8eac2-158">In practice, you can reserve a public IP address that stays with your VM even when your VM is restarted.</span></span>

## <a name="summary"></a><span data-ttu-id="8eac2-159">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="8eac2-159">Summary</span></span>

<span data-ttu-id="8eac2-160">Gut gemacht!</span><span class="sxs-lookup"><span data-stu-id="8eac2-160">Nice job!</span></span> <span data-ttu-id="8eac2-161">Mit nur wenigen Befehlen ist Ihr virtueller Computer jetzt doppelt so leistungsfähig.</span><span class="sxs-lookup"><span data-stu-id="8eac2-161">With just a few commands, your VM is now twice as powerful.</span></span>

<span data-ttu-id="8eac2-162">Zentrales und horizontales Hochskalieren stellen zwei Möglichkeiten dar, die Leistung zu steigern.</span><span class="sxs-lookup"><span data-stu-id="8eac2-162">Scaling up and scaling out are two ways to increase performance.</span></span> <span data-ttu-id="8eac2-163">Hier haben Sie Ihren virtuellen Computer zentral hochskaliert, um seine Computeleistung zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-163">Here you scaled up your VM to increase its compute power.</span></span>

<span data-ttu-id="8eac2-164">Sie heben die Zuordnung eines virtuellen Computers auf, bevor Sie seine Größe ändern können.</span><span class="sxs-lookup"><span data-stu-id="8eac2-164">You deallocate a VM before you can resize it.</span></span> <span data-ttu-id="8eac2-165">Sie können die Zuordnung Ihrer virtuellen Computer auch aufheben, wenn sie nicht verwendet werden, um Kosten zu sparen.</span><span class="sxs-lookup"><span data-stu-id="8eac2-165">You can also deallocate your VMs when they're not in use to save costs.</span></span>