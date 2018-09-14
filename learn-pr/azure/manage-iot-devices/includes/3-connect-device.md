<span data-ttu-id="02ebd-101">Das Erfassen von Wetterdaten ist eine wichtige Aufgabe, weil das Wetter vieles beeinflusst – von Verkehrsmustern bis hin zum Betrieb von Heizungs-, Lüftungs- und Klimasystemen im Einzelhandel.</span><span class="sxs-lookup"><span data-stu-id="02ebd-101">Capturing of weather data is an important task as weather can effect everything from traffic patterns to how HVAC systems in retail stores are operated.</span></span> <span data-ttu-id="02ebd-102">In dieser Übung verwenden Sie den Raspberry Pi-Onlinesimulator, um simulierte Wetterdaten zu erfassen und diese Daten über Azure IoT Hub zu speichern.</span><span class="sxs-lookup"><span data-stu-id="02ebd-102">In this exercise, you will be harnessing the online Raspberry Pi simulator to capture simulated weather data and capture said data via the Azure IoT Hub.</span></span>

<span data-ttu-id="02ebd-103">Wenngleich diese Übung in einer simulierten Umgebung durchgeführt wird, kann die auf dem simulierten Gerät ausgeführte Anwendung später auf ein echtes Gerät übertragen werden.</span><span class="sxs-lookup"><span data-stu-id="02ebd-103">While this exercise is being conducted in a simulated environment, the application running on the simulated device can be transferred to a real device in future.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="02ebd-104">Erstellen eines IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="02ebd-104">Create an IoT hub</span></span>

1. <span data-ttu-id="02ebd-105">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.</span><span class="sxs-lookup"><span data-stu-id="02ebd-105">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="02ebd-106">Wählen Sie **Ressource erstellen**\>**Internet der Dinge (IoT)**\>**IoT Hub** aus.</span><span class="sxs-lookup"><span data-stu-id="02ebd-106">Select **Create a resource** \> **Internet of Things** \> **IoT Hub**.</span></span>

![Screenshot der Navigation zu IoT Hub im Azure-Portal](../media-draft/fa40d1bc51bc4490f657e3c1a8371b5b.png)

1. <span data-ttu-id="02ebd-108">Geben Sie im Bereich **IoT Hub** die folgenden Informationen für Ihren IoT Hub ein:</span><span class="sxs-lookup"><span data-stu-id="02ebd-108">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

 - <span data-ttu-id="02ebd-109">**Abonnement**: Wählen Sie das Abonnement aus, das Sie zum Erstellen dieses IoT-Hubs verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="02ebd-109">**Subscription**: Choose the subscription that you want to use to create this IoT hub.</span></span>
 - <span data-ttu-id="02ebd-110">**Ressourcengruppe**: Erstellen Sie eine Ressourcengruppe zum Hosten des IoT Hubs, oder verwenden Sie eine vorhandene Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="02ebd-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="02ebd-111">Weitere Informationen finden Sie unter [Verwenden von Ressourcengruppen zum Verwalten von Azure-Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="02ebd-111">For more information, see [Use resource groups to manage your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>
 - <span data-ttu-id="02ebd-112">**Region**: Wählen Sie den nächstgelegenen Standort aus.</span><span class="sxs-lookup"><span data-stu-id="02ebd-112">**Region**: Select the closest location to you.</span></span>
 - <span data-ttu-id="02ebd-113">**Name**: Erstellen Sie einen Namen für Ihren IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="02ebd-113">**Name**: Create a name for your IoT hub.</span></span> <span data-ttu-id="02ebd-114">Wenn der eingegebene Name verfügbar ist, wird ein grünes Häkchen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="02ebd-114">If the name you enter is available, a green check mark appears.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02ebd-115">Der IoT Hub wird öffentlich als DNS-Endpunkt ermittelbar sein, sodass Sie beim Benennen die Verwendung von sensiblen Informationen vermeiden sollten.</span><span class="sxs-lookup"><span data-stu-id="02ebd-115">The IoT hub will be publicly discoverable as a DNS endpoint, so make sure to avoid any sensitive information while naming it.</span></span>

   ![Fenster mit IoT Hub-Grundeinstellungen](./../media-draft/dbb7319388673b8ee0e0b407536156c0.png)

