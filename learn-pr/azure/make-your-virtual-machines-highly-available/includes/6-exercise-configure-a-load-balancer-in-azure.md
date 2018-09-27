<span data-ttu-id="c0c50-101">Sie haben die wichtigsten Ressourcen für die Architektur Ihrer Onlinebank erstellt.</span><span class="sxs-lookup"><span data-stu-id="c0c50-101">You have created the key resources for your online bank architecture.</span></span> <span data-ttu-id="c0c50-102">In dieser Übung konfigurieren Sie Regeln für den Lastenausgleich und schließen das Setup dadurch ab.</span><span class="sxs-lookup"><span data-stu-id="c0c50-102">In this exercise, you will complete the setup by configuring the load-balancing rules.</span></span>

<span data-ttu-id="c0c50-103">Testen Sie den Lastenausgleich nach Abschluss des Setups, indem Sie eine VM aus dem Pool entfernen und überprüfen, ob die Clientanforderungen nicht mehr an diese VM gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="c0c50-103">Once setup is complete, you will test the load balancer by removing a VM from the pool and verifying that client requests are no longer sent to this VM.</span></span>

<span data-ttu-id="c0c50-104">Zunächst wird der Back-End-Pool im Lastenausgleich definiert.</span><span class="sxs-lookup"><span data-stu-id="c0c50-104">We'll start by defining our backend pool in the load balancer.</span></span> <span data-ttu-id="c0c50-105">Dadurch wird festgelegt, wohin eingehende Anforderungen weitergeleitet werden.</span><span class="sxs-lookup"><span data-stu-id="c0c50-105">This determines where inbound requests are routed.</span></span>

## <a name="create-a-backend-address-pool"></a><span data-ttu-id="c0c50-106">Erstellen eines Back-End-Adresspools</span><span class="sxs-lookup"><span data-stu-id="c0c50-106">Create a backend address pool</span></span>

1. <span data-ttu-id="c0c50-107">Klicken Sie im [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) im Menü auf der linken Seite auf **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-107">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), in the left menu, Select **All resources**.</span></span> <span data-ttu-id="c0c50-108">Wählen Sie dann Ihren Lastenausgleich (**woodgrove-LB**) aus der Ressourcenliste aus.</span><span class="sxs-lookup"><span data-stu-id="c0c50-108">Then, in the resource list, select your load balancer (**woodgrove-LB**).</span></span>

1. <span data-ttu-id="c0c50-109">Klicken Sie auf **Einstellungen** > **Back-End-Pools**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-109">Select **Settings** > **Backend pools**.</span></span> <span data-ttu-id="c0c50-110">Sie werden feststellen, dass bisher noch keiner definiert wurde.</span><span class="sxs-lookup"><span data-stu-id="c0c50-110">Notice we don't have any defined yet.</span></span>

1. <span data-ttu-id="c0c50-111">Klicken Sie auf **Hinzufügen**, um einen neuen Back-End-Pool hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-111">Click **Add** to add a new backend pool.</span></span>

    ![Screenshot, der das Hinzufügen eines Back-End-Pools darstellt](../media/6-backend-pools.png)

1. <span data-ttu-id="c0c50-113">Fügen Sie auf dem Blatt **Back-End-Pool hinzufügen** die folgenden Informationen hinzu:</span><span class="sxs-lookup"><span data-stu-id="c0c50-113">On the **Add backend pool** blade, add the following information:</span></span>
    - <span data-ttu-id="c0c50-114">Nennen Sie den Pool _woodgrove-BEP_.</span><span class="sxs-lookup"><span data-stu-id="c0c50-114">Name it _woodgrove-BEP_.</span></span>
    - <span data-ttu-id="c0c50-115">Verknüpfen Sie den Pool mit einer **Verfügbarkeitsgruppe**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-115">Associated the pool to an **Availability set**.</span></span>
    - <span data-ttu-id="c0c50-116">Wählen Sie _woodgrove-AS_ als Verfügbarkeitsgruppe aus.</span><span class="sxs-lookup"><span data-stu-id="c0c50-116">For the availability set, select _woodgrove-AS_.</span></span>

1. <span data-ttu-id="c0c50-117">Klicken Sie auf **Zielnetzwerk-IP-Konfiguration hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-117">Click **Add a target network IP configuration**.</span></span>

