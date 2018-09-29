<span data-ttu-id="c55fc-101">Das Erfassen von Wetterdaten ist eine wichtige Aufgabe, weil das Wetter vieles beeinflusst – von Verkehrsmustern bis hin zum Betrieb von Heizungs-, Lüftungs- und Klimasystemen (Heating, Ventilation, Air Conditioning, HVAC) im Einzelhandel.</span><span class="sxs-lookup"><span data-stu-id="c55fc-101">Capturing of weather data is an important task as weather can effect everything from traffic patterns to how heating, ventilation, and air conditioning (HVAC) systems in retail stores are operated.</span></span> <span data-ttu-id="c55fc-102">In dieser Übung interagieren Sie mit dem Raspberry Pi-Onlinesimulator, der in der vorherigen Einheit vorgestellt wurde, um simulierte Wetterdaten zu erfassen und über Azure IoT Hub zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c55fc-102">In this exercise, you will be interacting with the online Raspberry Pi simulator you learned about in the previous unit to capture simulated weather data and via the Azure IoT Hub.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="c55fc-103">Diese Übung wird zwar in einer simulierten Umgebung durchgeführt, die auf dem simulierten Gerät ausgeführte Anwendung kann jedoch später auf ein echtes Gerät übertragen werden.</span><span class="sxs-lookup"><span data-stu-id="c55fc-103">While this exercise is being conducted in a simulated environment, the application running on the simulated device can be transferred to a real device in the future.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c55fc-104">Erstellen einer IoT Hub-Instanz</span><span class="sxs-lookup"><span data-stu-id="c55fc-104">Create an IoT hub</span></span>
<span data-ttu-id="c55fc-105">Auf der Grundlage der Features und des Erweiterungsmodells von Azure IoT Hub können Geräte- und Back-End-Entwickler stabile Geräteverwaltungslösungen entwickeln.</span><span class="sxs-lookup"><span data-stu-id="c55fc-105">Azure IoT Hub provides the features and an extensibility model that enable device and back-end developers to build robust device management solutions.</span></span> <span data-ttu-id="c55fc-106">Das Spektrum der Geräte reicht von einfachen Sensoren und zweckgebundenen Microcontrollern bis hin zu leistungsfähigen Gateways zur Weiterleitung der Kommunikation für Gerätegruppen.</span><span class="sxs-lookup"><span data-stu-id="c55fc-106">Devices range from constrained sensors and single purpose microcontrollers, to powerful gateways that route communications for groups of devices.</span></span> <span data-ttu-id="c55fc-107">Die Anwendungsfälle und Anforderungen für IoT-Betreiber sind außerdem sehr branchenspezifisch.</span><span class="sxs-lookup"><span data-stu-id="c55fc-107">In addition, the use cases and requirements for IoT operators vary significantly across industries.</span></span> <span data-ttu-id="c55fc-108">Trotz dieser Vielfalt bietet die Geräteverwaltung mit Azure IoT Hub Funktionen, Muster und Codebibliotheken für unterschiedlichste Geräte und Endbenutzer.</span><span class="sxs-lookup"><span data-stu-id="c55fc-108">Despite this variation, device management with IoT Hub provides the capabilities, patterns, and code libraries to cater to a diverse set of devices and end users.</span></span>

<span data-ttu-id="c55fc-109">Um mit dem Sammeln von Daten aus dem Raspberry Pi-Simulator beginnen zu können, müssen Sie zunächst eine IoT Hub-Instanz erstellen.</span><span class="sxs-lookup"><span data-stu-id="c55fc-109">In order to start collecting the data from the Raspberry Pi simulator, you need to first create an IoT hub.</span></span>

1. <span data-ttu-id="c55fc-110">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="c55fc-110">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

2. <span data-ttu-id="c55fc-111">Klicken Sie links oben im Azure-Portal auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-111">Choose **Create a resource** in the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="c55fc-112">Klicken Sie auf **Internet der Dinge** und anschließend auf **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-112">Select **Internet of Things**, and then select **IoT Hub**.</span></span>

![Screenshot der Navigation zu IoT Hub im Azure-Portal](../media/fa40d1bc51bc4490f657e3c1a8371b5b.png)