1.  <span data-ttu-id="02ebd-117">Klicken Sie auf **Nächster Schritt: Größe festlegen und skalieren**, um die Erstellung Ihres IoT-Hubs fortzusetzen.</span><span class="sxs-lookup"><span data-stu-id="02ebd-117">Select **Next: Size and scale** to continue creating your IoT hub.</span></span>

1.  <span data-ttu-id="02ebd-118">Wählen Sie eine Option für **Tarif und Skalierung** aus.</span><span class="sxs-lookup"><span data-stu-id="02ebd-118">Choose your **Pricing and scale tier**.</span></span> <span data-ttu-id="02ebd-119">Legen Sie für diesen Artikel den Tarif **F1 – Free** fest, wenn er für Ihr Abonnement noch verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="02ebd-119">For this article, select the **F1 - Free** tier if it's still available on your subscription.</span></span> <span data-ttu-id="02ebd-120">Weitere Informationen hierzu finden Sie unter [Tarif und Skalierung](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="02ebd-120">For more information, see the [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

   ![Fenster für IoT Hub-Größe und -Skalierung](../media-draft/b506eb3293fa4aa9d4785ad498fc476c.png)

1.  <span data-ttu-id="02ebd-122">Klicken Sie auf **Überprüfen + erstellen**.</span><span class="sxs-lookup"><span data-stu-id="02ebd-122">Select **Review + create**.</span></span>

1.  <span data-ttu-id="02ebd-123">Überprüfen Sie die Informationen zum IoT-Hub, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="02ebd-123">Review your IoT hub information, then click **Create**.</span></span> <span data-ttu-id="02ebd-124">Die Erstellung des IoT Hubs kann mehrere Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="02ebd-124">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="02ebd-125">Sie können den Fortschritt im Bereich **Benachrichtigungen** überwachen.</span><span class="sxs-lookup"><span data-stu-id="02ebd-125">You can monitor the progress in the **Notifications** pane.</span></span>

<span data-ttu-id="02ebd-126">Nachdem Sie nun einen IoT Hub erstellt haben, können Sie nach den wichtigen Informationen suchen, die Sie zum Herstellen einer Verbindung für Geräte und Anwendungen mit Ihrem IoT Hub nutzen.</span><span class="sxs-lookup"><span data-stu-id="02ebd-126">Now that you have created an IoT hub, locate the important information that you use to connect devices and applications to your IoT hub.</span></span>

<span data-ttu-id="02ebd-127">Öffnen Sie in Ihrem IoT Hub-Navigationsmenü die Option  **	Richtlinien für gemeinsamen Zugriff**.</span><span class="sxs-lookup"><span data-stu-id="02ebd-127">In your IoT hub navigation menu, open **Shared access policies**.</span></span> <span data-ttu-id="02ebd-128">Wählen Sie die Richtlinie **iothubowner** aus, und kopieren Sie die **Verbindungszeichenfolge – Primärschlüssel** Ihres IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02ebd-128">Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub.</span></span> <span data-ttu-id="02ebd-129">Weitere Informationen finden Sie unter [Verwalten des Zugriffs auf IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).</span><span class="sxs-lookup"><span data-stu-id="02ebd-129">For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).</span></span>

> [!NOTE]
> <span data-ttu-id="02ebd-130">Die Verbindungszeichenfolge „iothubowner“ wird für dieses Tutorial nicht benötigt.</span><span class="sxs-lookup"><span data-stu-id="02ebd-130">You do not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="02ebd-131">Sie benötigen sie allerdings unter Umständen für einige Tutorials oder andere IoT-Szenarios, nachdem Sie diese Einrichtung abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="02ebd-131">However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.</span></span>