1. <span data-ttu-id="c0c50-118">Wählen Sie in der Liste **Virtueller Zielcomputer** den Eintrag _woodgrove-VM1_ aus.</span><span class="sxs-lookup"><span data-stu-id="c0c50-118">In the **Target virtual machine** list, select _woodgrove-VM1_.</span></span>

1. <span data-ttu-id="c0c50-119">Wählen Sie in der Liste **Netzwerk-IP-Konfiguration** für die VM den IP-Adressenpool der VM aus.</span><span class="sxs-lookup"><span data-stu-id="c0c50-119">In the **Network IP configuration** list for the VM, select the VM's IP address pool.</span></span>

1. <span data-ttu-id="c0c50-120">Wiederholen Sie diese Schritte, um _woodgrove-VM2_ und _woodgrove-VM3_ zum Back-End-Pool hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-120">Repeat those steps to add _woodgrove-VM2_ and _woodgrove-VM3_ to the backend pool.</span></span>

    ![Screenshot, der das Blatt „Back-End-Pool hinzufügen“ mit allen drei ausgewählten VMs zeigt](../media/6-add-backend-pool.png)

1. <span data-ttu-id="c0c50-122">Klicken Sie auf **OK**, um das Blatt zu schließen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-122">Click **OK** to close the blade.</span></span>

<span data-ttu-id="c0c50-123">Warten Sie, bis die Konfiguration für den Lastenausgleich aktualisiert wurde, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0c50-123">Wait until the load balancer configuration has updated before proceeding with the exercise.</span></span>

## <a name="create-a-health-probe-for-the-load-balancer"></a><span data-ttu-id="c0c50-124">Erstellen eines Integritätstests für den Lastenausgleich</span><span class="sxs-lookup"><span data-stu-id="c0c50-124">Create a health probe for the load balancer</span></span>

<span data-ttu-id="c0c50-125">Fügen Sie als Nächstes einen Integritätstest für HTTP über Port 80 hinzu.</span><span class="sxs-lookup"><span data-stu-id="c0c50-125">Next, add a health probe for HTTP over port 80.</span></span>

1. <span data-ttu-id="c0c50-126">Klicken Sie auf dem Blatt **woodgrove-LB** unter **Einstellungen** auf **Integritätstests**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-126">On the **woodgrove-LB** blade, under **Settings**, click **Health probes**.</span></span> <span data-ttu-id="c0c50-127">Sie werden feststellen, dass dieser Bereich derzeit leer ist.</span><span class="sxs-lookup"><span data-stu-id="c0c50-127">Notice it's currently empty.</span></span>

1. <span data-ttu-id="c0c50-128">Klicken Sie auf **Hinzufügen**, um einen neuen Integritätstest hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-128">Click **Add** to add a new health probe.</span></span>

1. <span data-ttu-id="c0c50-129">Legen Sie auf dem Blatt **Integritätstest hinzufügen** folgende Konfiguration fest:</span><span class="sxs-lookup"><span data-stu-id="c0c50-129">On the **Add health probe** blade, set the following configuration:</span></span>
    - <span data-ttu-id="c0c50-130">**Name:** _woodgrove-HP_</span><span class="sxs-lookup"><span data-stu-id="c0c50-130">**Name:** _woodgrove-HP_</span></span>
    - <span data-ttu-id="c0c50-131">**Protokoll:** _HTTP_</span><span class="sxs-lookup"><span data-stu-id="c0c50-131">**Protocol:** _HTTP_</span></span>
    - <span data-ttu-id="c0c50-132">**Port:** _80_</span><span class="sxs-lookup"><span data-stu-id="c0c50-132">**Port:** _80_</span></span>
    - <span data-ttu-id="c0c50-133">**Pfad:** _/_</span><span class="sxs-lookup"><span data-stu-id="c0c50-133">**Path:** _/_</span></span>
    - <span data-ttu-id="c0c50-134">**Intervall:** _15_</span><span class="sxs-lookup"><span data-stu-id="c0c50-134">**Interval:** _15_</span></span>
    - <span data-ttu-id="c0c50-135">**Fehlerhafter Schwellenwert:** _2_</span><span class="sxs-lookup"><span data-stu-id="c0c50-135">**Unhealthy threshold:** _2_</span></span>

