<span data-ttu-id="695b5-101">Angenommen, Sie verfügen in Ihrem globalen Unternehmen über eine Anwendung für das Vertriebsteam.</span><span class="sxs-lookup"><span data-stu-id="695b5-101">Suppose you have an application for the sales team in your global company.</span></span> <span data-ttu-id="695b5-102">Jedes Teammitglied nutzt ein Mobiltelefon, auf dem die App installiert ist.</span><span class="sxs-lookup"><span data-stu-id="695b5-102">Each team member has a mobile phone where your app will be installed.</span></span> <span data-ttu-id="695b5-103">Mit einem in Azure gehosteten Webdienst wird die Geschäftslogik für Ihre Anwendung implementiert, und die Informationen werden in Azure SQL-Datenbank gespeichert.</span><span class="sxs-lookup"><span data-stu-id="695b5-103">A web service hosted in Azure implements the business logic for your application and stores information in Azure SQL Database.</span></span> <span data-ttu-id="695b5-104">Für jede geografische Region ist eine Instanz des Webdiensts vorhanden.</span><span class="sxs-lookup"><span data-stu-id="695b5-104">There is one instance of the web service for each geographical region.</span></span> <span data-ttu-id="695b5-105">Sie haben für das Senden von Nachrichten zwischen der mobilen App und dem Webdienst die folgenden Ziele ermittelt:</span><span class="sxs-lookup"><span data-stu-id="695b5-105">You have identified the following purposes for sending messages between the mobile app and the web service:</span></span>

- <span data-ttu-id="695b5-106">Nachrichten, die sich auf einzelne Verkäufe beziehen, müssen nur an die Instanz des Webdiensts in der Region des Benutzers gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="695b5-106">Messages that relate to individual sales must be sent only to the web service instance in the user's region.</span></span>
- <span data-ttu-id="695b5-107">Nachrichten, die sich auf die Vertriebsleistung beziehen, müssen an alle Instanzen des Webdiensts gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="695b5-107">Messages that relate to sales performance must be sent to all instances of the web service.</span></span>

<span data-ttu-id="695b5-108">Sie haben sich dafür entschieden, eine Service Bus-Warteschlange für den ersten Anwendungsfall und das Service Bus-Thema für den zweiten Anwendungsfall zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="695b5-108">You have decided to implement a Service Bus queue for the first use case and the Service Bus topic for the second use case.</span></span>

<span data-ttu-id="695b5-109">In dieser Übung erstellen Sie einen Service Bus-Namespace, der sowohl eine Warteschlange als auch ein Thema mit Abonnements enthält.</span><span class="sxs-lookup"><span data-stu-id="695b5-109">In this exercise, you will create a Service Bus namespace, which will contain both a queue and a topic with subscriptions.</span></span>

## <a name="create-a-service-bus-namespace"></a><span data-ttu-id="695b5-110">Erstellen eines Service Bus-Namespace</span><span class="sxs-lookup"><span data-stu-id="695b5-110">Create a Service Bus namespace</span></span>

<span data-ttu-id="695b5-111">In Azure Service Bus ist ein Namespace ein Container mit einem eindeutigen vollqualifizierten Domänennamen für Warteschlangen, Themen und Relays.</span><span class="sxs-lookup"><span data-stu-id="695b5-111">In Azure Service Bus, a namespace is a container, with a unique fully qualified domain name, for queues, topics, and relays.</span></span> <span data-ttu-id="695b5-112">Sie müssen zunächst den Namespace erstellen.</span><span class="sxs-lookup"><span data-stu-id="695b5-112">You must start by creating the namespace.</span></span>

<span data-ttu-id="695b5-113">Jeder Namespace verfügt außerdem über primäre und sekundäre Shared Access Signature-Verschlüsselungsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="695b5-113">Each namespace also has primary and secondary shared access signature encryption keys.</span></span> <span data-ttu-id="695b5-114">Eine sendende oder empfangende Komponente muss diese Schlüssel angeben, wenn sie eine Verbindung herstellt, um Zugriff auf die Objekte im Namespace zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="695b5-114">A sending or receiving component must provide these keys when it connects to gain access to the objects within the namespace.</span></span>

