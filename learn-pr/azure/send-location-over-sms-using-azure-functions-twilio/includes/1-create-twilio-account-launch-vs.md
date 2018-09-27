> [!TIP]
> <span data-ttu-id="236f0-101">Der Benutzername und das Kennwort, die Sie für die Anmeldung bei der VM benötigen, müssen sich auf der Registerkarte **Ressourcen** befinden.</span><span class="sxs-lookup"><span data-stu-id="236f0-101">The username and password you need to sign in to the VM are located on the **Resources** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="236f0-102">Wenn Sie einen Mac verwenden, müssen Sie nach dem Starten der VM entweder das Blitzsymbol auf der Symbolleiste oder die Option **STRG+ALT+ENTF** von der Registerkarte **Ressourcen** neben den Anweisungen verwenden, um die VM zu entsperren.</span><span class="sxs-lookup"><span data-stu-id="236f0-102">If you are using a Mac, after launching the VM you may need to use either the lightning icon on the toolbar, or the **Ctrl+Alt+Delete** option from the **Resources** tab next to the instructions to unlock the VM.</span></span>


<span data-ttu-id="236f0-103">In diesem Modul erstellen Sie eine plattformübergreifende Xamarin.Forms-App mit serverlosem Back-End.</span><span class="sxs-lookup"><span data-stu-id="236f0-103">In this module, you'll create a cross-platform Xamarin.Forms app with a serverless back end.</span></span> <span data-ttu-id="236f0-104">Diese App ruft den Standort der Benutzer von deren Gerät ab und sendet ihn mit einer Liste von Telefonnummern an eine Azure-Funktion.</span><span class="sxs-lookup"><span data-stu-id="236f0-104">This app will get the user's location from their device and send it with a list of phone numbers to an Azure function.</span></span> <span data-ttu-id="236f0-105">Die Funktion verwendet dann eine Bindung an einen Drittanbieterdienst (Twilio), um Ihren Standort als SMS an alle angegebenen Telefonnummern zu senden.</span><span class="sxs-lookup"><span data-stu-id="236f0-105">The function will then use a binding to a third-party service (Twilio) to send your location as an SMS message to all the phone numbers provided.</span></span>

<span data-ttu-id="236f0-106">Dieser Vorgang umfasst die folgenden Schritte:</span><span class="sxs-lookup"><span data-stu-id="236f0-106">This process involves the following steps:</span></span>

1. <span data-ttu-id="236f0-107">Die App erfasst Ihren Standort mithilfe von Xamarin.Essentials als eine Abstraktion über gerätespezifische Standort-APIs.</span><span class="sxs-lookup"><span data-stu-id="236f0-107">The app captures your location using Xamarin.Essentials as an abstraction over device-specific location APIs.</span></span>

1. <span data-ttu-id="236f0-108">Der Standort und die Telefonnummern werden in eine JSON-Nutzlast verpackt und an eine Azure-Funktion gesendet.</span><span class="sxs-lookup"><span data-stu-id="236f0-108">The location and phone numbers are packaged up into a JSON payload and sent to an Azure function.</span></span>

1. <span data-ttu-id="236f0-109">Die Azure-Funktion decodiert die JSON-Nutzlast und erstellt SMS-Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="236f0-109">The Azure function decodes the JSON payload and creates SMS messages.</span></span>