1. <span data-ttu-id="c0c50-136">Klicken Sie zum Speichern der Änderungen auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-136">Click **OK** to save the changes.</span></span>

<span data-ttu-id="c0c50-137">Warten Sie, bis die Konfiguration für den Lastenausgleich aktualisiert wurde, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0c50-137">Wait until the load balancer configuration has updated before proceeding with the exercise.</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="c0c50-138">Erstellen einer Lastenausgleichsregel</span><span class="sxs-lookup"><span data-stu-id="c0c50-138">Create a load balancer rule</span></span>

<span data-ttu-id="c0c50-139">Erstellen Sie abschließend eine Lastenausgleichsregel für HTTP über Port 80, mit der der Back-End-Pool dem Integritätstest zugeordnet wird.</span><span class="sxs-lookup"><span data-stu-id="c0c50-139">Finally, create a load-balancing rule for the HTTP over port 80, that associates the backend pool with the health probe.</span></span>

1. <span data-ttu-id="c0c50-140">Klicken Sie auf dem Blatt **woodgrove-LB** unter **Einstellungen** auf **Lastenausgleichsregeln**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-140">On the **woodgrove-LB** blade, under **Settings**, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="c0c50-141">Klicken Sie auf **Hinzufügen**, um eine neue Regel hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-141">Click **Add** to add a new rule.</span></span>

1. <span data-ttu-id="c0c50-142">Legen Sie auf dem Blatt **Lastenausgleichsregel hinzufügen** den **Namen** auf _woodgrove-HTTP-LBRule_ fest.</span><span class="sxs-lookup"><span data-stu-id="c0c50-142">On the **Add load balancing rule** blade, set the the **Name** to _woodgrove-HTTP-LBRule_.</span></span>

1. <span data-ttu-id="c0c50-143">Überprüfen Sie, ob die folgenden Informationen automatisch eingegeben wurden:</span><span class="sxs-lookup"><span data-stu-id="c0c50-143">Verify that the following information has been automatically entered:</span></span>
    - <span data-ttu-id="c0c50-144">IP-Version: **IPv4**</span><span class="sxs-lookup"><span data-stu-id="c0c50-144">IP Version: **IPv4**</span></span>
    - <span data-ttu-id="c0c50-145">Front-End-IP-Adresse: **LoadBalancerFrontEnd**</span><span class="sxs-lookup"><span data-stu-id="c0c50-145">Frontend IP address: **LoadBalancerFrontEnd**</span></span>
    - <span data-ttu-id="c0c50-146">Protokoll: **TCP**</span><span class="sxs-lookup"><span data-stu-id="c0c50-146">Protocol: **TCP**</span></span>
    - <span data-ttu-id="c0c50-147">Port: **80**</span><span class="sxs-lookup"><span data-stu-id="c0c50-147">Port: **80**</span></span>
    - <span data-ttu-id="c0c50-148">Back-End-Port: **80**</span><span class="sxs-lookup"><span data-stu-id="c0c50-148">Backend port: **80**</span></span>
    - <span data-ttu-id="c0c50-149">Back-End-Pool: **woodgrove-BEP**</span><span class="sxs-lookup"><span data-stu-id="c0c50-149">Backend pool: **woodgrove-BEP**</span></span>
    - <span data-ttu-id="c0c50-150">Integritätstest: **woodgrove-HP**</span><span class="sxs-lookup"><span data-stu-id="c0c50-150">Health probe: **woodgrove-HP**</span></span>
    - <span data-ttu-id="c0c50-151">Sitzungspersistenz: **Keine**</span><span class="sxs-lookup"><span data-stu-id="c0c50-151">Session persistence: **None**</span></span>
    - <span data-ttu-id="c0c50-152">Leerlauftimeout: **4 Minuten**</span><span class="sxs-lookup"><span data-stu-id="c0c50-152">Idle timeout: **4 minutes**</span></span>
    - <span data-ttu-id="c0c50-153">Floating IP: **Deaktiviert**</span><span class="sxs-lookup"><span data-stu-id="c0c50-153">Floating IP: **Disabled**</span></span>

1. <span data-ttu-id="c0c50-154">Klicken Sie zum Speichern der Regel auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-154">Click **OK** to save the rule.</span></span>