<span data-ttu-id="695b5-115">Führen Sie diese Schritte aus, um einen Service Bus-Namespace mit dem Azure-Portal zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="695b5-115">To create a Service Bus namespace by using the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="695b5-116">Navigieren Sie in einem Browser zum [Azure-Portal](https://portal.azure.com/), und melden Sie sich mit Ihren normalen Anmeldeinformationen für das Azure-Konto an.</span><span class="sxs-lookup"><span data-stu-id="695b5-116">In a browser, navigate to the [Azure portal](https://portal.azure.com/) and log in with your usual Azure account credentials.</span></span>

1. <span data-ttu-id="695b5-117">Klicken Sie im linken Navigationsbereich auf **Alle Dienste**.</span><span class="sxs-lookup"><span data-stu-id="695b5-117">In the navigation on the left, click **All services**.</span></span>

1. <span data-ttu-id="695b5-118">Scrollen Sie auf dem Blatt **Alle Dienste** nach unten zum Abschnitt **INTEGRATION**, und klicken Sie auf **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="695b5-118">In the **All Services** blade, scroll down to the **INTEGRATION** section, and then click **Service Bus**.</span></span>

    ![Erstellen eines Service Bus-Namespace](../media/3-create-namespace-1.png)

1. <span data-ttu-id="695b5-120">Klicken Sie oben links auf dem Blatt **Service Bus** auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="695b5-120">In the top left of the **Service Bus** blade, click **Add**.</span></span>

1. <span data-ttu-id="695b5-121">Geben Sie im Textfeld **Name** einen eindeutigen Namen für den Namespace ein.</span><span class="sxs-lookup"><span data-stu-id="695b5-121">In the **Name** text box, type a unique name for the namespace.</span></span> <span data-ttu-id="695b5-122">Beispiel: „salesteamapp“ + *Ihre Initialen* + *aktuelles Datum*.</span><span class="sxs-lookup"><span data-stu-id="695b5-122">For example "salesteamapp" + *your initials* + *current date*.</span></span>

1. <span data-ttu-id="695b5-123">Wählen Sie in der Dropdownliste **Tarif** die Option **Standard** aus.</span><span class="sxs-lookup"><span data-stu-id="695b5-123">In the **Pricing tier** drop-down list, select **Standard**.</span></span>

1. <span data-ttu-id="695b5-124">Wählen Sie in der Dropdownliste **Abonnement** Ihr Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="695b5-124">In the **Subscription** drop-down list, select your subscription.</span></span>

1. <span data-ttu-id="695b5-125">Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen** aus, und geben Sie dann **SalesTeamAppRG** ein.</span><span class="sxs-lookup"><span data-stu-id="695b5-125">Under **Resource group**, select **Create new**, and then type **SalesTeamAppRG**.</span></span>

1. <span data-ttu-id="695b5-126">Wählen Sie in der Dropdownliste **Standort** einen Standort in Ihrer Nähe aus, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="695b5-126">In the **Location** drop-down list, select a location near you, and then click **Create**.</span></span> <span data-ttu-id="695b5-127">Der neue Service Bus-Namespace wird in Azure erstellt.</span><span class="sxs-lookup"><span data-stu-id="695b5-127">Azure creates the new Service Bus namespace.</span></span>

    ![Erstellen eines Service Bus-Namespace](../media/3-create-namespace-2.png)

## <a name="create-a-service-bus-queue"></a><span data-ttu-id="695b5-129">Erstellen einer Service Bus-Warteschlange</span><span class="sxs-lookup"><span data-stu-id="695b5-129">Create a Service Bus queue</span></span>

<span data-ttu-id="695b5-130">Nachdem Sie nun über einen Namespace verfügen, können Sie eine Warteschlange für Nachrichten zu einzelnen Verkäufen erstellen.</span><span class="sxs-lookup"><span data-stu-id="695b5-130">Now that you have a namespace, you can create a queue for messages about individual sales.</span></span> <span data-ttu-id="695b5-131">Gehen Sie hierzu wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="695b5-131">To do this, follow these steps:</span></span>

1. <span data-ttu-id="695b5-132">Klicken Sie auf dem Blatt **Service Bus** auf **Aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="695b5-132">In the **Service Bus** blade, click **Refresh**.</span></span> <span data-ttu-id="695b5-133">Der Namespace, den Sie gerade erstellt haben, wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="695b5-133">The namespace you just created is displayed.</span></span>

1. <span data-ttu-id="695b5-134">Klicken Sie auf den gerade erstellten Namespace.</span><span class="sxs-lookup"><span data-stu-id="695b5-134">Click the namespace you just created.</span></span>

1. <span data-ttu-id="695b5-135">Klicken Sie oben links auf dem Namespaceblatt auf **+ Warteschlange**.</span><span class="sxs-lookup"><span data-stu-id="695b5-135">In the top left of the namespace blade, click **+ Queue**.</span></span>

1. <span data-ttu-id="695b5-136">Geben Sie auf dem Blatt **Warteschlange erstellen** im Textfeld **Name** den Namen **salesmessages** ein, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="695b5-136">In the **Create queue** blade, in the **Name** text box, type **salesmessages**, and then click **Create**.</span></span> <span data-ttu-id="695b5-137">Azure erstellt die Warteschlange in Ihrem Namespace.</span><span class="sxs-lookup"><span data-stu-id="695b5-137">Azure creates the queue in your namespace.</span></span>

    ![Erstellen einer Warteschlange](../media/3-create-queue.png)

## <a name="create-a-service-bus-topic-and-subscriptions"></a><span data-ttu-id="695b5-139">Erstellen eines Service Bus-Themas und von Abonnements</span><span class="sxs-lookup"><span data-stu-id="695b5-139">Create a Service Bus topic and subscriptions</span></span>

<span data-ttu-id="695b5-140">Außerdem möchten Sie ein Thema erstellen, das für Nachrichten zur Vertriebsleistung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="695b5-140">You also want to create a topic that will be used for messages that relate to sales performance.</span></span> <span data-ttu-id="695b5-141">Mehrere Instanzen des Geschäftslogik-Webdiensts abonnieren dieses Thema aus verschiedenen Ländern.</span><span class="sxs-lookup"><span data-stu-id="695b5-141">Multiple instances of the business logic web service will subscribe to this topic from different countries.</span></span> <span data-ttu-id="695b5-142">Jede Nachricht wird für mehrere Instanzen zugestellt.</span><span class="sxs-lookup"><span data-stu-id="695b5-142">Each message will be delivered to multiple instances.</span></span>

<span data-ttu-id="695b5-143">Führen Sie diese Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="695b5-143">Follow these steps:</span></span>

1. <span data-ttu-id="695b5-144">Klicken Sie auf dem Blatt **Service Bus-Namespace** auf **+ Thema**.</span><span class="sxs-lookup"><span data-stu-id="695b5-144">In the **Service Bus Namespace** blade, click **+ Topic**.</span></span>

1. <span data-ttu-id="695b5-145">Geben Sie auf dem Blatt **Thema erstellen** im Textfeld **Name** den Namen **salesperformancemessages** ein, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="695b5-145">In the **Create topic** blade, in the **Name** text box, type **salesperformancemessages**, and then click **Create**.</span></span> <span data-ttu-id="695b5-146">Azure erstellt das Thema in Ihrem Namespace.</span><span class="sxs-lookup"><span data-stu-id="695b5-146">Azure creates the topic in your namespace.</span></span>

    ![Erstellen eines Themas](../media/3-create-topic.png)

1. <span data-ttu-id="695b5-148">Klicken Sie nach dem Erstellen des Themas auf dem Blatt **Service Bus-Namespace** unter **Entitäten** auf **Themen**.</span><span class="sxs-lookup"><span data-stu-id="695b5-148">When the topic has been created, in the **Service Bus Namespace** blade, under **Entities**, click **Topics**.</span></span>

1. <span data-ttu-id="695b5-149">Klicken Sie in der Liste mit den Themen auf **salesperformancemessages** und dann auf **+ Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="695b5-149">In the list of topics, click **salesperformancemessages**, and then click **+ Subscription**.</span></span>

1. <span data-ttu-id="695b5-150">Geben Sie im Textfeld **Name** den Namen **Americas** ein, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="695b5-150">In the **Name** text box, type **Americas**, and then click **Create**.</span></span>

1. <span data-ttu-id="695b5-151">Klicken Sie auf **+ Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="695b5-151">Click **+ Subscription**.</span></span>

1. <span data-ttu-id="695b5-152">Geben Sie im Textfeld **Name** den Namen **EuropeAndAfrica** ein, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="695b5-152">In the **Name** text box, type **EuropeAndAfrica**, and then click **Create**.</span></span>

<span data-ttu-id="695b5-153">Sie haben die Infrastruktur erstellt, die erforderlich ist, um Service Bus zum Erhöhen der Resilienz Ihrer verteilten Anwendung für die Vertriebsmitarbeiter zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="695b5-153">You have built the infrastructure required to use Service Bus to increase the resilience of your sales force distributed application.</span></span> <span data-ttu-id="695b5-154">Sie haben eine Warteschlange für Nachrichten zu einzelnen Verkäufen und ein Thema für Nachrichten zur Vertriebsleistung erstellt.</span><span class="sxs-lookup"><span data-stu-id="695b5-154">You have created a queue for messages about individual sales and a topic for messages about sales performance.</span></span> <span data-ttu-id="695b5-155">Das Thema enthält mehrere Abonnements, da an das Thema gesendete Nachrichten für mehrere Empfängerwebdienste weltweit zugestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="695b5-155">The topic includes multiple subscriptions because messages sent to that topic can be delivered to multiple recipient web services around the world.</span></span>