4. <span data-ttu-id="c55fc-114">Geben Sie im Bereich **IoT Hub** die folgenden Informationen für Ihre IoT Hub-Instanz ein:</span><span class="sxs-lookup"><span data-stu-id="c55fc-114">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

   - <span data-ttu-id="c55fc-115">**Abonnement:** Verwenden Sie für dieses Beispiel das Standardabonnement.</span><span class="sxs-lookup"><span data-stu-id="c55fc-115">**Subscription**: Use the default subscription for this example.</span></span>
   - <span data-ttu-id="c55fc-116">**Ressourcengruppe:** Verwenden Sie die vorhandene Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="c55fc-116">**Resource group**: Use the existing resource group.</span></span> <span data-ttu-id="c55fc-117">Indem Sie alle verwandten Ressourcen in der gleichen Gruppe zusammenfassen, können Sie sie alle zusammen verwalten.</span><span class="sxs-lookup"><span data-stu-id="c55fc-117">By putting all related resources in the same group you can manage them all together.</span></span> <span data-ttu-id="c55fc-118">Wenn Sie also beispielsweise die Ressourcengruppe löschen, werden alle Ressourcen in dieser Gruppe gelöscht.</span><span class="sxs-lookup"><span data-stu-id="c55fc-118">For example, deleting the resource group deletes all resources contained in that group.</span></span>
   - <span data-ttu-id="c55fc-119">**Name:** Erstellen Sie einen eindeutigen Namen für Ihre IoT Hub-Instanz.</span><span class="sxs-lookup"><span data-stu-id="c55fc-119">**Name**: Create a unique name for your IoT hub.</span></span> <span data-ttu-id="c55fc-120">Ist der eingegebene Name verfügbar, wird ein grünes Häkchen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c55fc-120">If the name you enter is available, a green check mark appears.</span></span>
   - <span data-ttu-id="c55fc-121">**Region:** Wählen Sie in der folgenden Liste den nächstgelegenen Standort aus.</span><span class="sxs-lookup"><span data-stu-id="c55fc-121">**Region**: Select the closest location to you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    > [!IMPORTANT]
    > <span data-ttu-id="c55fc-122">Der IoT Hub wird öffentlich als DNS-Endpunkt ermittelbar sein, sodass Sie beim Benennen die Verwendung von sensiblen Informationen vermeiden sollten.</span><span class="sxs-lookup"><span data-stu-id="c55fc-122">The IoT hub will be publicly discoverable as a DNS endpoint, so make sure to avoid any sensitive information while naming it.</span></span>

    ![Fenster mit IoT Hub-Grundeinstellungen](./../media/dbb7319388673b8ee0e0b407536156c0.png)

1. <span data-ttu-id="c55fc-124">Klicken Sie auf **Nächster Schritt: Größe festlegen und skalieren**, um die Erstellung Ihres IoT-Hubs fortzusetzen.</span><span class="sxs-lookup"><span data-stu-id="c55fc-124">Select **Next: Size and scale** to continue creating your IoT hub.</span></span>
2. <span data-ttu-id="c55fc-125">Wählen Sie eine Option für **Tarif und Skalierung** aus.</span><span class="sxs-lookup"><span data-stu-id="c55fc-125">Choose your **Pricing and scale tier**.</span></span> <span data-ttu-id="c55fc-126">Verwenden Sie für dieses Beispiel den Tarif **F1 – Free**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-126">For this example, select the **F1 - Free** tier.</span></span>

    ![Fenster für IoT Hub-Größe und -Skalierung](../media/b506eb3293fa4aa9d4785ad498fc476c.png)

3. <span data-ttu-id="c55fc-128">Klicken Sie auf **Überprüfen + erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-128">Select **Review + create**.</span></span>

4. <span data-ttu-id="c55fc-129">Überprüfen Sie die Informationen zum IoT-Hub, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-129">Review your IoT hub information, then click **Create**.</span></span> <span data-ttu-id="c55fc-130">Die Erstellung des IoT Hubs kann mehrere Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="c55fc-130">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="c55fc-131">Sie können den Fortschritt im Bereich **Benachrichtigungen** überwachen.</span><span class="sxs-lookup"><span data-stu-id="c55fc-131">You can monitor the progress in the **Notifications** pane.</span></span>

<!--STOPPED HERE-->
<!--
Now that you have created an IoT hub, it's time to locate the important information that you use to connect devices and applications to your IoT hub. In your IoT hub navigation menu, open **Shared access policies**. Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub. For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> You do not need this iothubowner connection string for this set-up exercise. However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.

![Get your IoT hub connection string](../media/a4b41e6ea46ccbef653c411a9829610c.png)
-->

## <a name="register-a-device"></a><span data-ttu-id="c55fc-132">Registrieren eines Geräts</span><span class="sxs-lookup"><span data-stu-id="c55fc-132">Register a device</span></span>
<span data-ttu-id="c55fc-133">Ein Gerät muss bei Ihrer IoT Hub-Instanz registriert werden, um eine Verbindung herstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="c55fc-133">A device must be registered with your IoT hub before it can connect.</span></span>

1. <span data-ttu-id="c55fc-134">Öffnen Sie in Ihrem IoT Hub-Navigationsmenü die Option **IoT-Geräte**, und klicken Sie auf **Hinzufügen**, um ein Gerät bei Ihrer IoT Hub-Instanz zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="c55fc-134">In your IoT hub navigation menu, open **IoT devices**, then click **Add** to register a device in your IoT hub.</span></span>

   ![Hinzufügen eines Geräts im Bereich „IoT-Geräte“ Ihres IoT Hubs](../media/ee5f177abcf06b86dd007fce3b8448ad.png)