<span data-ttu-id="c0c50-155">Warten Sie, bis die Konfiguration für den Lastenausgleich aktualisiert wurde, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0c50-155">Wait until the load balancer configuration has updated before proceeding with the exercise.</span></span>

## <a name="test-the-load-balancer"></a><span data-ttu-id="c0c50-156">Testen des Lastenausgleichs</span><span class="sxs-lookup"><span data-stu-id="c0c50-156">Test the load balancer</span></span>

1. <span data-ttu-id="c0c50-157">Wechseln Sie zurück zur Seite **Übersicht** des Lastenausgleichs, und klicken Sie auf den Link **Öffentliche IP-Adresse**, um zur zugewiesenen IP-Adresse zu gelangen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-157">Switch back to the **Overview** page of the load balancer and click the **Public IP address** link on the page to get to the IP address assigned.</span></span> <span data-ttu-id="c0c50-158">Alternativ können Sie auf **Alle Ressourcen** klicken und in der Ressourcenliste **woodgrove-LB-ip** auswählen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-158">Alternatively, you can use **All resources** and then in the resource list, select **woodgrove-LB-ip**.</span></span>

1. <span data-ttu-id="c0c50-159">Wählen Sie auf dem Blatt **Übersicht** die **IP-Adresse** aus, und klicken Sie direkt daneben auf die Schaltfläche **Kopieren**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-159">On the **Overview** blade, select the **IP address**, and click the **Copy** button next to it.</span></span> <span data-ttu-id="c0c50-160">Dies ist die _öffentliche_ IP-Adresse des Lastenausgleichs.</span><span class="sxs-lookup"><span data-stu-id="c0c50-160">This is the _public_ IP address for the load balancer.</span></span>

    ![Screenshot, der die öffentliche IP-Adresse im Bereich „Übersicht“ anzeigt](../media/6-public-ip.png)

1. <span data-ttu-id="c0c50-162">Öffnen Sie eine neue Browserregisterkarte, und fügen Sie die IP-Adresse in die Adressleiste Ihres Browsers ein.</span><span class="sxs-lookup"><span data-stu-id="c0c50-162">Open a new browser tab and paste the IP address into the address bar of your browser.</span></span> <span data-ttu-id="c0c50-163">Notieren Sie sich den Namen des Servers, und lassen Sie die Registerkarte geöffnet.</span><span class="sxs-lookup"><span data-stu-id="c0c50-163">Note the name of the server and keep this tab open.</span></span>

1. <span data-ttu-id="c0c50-164">Klicken Sie im Azure-Portal im Menü auf der linken Seite auf **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-164">In the Azure portal, in the left menu, click **All resources**.</span></span> <span data-ttu-id="c0c50-165">Klicken Sie in der Ressourcenliste dann auf den Server, den Sie sich oben notiert haben.</span><span class="sxs-lookup"><span data-stu-id="c0c50-165">Then, in the resource list, click the server you noted above.</span></span>

1. <span data-ttu-id="c0c50-166">Klicken Sie auf dem Blatt **Übersicht** auf **Beenden** und dann auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c0c50-166">On the **Overview** blade, click **Stop**, and then click **Yes**.</span></span>

1. <span data-ttu-id="c0c50-167">Warten Sie, bis die VM beendet wurde, und wechseln Sie dann zu der Registerkarte, die Sie in Schritt 3 angezeigt haben.</span><span class="sxs-lookup"><span data-stu-id="c0c50-167">Wait until the VM has stopped, and then switch to the tab you viewed in step 3.</span></span> <span data-ttu-id="c0c50-168">Aktualisieren Sie die Seite.</span><span class="sxs-lookup"><span data-stu-id="c0c50-168">Refresh the page.</span></span>

1. <span data-ttu-id="c0c50-169">Der Lastenausgleich sendet Ihre HTTP-Anforderung an eine Ihrer anderen VMs.</span><span class="sxs-lookup"><span data-stu-id="c0c50-169">The load balancer will now send your HTTP request to one of your other VMs.</span></span>

<span data-ttu-id="c0c50-170">In dieser Übung haben Sie erfahren, wie Sie Back-End-VMs und den Lastenausgleich bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c0c50-170">In this exercise, you completed the deployment of your backend VMs and the load balancer.</span></span>