![Abrufen der IoT Hub-Verbindungszeichenfolge](../media-draft/a4b41e6ea46ccbef653c411a9829610c.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a><span data-ttu-id="02ebd-133">Registrieren eines Geräts beim IoT Hub für Ihr Gerät</span><span class="sxs-lookup"><span data-stu-id="02ebd-133">Register a device in the IoT hub for your device</span></span>
------------------------------------------------

1.  <span data-ttu-id="02ebd-134">Öffnen Sie in Ihrem IoT Hub-Navigationsmenü die Option **IoT-Geräte**, und klicken Sie auf **Hinzufügen**, um ein Gerät in Ihrem IoT Hub zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="02ebd-134">In your IoT hub navigation menu, open **IoT devices**, then click **Add** to register a device in your IoT hub.</span></span>

   ![Hinzufügen eines Geräts im Bereich „IoT-Geräte“ Ihres IoT Hubs](../media-draft/ee5f177abcf06b86dd007fce3b8448ad.png)

1.  <span data-ttu-id="02ebd-136">Geben Sie eine **Geräte-ID** für das neue Gerät ein.</span><span class="sxs-lookup"><span data-stu-id="02ebd-136">Enter a **Device ID** for the new device.</span></span> <span data-ttu-id="02ebd-137">Bei Geräte-IDs wird die Groß-/Kleinschreibung beachtet.</span><span class="sxs-lookup"><span data-stu-id="02ebd-137">Device IDs are case sensitive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02ebd-138">Diese Geräte-ID ist unter Umständen in den Protokollen sichtbar, die für den Kundensupport und die Problembehandlung erfasst werden. Stellen Sie also sicher, dass Sie beim Benennen keine sensiblen Informationen verwenden.</span><span class="sxs-lookup"><span data-stu-id="02ebd-138">The device ID may be visible in the logs collected for customer support and troubleshooting, so make sure to avoid any sensitive information while naming it.</span></span>

1.  <span data-ttu-id="02ebd-139">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="02ebd-139">Click **Save**.</span></span>

1.  <span data-ttu-id="02ebd-140">Öffnen Sie das Gerät nach der Erstellung in der Liste im Bereich **IoT-Geräte**.</span><span class="sxs-lookup"><span data-stu-id="02ebd-140">After the device is created, open the device from the list in the **IoT devices** pane.</span></span>

1.  <span data-ttu-id="02ebd-141">Kopieren Sie **Verbindungszeichenfolge – Primärschlüssel** zur späteren Verwendung.</span><span class="sxs-lookup"><span data-stu-id="02ebd-141">Copy the **Connection string---primary key** to use later.</span></span>

   ![Abrufen der Geräte-Verbindungszeichenfolge](../media-draft/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="02ebd-143">Ausführen einer Beispielanwendung im Pi-Websimulator</span><span class="sxs-lookup"><span data-stu-id="02ebd-143">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="02ebd-144">Stellen Sie im Codingbereich sicher, dass Sie mit der Standard-Beispielanwendung arbeiten.</span><span class="sxs-lookup"><span data-stu-id="02ebd-144">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="02ebd-145">Ersetzen Sie den Platzhalter in Zeile 15 durch die Verbindungszeichenfolge für das Azure IoT Hub-Gerät.</span><span class="sxs-lookup"><span data-stu-id="02ebd-145">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>

    ![Ersetzen der Verbindungszeichenfolge für das Gerät](../media-draft/92ea2c31d42f5b939fb5512e7220e957.png)

2.  <span data-ttu-id="02ebd-147">Klicken Sie auf **Ausführen**, oder geben Sie „npm start“ ein, um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="02ebd-147">Click **Run** or type npm start to run the application.</span></span>

<span data-ttu-id="02ebd-148">Sie sollten die folgende Ausgabe sehen, die die Sensordaten und Nachrichten zeigt, die an Ihren IoT Hub gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="02ebd-148">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub</span></span>

   ![Ausgabe: Von Raspberry Pi an Ihren IoT Hub gesendete Sensordaten](../media-draft/96b28d30e317b04347abb0d613738117.png)

<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
