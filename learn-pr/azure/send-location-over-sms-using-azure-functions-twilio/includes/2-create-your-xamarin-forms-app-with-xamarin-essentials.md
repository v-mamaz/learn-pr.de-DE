<span data-ttu-id="475b6-101">Die zu erstellende Anwendung ist eine plattformübergreifende mobile App, die mit einer Azure-Funktion kommuniziert, um Ihren Standort zu teilen.</span><span class="sxs-lookup"><span data-stu-id="475b6-101">The application you're building is a cross-platform mobile app that talks to an Azure function to share your location.</span></span> <span data-ttu-id="475b6-102">In dieser Einheit erstellen Sie mit Visual Studio die leere mobile App und installieren ein NuGet-Paket mit einer API zum Abrufen des Benutzerstandorts.</span><span class="sxs-lookup"><span data-stu-id="475b6-102">In this unit, you create the blank mobile app using Visual Studio and install a NuGet package that has an API for getting the user's location.</span></span>

## <a name="create-the-xamarinforms-project"></a><span data-ttu-id="475b6-103">Erstellen des Xamarin.Forms-Projekts</span><span class="sxs-lookup"><span data-stu-id="475b6-103">Create the Xamarin.Forms project</span></span>

1. <span data-ttu-id="475b6-104">Wählen Sie in Visual Studio *Datei > Neu > Projekt* aus.</span><span class="sxs-lookup"><span data-stu-id="475b6-104">From Visual Studio, select *File->New->Project...*.</span></span>

1. <span data-ttu-id="475b6-105">Wählen Sie in der Struktur links *Visual C# > Plattformübergreifend* aus, und klicken Sie dann im Arbeitsbereich in der Mitte auf *Mobile App (Xamarin.Forms)*.</span><span class="sxs-lookup"><span data-stu-id="475b6-105">From the tree on the left-hand side, select *Visual C#->Cross-Platform* and then select *Mobile App (Xamarin.Forms)* from the panel in the center.</span></span>

1. <span data-ttu-id="475b6-106">Geben Sie der Projektmappe den Namen „ImHere“.</span><span class="sxs-lookup"><span data-stu-id="475b6-106">Name the solution "ImHere".</span></span>

1. <span data-ttu-id="475b6-107">Wählen Sie einen geeigneten Speicherort für die Projektmappe aus.</span><span class="sxs-lookup"><span data-stu-id="475b6-107">Choose an appropriate location for the solution.</span></span>

1. <span data-ttu-id="475b6-108">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="475b6-108">Click **OK**.</span></span>

    ![Dialogfeld „Neue Projektmappe“](../media/2-new-solution-dialog.png)

1. <span data-ttu-id="475b6-110">Wählen Sie im Dialogfeld **Neue plattformübergreifende App** die Vorlage *Leere App* aus.</span><span class="sxs-lookup"><span data-stu-id="475b6-110">From the **New Cross Platform App** dialog, select the *Blank App* template.</span></span>

1. <span data-ttu-id="475b6-111">Für dieses Modul erstellen Sie eine UWP-App. Deaktivieren Sie deshalb iOS und Android, und lassen Sie UWP aktiviert.</span><span class="sxs-lookup"><span data-stu-id="475b6-111">For this module you will build a UWP app, so uncheck iOS and Android and leave UWP checked.</span></span>

1. <span data-ttu-id="475b6-112">Wählen Sie für *Codefreigabestrategie* die Option **.NET Standard** aus.</span><span class="sxs-lookup"><span data-stu-id="475b6-112">For the *Code Sharing Strategy*, select **.NET Standard**.</span></span>

1. <span data-ttu-id="475b6-113">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="475b6-113">Click **OK**.</span></span>

    ![Dialogfeld zum Konfigurieren der neuen Projektmappe](../media/2-configure-solution-dialog.png)