2. <span data-ttu-id="c55fc-136">Geben Sie eine **Geräte-ID** für das neue Gerät ein.</span><span class="sxs-lookup"><span data-stu-id="c55fc-136">Enter a **Device ID** for the new device.</span></span> <span data-ttu-id="c55fc-137">Bei Geräte-IDs wird die Groß-/Kleinschreibung beachtet.</span><span class="sxs-lookup"><span data-stu-id="c55fc-137">Device IDs are case sensitive.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c55fc-138">Diese Geräte-ID ist unter Umständen in den Protokollen sichtbar, die für den Kundensupport und die Problembehandlung erfasst werden. Stellen Sie also sicher, dass Sie beim Benennen keine sensiblen Informationen verwenden.</span><span class="sxs-lookup"><span data-stu-id="c55fc-138">The device ID may be visible in the logs collected for customer support and troubleshooting, so make sure to avoid any sensitive information while naming it.</span></span>

3. <span data-ttu-id="c55fc-139">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-139">Click **Save**.</span></span>
4. <span data-ttu-id="c55fc-140">Öffnen Sie das Gerät nach der Erstellung in der Liste im Bereich **IoT-Geräte**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-140">After the device is created, open the device from the list in the **IoT devices** pane.</span></span>
5. <span data-ttu-id="c55fc-141">Kopieren Sie **Verbindungszeichenfolge – Primärschlüssel** zur späteren Verwendung.</span><span class="sxs-lookup"><span data-stu-id="c55fc-141">Copy the **Connection string---primary key** to use later.</span></span>

   ![Abrufen der Geräte-Verbindungszeichenfolge](../media/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="send-simulated-telemetry"></a><span data-ttu-id="c55fc-143">Senden simulierter Telemetriedaten</span><span class="sxs-lookup"><span data-stu-id="c55fc-143">Send simulated telemetry</span></span>

1. <span data-ttu-id="c55fc-144">Öffnen Sie den [Azure IoT-Simulator für den Raspberry Pi](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="c55fc-144">Open the [Raspberry Pi Azure IoT Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true).</span></span>
1. <span data-ttu-id="c55fc-145">Ersetzen Sie den Platzhalter in Zeile 15 durch die soeben kopierte Verbindungszeichenfolge für das Azure IoT Hub-Gerät.</span><span class="sxs-lookup"><span data-stu-id="c55fc-145">Replace the placeholder in Line 15 with the Azure IoT hub device connection string you just copied.</span></span>
1. <span data-ttu-id="c55fc-146">Klicken Sie auf die Schaltfläche `Run`, oder geben Sie im Konsolenfenster `npm start` ein, um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="c55fc-146">Click the `Run` button or type `npm start` in the console window to run the application.</span></span>

    ![Ersetzen der Geräte-Verbindungszeichenfolge](../media/Line15.png)

1. <span data-ttu-id="c55fc-148">Die folgende Ausgabe sollte angezeigt werden, die die Sensordaten und Nachrichten zeigt, die an Ihren IoT Hub gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="c55fc-148">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

    ![Ausgabe: Von Raspberry Pi an Ihren IoT Hub gesendete Sensordaten](../media/96b28d30e317b04347abb0d613738117.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="c55fc-150">Lesen der Telemetriedaten aus Ihrem Hub</span><span class="sxs-lookup"><span data-stu-id="c55fc-150">Read the telemetry from your hub</span></span>
<span data-ttu-id="c55fc-151">Nun passiert Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c55fc-151">So what's happening?</span></span> <span data-ttu-id="c55fc-152">IoT Hub empfängt die vom simulierten Gerät gesendeten Gerät-zu-Cloud-Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="c55fc-152">IoT hub is receiving the device-to-cloud messages sent from the simulated device.</span></span> <span data-ttu-id="c55fc-153">Um das zu sehen, schauen wir uns kurz an, wie Azure IoT Hub die eingehenden Daten verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="c55fc-153">In order to see that, let's take a quick look at how Azure IoT Hub is processing the incoming data.</span></span> <span data-ttu-id="c55fc-154">Klicken Sie in Ihrer IoT Hub-Instanz unter **Überwachung** auf **Metriken**.</span><span class="sxs-lookup"><span data-stu-id="c55fc-154">In your IoT Hub, under **Monitoring**, select **Metrics**.</span></span> <span data-ttu-id="c55fc-155">Warten Sie ein paar Minuten, bis die Daten eintreffen.</span><span class="sxs-lookup"><span data-stu-id="c55fc-155">Give it a few minutes as you wait for the data to come into the picture.</span></span>

![IoT Hub-Metriken](../media/HubMetrics.png)


<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