1. <span data-ttu-id="236f0-110">Die SMS-Nachrichten werden über [Twilio](https://www.twilio.com/?azure-portal=true) gesendet.</span><span class="sxs-lookup"><span data-stu-id="236f0-110">The SMS messages are sent via [Twilio](https://www.twilio.com/?azure-portal=true).</span></span>

<span data-ttu-id="236f0-111">Die folgende Abbildung zeigt eine Übersicht dieses Prozesses.</span><span class="sxs-lookup"><span data-stu-id="236f0-111">The following illustration shows an overview of this process.</span></span>

![Abbildung, die die allgemeine Architektur des Prozesses des Teilens des Standorts mithilfe von Textnachrichten darstellt.](../media/1-architecture.png)

## <a name="create-a-twilio-account"></a><span data-ttu-id="236f0-113">Erstellen von Twilio-Konten</span><span class="sxs-lookup"><span data-stu-id="236f0-113">Create a Twilio account</span></span>

<span data-ttu-id="236f0-114">Um SMS-Nachrichten von einer Azure-Funktion senden können, benötigen Sie ein Twilio-Konto.</span><span class="sxs-lookup"><span data-stu-id="236f0-114">To be able to send SMS messages from an Azure function, you'll need a Twilio account.</span></span> <span data-ttu-id="236f0-115">Das kostenlose Konto ist für den Beginn völlig ausreichend.</span><span class="sxs-lookup"><span data-stu-id="236f0-115">The free account is more than enough to get started.</span></span>

1. <span data-ttu-id="236f0-116">Besuchen Sie [twilio.com](https://www.twilio.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="236f0-116">Head to [twilio.com](https://www.twilio.com?azure-portal=true).</span></span>

1. <span data-ttu-id="236f0-117">Klicken Sie auf die rote Schaltfläche **Sign up** (Registrieren) in der oberen rechten Ecke.</span><span class="sxs-lookup"><span data-stu-id="236f0-117">Click the red **Sign Up** button in the top-right corner.</span></span>

1. <span data-ttu-id="236f0-118">Geben Sie Ihre Informationen ein, und klicken Sie auf **Get Started** (Erste Schritte).</span><span class="sxs-lookup"><span data-stu-id="236f0-118">Fill in your details and click **Get Started**.</span></span>

1. <span data-ttu-id="236f0-119">Sie müssen Ihre Telefonnummer bestätigen.</span><span class="sxs-lookup"><span data-stu-id="236f0-119">You'll need to verify your phone number.</span></span> <span data-ttu-id="236f0-120">Mit kostenlosen Twilio-Konten können Sie Nachrichten nur an verifizierte Telefonnummern senden, um zu verhindern, dass diese für Spam-Mails verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="236f0-120">Twilio free accounts let you send messages only to verified phone numbers to stop them being used for spam.</span></span> <span data-ttu-id="236f0-121">Twilio sendet Ihnen einen Prüfcode, den Sie eingeben müssen, um Ihre Telefonnummer zu bestätigen.</span><span class="sxs-lookup"><span data-stu-id="236f0-121">Twilio will send you a verification code that you need to enter to verify your phone.</span></span>

1. <span data-ttu-id="236f0-122">Klicken Sie auf die Registerkarte **Produkte** > **Programmable SMS** (Programmierbare SMS), und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="236f0-122">Select the **Products** tab, and click **Programmable SMS**, then click **Continue**.</span></span>

1. <span data-ttu-id="236f0-123">Geben Sie einen Namen für Ihr erstes Projekt ein, z.B. „Ich bin hier“, und klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="236f0-123">Provide a name for your first project, such as "I'm here", then click **Continue**.</span></span>

1. <span data-ttu-id="236f0-124">Überspringen Sie den Schritt, um ein Teammitglied einzuladen.</span><span class="sxs-lookup"><span data-stu-id="236f0-124">Skip the step to invite a team mate.</span></span>

1. <span data-ttu-id="236f0-125">Erweitern Sie im Twilio-Nachrichtendashboard das Panel **Project Info** (Projektinformationen).</span><span class="sxs-lookup"><span data-stu-id="236f0-125">From the Twilio messaging dashboard, expand the **Project Info** panel.</span></span>

1. <span data-ttu-id="236f0-126">Notieren Sie sich Ihre **KONTO-SID** und Ihr **AUTHENTIFIZIERUNGSTOKEN**, da Sie diese Werte später benötigen.</span><span class="sxs-lookup"><span data-stu-id="236f0-126">Note your **ACCOUNT SID** and **AUTH TOKEN** because you will need these values later.</span></span>

    <span data-ttu-id="236f0-127">Wenn Sie ein Twilio-Konto erstellen, wird Ihnen eine Telefonnummer zugewiesen, über die Sie Nachrichten senden können.</span><span class="sxs-lookup"><span data-stu-id="236f0-127">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="236f0-128">Sie finden diese Telefonnummer im Twilio-Dashboard **Phone Numbers** (Telefonnummern).</span><span class="sxs-lookup"><span data-stu-id="236f0-128">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span>

1. <span data-ttu-id="236f0-129">Wählen Sie auf der Twilio-Website die Auslassungspunkte im unteren Bereich des links angezeigten Menüs aus.</span><span class="sxs-lookup"><span data-stu-id="236f0-129">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="236f0-130">Wählen Sie dann *SUPER NETWORK > Phone Numbers* (SUPERNETZWERK > Telefonnummern) aus.</span><span class="sxs-lookup"><span data-stu-id="236f0-130">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="236f0-131">Sie können dieses Dashboard mithilfe des Stecknadelsymbols an das Menü im linken Bereich anheften.</span><span class="sxs-lookup"><span data-stu-id="236f0-131">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="236f0-132">Ihre Twilio-Nummer finden Sie unter *Manage Numbers > Active Numbers* (Nummern verwalten > Aktive Nummern).</span><span class="sxs-lookup"><span data-stu-id="236f0-132">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span>

    ![Ermitteln Ihrer Twilio-Nummer](../media/7-twilio-find-number.png)

    > [!TIP]
    > <span data-ttu-id="236f0-134">Wenn Sie noch nicht über eine aktive Nummer verfügen, wählen Sie **Erste Schritte** auf der Seite „Aktive Nummern“ aus, um die Erstellung einer Zahl anzustoßen.</span><span class="sxs-lookup"><span data-stu-id="236f0-134">If you don't have an active number yet, select **Get Started** in the Active Numbers page to begin the process of creating a number.</span></span>

1. <span data-ttu-id="236f0-135">Notieren Sie sich Ihre aktive Telefonnummer.</span><span class="sxs-lookup"><span data-stu-id="236f0-135">Note your active phone number.</span></span> <span data-ttu-id="236f0-136">Sie wird später in diesem Modul verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="236f0-136">It will be used later in this module.</span></span>


> [!NOTE]
> <span data-ttu-id="236f0-137">Wenn Sie sich anmelden, wird Ihnen eine Twilio-Telefonnummer zum Senden von SMS-Nachrichten zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="236f0-137">When you sign up, you will be assigned a Twilio phone number that will be used to send SMS messages.</span></span> <span data-ttu-id="236f0-138">In einigen Ländern ist das Senden von Nachrichten über diese Nummern jedoch möglicherweise nicht möglich.</span><span class="sxs-lookup"><span data-stu-id="236f0-138">In some countries, these numbers may not be able to send SMS messages.</span></span> <span data-ttu-id="236f0-139">In der Twilio-Dokumentation ist aufgelistet, [in welchen Ländern Einschränkungen gelten](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true). Außerdem wird gezeigt, wie Sie SMS-Nachrichten mithilfe einer [gebührenpflichtigen Nummer oder einer alphanumerischen Absender-ID](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true) senden.</span><span class="sxs-lookup"><span data-stu-id="236f0-139">The Twilio documentation lists [which countries have restrictions](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), and shows ways to send SMS messages using an [international number or AlphaNumeric sender Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true).</span></span>

## <a name="launch-visual-studio"></a><span data-ttu-id="236f0-140">Starten von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="236f0-140">Launch Visual Studio</span></span>

<span data-ttu-id="236f0-141">Für dieses Modul entwickeln Sie die mobile App und die Azure Functions-App mit Visual Studio 2017, das über einen virtuellen Computer verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="236f0-141">For this module, you'll develop the mobile app and Azure Functions app using Visual Studio 2017, available via a virtual machine.</span></span> <span data-ttu-id="236f0-142">Obwohl Xamarin.Forms-Apps so erstellt werden können, dass sie unter iOS, Android und Universelle Windows-Plattform (UWP) verwendet werden können, konzentriert sich dieses Modul nur auf UWP und darauf, dass die App innerhalb des virtuellen Lab-Computers funktioniert.</span><span class="sxs-lookup"><span data-stu-id="236f0-142">Although Xamarin.Forms apps can be built to run on iOS, Android, and Universal Windows Platform (UWP), this module will just focus on UWP so that it works inside the lab virtual machine.</span></span>

<span data-ttu-id="236f0-143">Starten Sie Visual Studio 2017 über das Startmenü der VM oder über die Desktopverknüpfung.</span><span class="sxs-lookup"><span data-stu-id="236f0-143">Launch Visual Studio 2017 from the VM's Start Menu, or from the desktop shortcut.</span></span>

## <a name="summary"></a><span data-ttu-id="236f0-144">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="236f0-144">Summary</span></span>

<span data-ttu-id="236f0-145">In dieser Einheit haben Sie ein Twilio-Konto zum Senden von SMS-Nachrichten erstellt und Visual Studio gestartet.</span><span class="sxs-lookup"><span data-stu-id="236f0-145">In this unit, you created a Twilio account to use to send SMS messages and launched Visual Studio.</span></span> <span data-ttu-id="236f0-146">Als Nächstes erfahren Sie, wie Sie eine Xamarin.Forms-App erstellen und das NuGet-Paket „Xamarin.Essentials“ hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="236f0-146">Next, you learn how to create a Xamarin.Forms app and add the Xamarin.Essentials NuGet package.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="236f0-147">Notieren Sie sich die Werte für Ihre Twilio-**Konto-SID**, das Twilio-**AUTHENTIFIZIERUNGSTOKEN** und die **aktive Twilio-Telefonnummer**, die Sie in dieser Einheit gesammelt haben. Sie werden sie später noch einmal benötigen.</span><span class="sxs-lookup"><span data-stu-id="236f0-147">Keep note of the Twilio  **ACCOUNT SID** and **AUTH TOKEN** and **Active Phone Number** values that you gathered in this unit, because you'll need these values later.</span></span>
