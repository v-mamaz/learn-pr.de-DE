<span data-ttu-id="48bcf-101">Im Folgenden installieren Sie Visual Studio auf Ihrem Windows- oder macOS-Entwicklungscomputer.</span><span class="sxs-lookup"><span data-stu-id="48bcf-101">Here, you'll install Visual Studio on either your Windows or your macOS development machine.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="48bcf-102">Schritte in dieser Übung</span><span class="sxs-lookup"><span data-stu-id="48bcf-102">Exercise steps</span></span>

<span data-ttu-id="48bcf-103">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="48bcf-103">::: zone pivot="windows"</span></span>

### <a name="windows"></a><span data-ttu-id="48bcf-104">Windows</span><span class="sxs-lookup"><span data-stu-id="48bcf-104">Windows</span></span>

1. <span data-ttu-id="48bcf-105">Laden Sie den Visual Studio-Installer von https://visualstudio.microsoft.com/downloads/ herunter.</span><span class="sxs-lookup"><span data-stu-id="48bcf-105">Download the Visual Studio installer from https://visualstudio.microsoft.com/downloads/.</span></span>

1. <span data-ttu-id="48bcf-106">Führen Sie das Installationsprogramm aus.</span><span class="sxs-lookup"><span data-stu-id="48bcf-106">Run the installer.</span></span>

1. <span data-ttu-id="48bcf-107">Wählen Sie auf der Registerkarte **Workloads** die Workload **Azure-Entwicklung** aus.</span><span class="sxs-lookup"><span data-stu-id="48bcf-107">On the **Workloads** tab, select the **Azure development** workload.</span></span>

    <span data-ttu-id="48bcf-108">Der folgende Screenshot stellt den Visual Studio-Installer mit der ausgewählten Workload dar, durch die die Azure-Entwicklung in Visual Studio ermöglicht wird.</span><span class="sxs-lookup"><span data-stu-id="48bcf-108">The following screenshot shows the Visual Studio Installer workload selected to allow Azure development within Visual Studio.</span></span>

    ![Screenshot des Visual Studio-Installers mit der hervorgehobenen Workload „Azure-Entwicklung“](../media/5-select-azure-workload.png)

1. <span data-ttu-id="48bcf-110">(Optional) Installieren Sie die Workload „ASP.NET und Webentwicklung“, damit Sie Webanwendungen für Azure erstellen können.</span><span class="sxs-lookup"><span data-stu-id="48bcf-110">(Optional) Install the ASP.NET and web development workload to be ready to create web applications for Azure.</span></span>

1. <span data-ttu-id="48bcf-111">Klicken Sie auf **Installieren**, und warten Sie, bis Visual Studio installiert ist.</span><span class="sxs-lookup"><span data-stu-id="48bcf-111">Click **Install**, and wait for Visual Studio to install.</span></span> <span data-ttu-id="48bcf-112">Für Systeme, auf denen Visual Studio bereits installiert ist, kann diese Schaltfläche beispielsweise **Ändern** heißen.</span><span class="sxs-lookup"><span data-stu-id="48bcf-112">For systems with Visual Studio already installed, this button may say **Modify**.</span></span>

1. <span data-ttu-id="48bcf-113">Öffnen Sie Visual Studio nach der Installation.</span><span class="sxs-lookup"><span data-stu-id="48bcf-113">When the installation is complete, open Visual Studio.</span></span>

1. <span data-ttu-id="48bcf-114">Navigieren Sie zum Menü „Ansicht“ in Visual Studio, und stellen Sie sicher, dass die Option **Cloud-Explorer** vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="48bcf-114">Go to the View menu in Visual Studio and make sure you have the **Cloud Explorer** option.</span></span>

    <span data-ttu-id="48bcf-115">Auf dem folgenden Screenshot wird die Menüoption „Cloud-Explorer“ dargestellt, die vorhanden ist, wenn die Workload „Azure-Entwicklung“ installiert ist.</span><span class="sxs-lookup"><span data-stu-id="48bcf-115">The following screenshot shows the Cloud Explorer menu option that will be present if you have the Azure development workload installed.</span></span>

    ![Screenshot des Visual Studio-Menüs „Ansicht“ mit der hervorgehobenen Menüoption „Cloud-Explorer“](../media/5-verify-cloud-explorer.png)