<span data-ttu-id="475b6-115">Visual Studio erstellt zwei Projekte für Sie: eine UWP-App namens `ImHere.UWP` und eine .NET Standard-Bibliothek `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="475b6-115">Visual Studio will create two projects for you - a UWP app called `ImHere.UWP` and a .NET Standard library, `ImHere`.</span></span> <span data-ttu-id="475b6-116">Xamarin.Forms-Apps umfassen zwei Bestandteile – mindestens ein plattformspezifisches App-Projekt und (mindestens) eine .NET Standard-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="475b6-116">Xamarin.Forms apps are made up of two parts - one or more platform-specific app projects and one (or more) .NET Standard libraries.</span></span> <span data-ttu-id="475b6-117">Die plattformspezifischen App-Projekte enthalten den plattformspezifischen Code, der zum Ausführen einer App auf der jeweiligen Plattform benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="475b6-117">The platform-specific app projects contain the platform-specific code needed to run an app on the relevant platform.</span></span> <span data-ttu-id="475b6-118">Diese Projekte starten anschließend eine Xamarin.Forms-App, die in einer plattformübergreifenden .NET Standard-Bibliothek definiert ist.</span><span class="sxs-lookup"><span data-stu-id="475b6-118">These projects then launch a Xamarin.Forms app that is defined in a cross-platform .NET Standard library.</span></span> <span data-ttu-id="475b6-119">Sie entwickeln Ihre App in plattformübergreifendem Code, und zur Laufzeit werden alle erstellten Benutzeroberflächen in die relevanten plattformspezifischen Benutzeroberflächenkomponenten übersetzt.</span><span class="sxs-lookup"><span data-stu-id="475b6-119">You build your app in cross-platform code and, at runtime, any user interfaces you create are translated into the relevant platform-specific UI components.</span></span>

## <a name="adding-xamarinessentials"></a><span data-ttu-id="475b6-120">Hinzufügen von „Xamarin.Essentials“</span><span class="sxs-lookup"><span data-stu-id="475b6-120">Adding Xamarin.Essentials</span></span>

<span data-ttu-id="475b6-121">Die UWP-, Android- und iOS-Plattformen bieten zahlreiche ähnliche Funktionen, die das Betriebssystem und die Hardware nutzen.</span><span class="sxs-lookup"><span data-stu-id="475b6-121">The UWP, Android, and iOS platforms provide numerous similar capabilities that take advantage of the operating system and hardware.</span></span> <span data-ttu-id="475b6-122">Trotz dieser Ähnlichkeiten sind die APIs sehr unterschiedlich.</span><span class="sxs-lookup"><span data-stu-id="475b6-122">Despite these similarities, the APIs are very different.</span></span> <span data-ttu-id="475b6-123">Zur Verwendung dieser APIs aus plattformübergreifendem Code muss plattformspezifischer Code in Ihren App-Projekten geschrieben werden, den Sie für Ihre .NET Standard-Bibliotheken verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="475b6-123">Using these APIs from cross-platform code requires writing platform-specific code in your app projects that you expose to your .NET Standard libraries.</span></span> <span data-ttu-id="475b6-124">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true) ist ein NuGet-Paket, das eine plattformübergreifende Abstraktion über eine Reihe dieser APIs bietet, sodass Sie keinen plattformspezifischen Code schreiben müssen.</span><span class="sxs-lookup"><span data-stu-id="475b6-124">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true) is a NuGet package that provides a cross-platform abstraction over a number of these APIs so that you don't need to write platform-specific code.</span></span> <span data-ttu-id="475b6-125">Dazu gehören auch die Geolocation-APIs, die Sie in Ihrer App verwenden werden, um den Standort des Benutzers zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="475b6-125">This includes the geolocation APIs that you will use in your app to get the user's location.</span></span>

1. <span data-ttu-id="475b6-126">Klicken Sie im Projektmappen-Explorer von Visual Studio mit der rechten Maustaste auf die Projektmappe `ImHere` (die oberste Projektmappe, nicht das .NET Standard-Projekt `ImHere`), und wählen Sie *NuGet-Pakete für Projektmappe verwalten...* aus.</span><span class="sxs-lookup"><span data-stu-id="475b6-126">Right-click on the `ImHere` solution (the top level solution, not the `ImHere` .NET Standard project) in the Visual Studio Solution Explorer and select *Manage NuGet Packages for Solution...*.</span></span>

1. <span data-ttu-id="475b6-127">Klicken Sie auf die Registerkarte **Durchsuchen**, und suchen Sie nach „Xamarin.Essentials“.</span><span class="sxs-lookup"><span data-stu-id="475b6-127">Select the **Browse** tab and search for "Xamarin.Essentials".</span></span> <span data-ttu-id="475b6-128">Dieses Paket ist zurzeit als Vorabversion-NuGet-Paket verfügbar. Aktivieren Sie deshalb das Kontrollkästchen neben *Include prelease* (Vorabversion einbeziehen).</span><span class="sxs-lookup"><span data-stu-id="475b6-128">This package is currently available as a prerelease NuGet package, so check the *include prelease* box.</span></span>

    > [!TIP]
    > <span data-ttu-id="475b6-129">Wenn Sie das Xamarin.Essentials-NuGet-Paket nicht sehen, überprüfen Sie nochmals, ob *Include prelease* aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="475b6-129">If you do not see the Xamarin.Essentials NuGet package, double check that *include prelease* is checked.</span></span> 

1. <span data-ttu-id="475b6-130">Wählen Sie das NuGet-Paket **Xamarin.Essentials** aus.</span><span class="sxs-lookup"><span data-stu-id="475b6-130">Select the **Xamarin.Essentials** NuGet package.</span></span>

1. <span data-ttu-id="475b6-131">Aktivieren Sie in der Projektliste auf der rechten Seite sämtliche Ihrer Projekte.</span><span class="sxs-lookup"><span data-stu-id="475b6-131">Check all your projects in the project list on the right-hand side.</span></span>

1. <span data-ttu-id="475b6-132">Klicken Sie auf die Schaltfläche **Installieren**, um das NuGet-Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="475b6-132">Click the **Install** button to install the NuGet package.</span></span> <span data-ttu-id="475b6-133">Sie müssen die Lizenz akzeptieren, um den Vorgang fortzusetzen.</span><span class="sxs-lookup"><span data-stu-id="475b6-133">You'll need to accept the license to continue.</span></span>

    ![Hinzufügen des NuGet-Pakets „Xamarin.Essentials“ zu allen Projekten in der Projektmappe](../media/2-add-essentials-nuget.png)

## <a name="building-and-running-the-app"></a><span data-ttu-id="475b6-135">Erstellen und Ausführen der App</span><span class="sxs-lookup"><span data-stu-id="475b6-135">Building and running the app</span></span>

1. <span data-ttu-id="475b6-136">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das `ImHere.UWP`-Projekt, und wählen Sie *Als Startprojekt festlegen* aus.</span><span class="sxs-lookup"><span data-stu-id="475b6-136">Right-click on the `ImHere.UWP` project in Solution Explorer and select *Set as StartUp project*.</span></span>

1. <span data-ttu-id="475b6-137">Legen Sie die Buildkonfiguration auf **Debuggen**, die Plattform auf **x86** und das Gerät für die Ausführung auf **Lokaler Computer** fest.</span><span class="sxs-lookup"><span data-stu-id="475b6-137">Set the build configuration to **Debug**, the platform to **x86**, and the device to run on to **Local Machine**.</span></span>

    ![Festlegen der x86-Debugkonfiguration zur Ausführung auf dem lokalen Gerät](../media/2-debug-configuration.png)

1. <span data-ttu-id="475b6-139">Beginnen Sie mit dem Debuggen der App.</span><span class="sxs-lookup"><span data-stu-id="475b6-139">Start debugging the app.</span></span>

    ![App bei der Ausführung](../media/2-debuging-app.png)

## <a name="summary"></a><span data-ttu-id="475b6-141">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="475b6-141">Summary</span></span>

<span data-ttu-id="475b6-142">In dieser Einheit haben Sie eine neue plattformübergreifende mobile Xamarin.Forms-App erstellt und das NuGet-Paket „Xamarin.Essentials“ hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="475b6-142">In this unit, you created a new Xamarin.Forms cross-platform mobile app and added the Xamarin.Essentials NuGet package.</span></span> <span data-ttu-id="475b6-143">Als Nächstes lernen Sie, wie Sie die Benutzeroberfläche und Logik der mobilen App entwickeln.</span><span class="sxs-lookup"><span data-stu-id="475b6-143">Next, you learn how to build up the mobile app UI and logic.</span></span>