<span data-ttu-id="48bcf-117">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="48bcf-117">::: zone-end</span></span>

<span data-ttu-id="48bcf-118">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="48bcf-118">::: zone pivot="macos"</span></span>

### <a name="macos"></a><span data-ttu-id="48bcf-119">macOS</span><span class="sxs-lookup"><span data-stu-id="48bcf-119">macOS</span></span>

1. <span data-ttu-id="48bcf-120">Navigieren Sie zu https://visualstudio.microsoft.com/, und laden Sie den Installer für Visual Studio für Mac herunter.</span><span class="sxs-lookup"><span data-stu-id="48bcf-120">Go to https://visualstudio.microsoft.com/ and download the Visual Studio for Mac installer.</span></span>

1. <span data-ttu-id="48bcf-121">Klicken Sie auf die Datei „VisualStudioInstaller.dmg“, um den Installer einzubinden, und führen Sie diesen anschließend aus, indem Sie auf das Logo doppelklicken.</span><span class="sxs-lookup"><span data-stu-id="48bcf-121">Click the VisualStudioInstaller.dmg file to mount the installer, then run it by double-clicking the logo.</span></span>

1. <span data-ttu-id="48bcf-122">Stimmen Sie den Datenschutzbestimmungen und Lizenzbedingungen zu, wenn diese angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="48bcf-122">Acknowledge the Privacy and License terms when presented.</span></span>

1. <span data-ttu-id="48bcf-123">Wählen Sie im Installer die Komponenten aus, die installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="48bcf-123">The installer will ask which components you wish to install.</span></span> <span data-ttu-id="48bcf-124">Azure-Komponenten sind in Visual Studio für Mac bereits enthalten, es wird jedoch empfohlen, die Plattform **.NET Core** zu installieren, um Webinhalte für Azure entwickeln zu können.</span><span class="sxs-lookup"><span data-stu-id="48bcf-124">Azure components are already part of Visual Studio for Mac, but it is recommended to install the **.NET Core** platform to develop web experiences for Azure.</span></span>

    <span data-ttu-id="48bcf-125">Der folgende Screenshot zeigt die .NET Core-Plattform an, die zum Hinzufügen von Azure-Entwicklungsfunktionen zu Visual Studio für Mac erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="48bcf-125">The following screenshot shows the .NET Core platform required to add Azure development capabilities to Visual Studio for Mac.</span></span>

    ![Screenshot des Visual Studio für Mac-Installers mit der hervorgehoben Option für die Plattform „.NET Core“](../media/5-vsmac-install-net-core.png)

1. <span data-ttu-id="48bcf-127">Klicken Sie auf **Installieren und aktualisieren**, sobald Sie mit der Auswahl zufrieden sind, und warten Sie, bis die Installation abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="48bcf-127">Click **Install and Update** once you are happy with the selections, and wait for the installer to complete.</span></span>

1. <span data-ttu-id="48bcf-128">Wenn Sie dazu aufgefordert werden, die Berechtigungen zu erhöhen, verwenden Sie Ihre Administratoranmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="48bcf-128">If you are prompted to elevate the permissions needed, use your administrator credentials to do so.</span></span>

1. <span data-ttu-id="48bcf-129">Starten Sie Visual Studio für Mac nach der Installation.</span><span class="sxs-lookup"><span data-stu-id="48bcf-129">Once the installer is complete, start Visual Studio for Mac.</span></span>

<span data-ttu-id="48bcf-130">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="48bcf-130">::: zone-end</span></span>