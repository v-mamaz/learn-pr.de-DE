<span data-ttu-id="887f8-101">Nachdem wir nun über ein Konto verfügen, können wir uns beim **Azure-Portal** anmelden.</span><span class="sxs-lookup"><span data-stu-id="887f8-101">Now that we have an account, we can sign into the **Azure portal**.</span></span> <span data-ttu-id="887f8-102">Beim Portal handelt es sich um einen webbasierten Standort der zentralen Verwaltung mit allen Abonnements und Ressourcen, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="887f8-102">The portal is a web-based administration site that lets you interact with all of your subscriptions and resources you have created.</span></span> <span data-ttu-id="887f8-103">Über diese Webschnittstelle können Sie praktisch alle Aktionen mit Azure ausführen.</span><span class="sxs-lookup"><span data-stu-id="887f8-103">Almost everything you do with Azure can be done through this web interface.</span></span>

## <a name="azure-portal-layout"></a><span data-ttu-id="887f8-104">Layout des Azure-Portals</span><span class="sxs-lookup"><span data-stu-id="887f8-104">Azure portal layout</span></span>

<span data-ttu-id="887f8-105">Das Azure-Portal ist die zentrale grafische Benutzeroberfläche für die Steuerung von Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="887f8-105">The Azure portal is the primary graphical user interface (GUI) for controlling Microsoft Azure.</span></span> <span data-ttu-id="887f8-106">Sie können einen Großteil der Verwaltungsaktionen im Portal ausführen. Das Portal ist in der Regel auch der beste Ort zur Durchführung einzelner Aufgaben oder zum Anzeigen detaillierter Konfigurationsoptionen.</span><span class="sxs-lookup"><span data-stu-id="887f8-106">You can carry out the majority of management actions in the portal, and it is typically the best interface for carrying out single tasks or where you want to look at the configuration options in detail.</span></span>

![Das Azure-Portal](../media-draft/5-portal.png)

:::row:::

    :::column:::
    ![The resources and favorites](../media-draft/5-favorites.png)
    :::column-end:::

    :::column span="3":::
    **Resource Panel**
    
    In the left-hand sidebar of the portal is the resource pane, which lists the main resource types. Note that Azure has more resource types than just those shown. The resources listed are part of your _favorites_. 

    You can customize this with the specific resource types you tend to create or administer most often. 

    You can also collapse this pane; with the **<<** caret. This will minimize it to just icons which can be convenient if you are working with limited screen real-estate.
    :::column-end:::

:::row-end:::

<span data-ttu-id="887f8-108">Der restliche Teil der Portalansicht ist für die jeweiligen Elemente bestimmt, mit denen Sie arbeiten.</span><span class="sxs-lookup"><span data-stu-id="887f8-108">The remainder of the portal view is for the specific elements you are working with.</span></span> <span data-ttu-id="887f8-109">Das _Dashboard_ ist die Standardseite (Hauptseite).</span><span class="sxs-lookup"><span data-stu-id="887f8-109">The default (main) page is the _dashboard_.</span></span> <span data-ttu-id="887f8-110">Wir behandeln das Dashboard später. Aber soviel schon jetzt: Es stellt eine anpassbare Übersicht über Ihre Ressourcen dar.</span><span class="sxs-lookup"><span data-stu-id="887f8-110">We'll cover this a bit later, but this represents a customizable birds-eye-view of your resources.</span></span> <span data-ttu-id="887f8-111">Sie können es verwenden, um zu bestimmten Ressourcen zu wechseln, die Sie verwalten möchten, oder um mit dem Eintrag **Alle Ressourcen** im Ressourcenbereich nach Ressourcen zu suchen.</span><span class="sxs-lookup"><span data-stu-id="887f8-111">You can use it to jump into specific resources you want to manage, or search for resources with the **All resources** entry in the resource panel.</span></span> <span data-ttu-id="887f8-112">Beim Verwalten einer Ressource, wie etwa einem virtuellen Computer oder einer Web-App, arbeiten Sie mit einem _Blatt_, auf dem bestimmte Informationen über die Ressource angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="887f8-112">When you are managing a resource, such as a virtual machine or a web app, you will work with a _blade_ that presents specific information about the resource.</span></span>

## <a name="what-is-a-blade"></a><span data-ttu-id="887f8-113">Was ist ein Blatt?</span><span class="sxs-lookup"><span data-stu-id="887f8-113">What is a blade?</span></span>

<span data-ttu-id="887f8-114">Die Navigation im Azure-Portal erfolgt über Blätter.</span><span class="sxs-lookup"><span data-stu-id="887f8-114">The Azure portal uses a blades model for navigation.</span></span> <span data-ttu-id="887f8-115">Ein _Blatt_ ist ein einblendbarer Bereich, der die Benutzeroberfläche für eine einzelne Ebene in einer Navigationssequenz enthält.</span><span class="sxs-lookup"><span data-stu-id="887f8-115">A _blade_ is a slide-out panel containing the UI for a single level in a navigation sequence.</span></span> <span data-ttu-id="887f8-116">Beispielsweise wird jedes der Elemente dieser Sequenz durch ein Blatt repräsentiert: **Virtuelle Computer** > **Compute** > **Ubuntu Server**.</span><span class="sxs-lookup"><span data-stu-id="887f8-116">For example, each of these elements in this sequence would be represented by a blade: **Virtual machines** > **Compute** > **Ubuntu Server**.</span></span>

<span data-ttu-id="887f8-117">Jedes Blatt enthält Informationen und konfigurierbare Optionen.</span><span class="sxs-lookup"><span data-stu-id="887f8-117">Each blade contains some information and configurable options.</span></span> <span data-ttu-id="887f8-118">Einige dieser Optionen generieren ein weiteres Blatt, das rechts neben vorhandenen Blättern angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="887f8-118">Some of these options generate another blade, which reveals itself to the right of any existing blade.</span></span> <span data-ttu-id="887f8-119">Auch auf dem neuen Blatt erzeugen konfigurierbare Optionen ein weiteres Blatt usw.</span><span class="sxs-lookup"><span data-stu-id="887f8-119">On the new blade, any further configurable options will spawn another blade, and so on.</span></span> <span data-ttu-id="887f8-120">So ist möglicherweise bereits nach kurzer Zeit eine Vielzahl verschiedener Blätter geöffnet.</span><span class="sxs-lookup"><span data-stu-id="887f8-120">Pretty soon, you can end up with several blades open at the same time.</span></span> <span data-ttu-id="887f8-121">Sie können Blätter auch maximieren, sodass sie den gesamten Bildschirm ausfüllen.</span><span class="sxs-lookup"><span data-stu-id="887f8-121">You can maximize blades as well so that they fill the entire screen.</span></span>

<span data-ttu-id="887f8-122">Da neue Blätter immer rechts neben dem Besitzer hinzugefügt werden, können Sie mithilfe der Scrollleiste am unteren Fensterrand zurückgehen, um nachzuvollziehen, wie Sie zum jeweiligen Teil der Konfiguration gelangt sind.</span><span class="sxs-lookup"><span data-stu-id="887f8-122">Since new blades are always added to the right of the owner, you can use the scrollbar at the bottom of the window to go backwards to see how you got to this spot in the configuration.</span></span> <span data-ttu-id="887f8-123">Alternativ können Sie Blätter einzeln schließen, indem Sie auf die Schaltfläche `X` in der oberen Ecke des Blatts klicken.</span><span class="sxs-lookup"><span data-stu-id="887f8-123">Alternatively, you can close blades individually by clicking the `X` button in the top corner of the blade.</span></span> <span data-ttu-id="887f8-124">Wenn Sie Änderungen vorgenommen, aber noch nicht gespeichert haben, werden Sie von Azure darüber informiert, dass die Änderungen verloren gehen, wenn Sie den Vorgang fortsetzen.</span><span class="sxs-lookup"><span data-stu-id="887f8-124">If you have unsaved changes, Azure will prompt you to let you know that the changes will be lost if you continue.</span></span>

## <a name="configuring-settings-in-the-azure-portal"></a><span data-ttu-id="887f8-125">Konfigurieren von Einstellungen im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="887f8-125">Configuring settings in the Azure portal</span></span>

<span data-ttu-id="887f8-126">Das Azure-Portal zeigt eine Reihe von Konfigurationsoptionen an, die meisten davon in der Statusleiste im oberen rechten Bereich des Bildschirms.</span><span class="sxs-lookup"><span data-stu-id="887f8-126">The Azure portal displays several configuration options, mostly in the status bar at the top-right of the screen.</span></span>

### <a name="notifications"></a><span data-ttu-id="887f8-127">Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="887f8-127">Notifications</span></span>

<span data-ttu-id="887f8-128">Durch Klicken auf das Glockensymbol wird der **Benachrichtigungsbereich** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="887f8-128">Clicking the bell icon displays the **Notifications** pane.</span></span> <span data-ttu-id="887f8-129">In diesem Bereich werden die letzten ausgeführten Aktionen mit dem zugehörigen Status aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="887f8-129">This pane lists the last actions that have been carried out, along with their status.</span></span>

![Das Blatt „Benachrichtigungen“](../media-draft/5-notifications-blade.png)

### <a name="cloud-shell"></a><span data-ttu-id="887f8-131">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="887f8-131">Cloud Shell</span></span>

<span data-ttu-id="887f8-132">Wenn Sie auf das **Cloud Shell-Symbol** (>_) klicken, erstellen Sie eine neue Azure Cloud Shell-Sitzung.</span><span class="sxs-lookup"><span data-stu-id="887f8-132">If you click the **Cloud Shell** icon (>_), you will create a new Azure Cloud Shell session.</span></span> <span data-ttu-id="887f8-133">Azure Cloud Shell ist eine interaktive, über den Browser zugängliche Shell für die Verwaltung von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="887f8-133">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span> <span data-ttu-id="887f8-134">Es bietet Ihnen die Flexibilität, die Shell-Benutzeroberfläche auszuwählen, die sich am besten für Ihre Arbeitsweise eignet.</span><span class="sxs-lookup"><span data-stu-id="887f8-134">It provides the flexibility of choosing the shell experience that best suits the way you work.</span></span> <span data-ttu-id="887f8-135">Linux-Benutzer können Bash-Benutzeroberflächen verwenden, während Windows-Benutzer PowerShell nutzen können.</span><span class="sxs-lookup"><span data-stu-id="887f8-135">Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.</span></span> <span data-ttu-id="887f8-136">Mit diesem browserbasierten Terminal können Sie Ihre Azure-Ressourcen im aktuellen Abonnement über eine im Portal integrierte Befehlszeilenschnittstelle steuern und verwalten.</span><span class="sxs-lookup"><span data-stu-id="887f8-136">This browser-based terminal lets you control and administer all of your Azure resources in the current subscription through a command-line interface built right into the portal.</span></span>

![Cloud Shell](../media-draft/5-choose-shell.png)

### <a name="settings"></a><span data-ttu-id="887f8-138">Einstellungen</span><span class="sxs-lookup"><span data-stu-id="887f8-138">Settings</span></span>

<span data-ttu-id="887f8-139">Klicken Sie auf das **Zahnradsymbol**, um die Einstellungen des Azure-Portals zu ändern.</span><span class="sxs-lookup"><span data-stu-id="887f8-139">Click the **gear** icon to change the Azure portal settings.</span></span> <span data-ttu-id="887f8-140">Diese umfassen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="887f8-140">These settings include:</span></span>

- <span data-ttu-id="887f8-141">Uhrzeit der Abmeldung</span><span class="sxs-lookup"><span data-stu-id="887f8-141">Logout time</span></span>
- <span data-ttu-id="887f8-142">Farbschema</span><span class="sxs-lookup"><span data-stu-id="887f8-142">Color scheme</span></span>
- <span data-ttu-id="887f8-143">Designs mit hohem Kontrast</span><span class="sxs-lookup"><span data-stu-id="887f8-143">High contrast themes</span></span>
- <span data-ttu-id="887f8-144">Popupbenachrichtigungen (auf einem mobilen Gerät)</span><span class="sxs-lookup"><span data-stu-id="887f8-144">Toast notifications (to a mobile device)</span></span>
- <span data-ttu-id="887f8-145">Doppelklicken zum Ändern des Themas</span><span class="sxs-lookup"><span data-stu-id="887f8-145">Double-click to change the theme</span></span>
- <span data-ttu-id="887f8-146">Sprache</span><span class="sxs-lookup"><span data-stu-id="887f8-146">Language</span></span>
- <span data-ttu-id="887f8-147">Regionales Format</span><span class="sxs-lookup"><span data-stu-id="887f8-147">Regional format</span></span>

![Portaleinstellungen](../media-draft/5-settings-blade.png)

<span data-ttu-id="887f8-149">Wenn Sie die Einstellungen geändert haben, klicken Sie auf **Übernehmen**, um die Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="887f8-149">When you have changed settings, click **Apply** to accept your changes.</span></span>

### <a name="feedback-blade"></a><span data-ttu-id="887f8-150">Das Blatt „Feedback“</span><span class="sxs-lookup"><span data-stu-id="887f8-150">Feedback blade</span></span>

<span data-ttu-id="887f8-151">Klicken Sie auf das **Smiley-Symbol**, um das Blatt **Senden Sie uns Feedback** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="887f8-151">The **smiley face** icon opens the **Send us feedback** blade.</span></span> <span data-ttu-id="887f8-152">Hier können Sie Feedback zu Azure an Microsoft zu senden.</span><span class="sxs-lookup"><span data-stu-id="887f8-152">Here you can send feedback to Microsoft about Azure.</span></span> <span data-ttu-id="887f8-153">Sie können angeben, ob Microsoft per E-Mail auf Ihr Feedback antworten darf.</span><span class="sxs-lookup"><span data-stu-id="887f8-153">Note that you can specify whether Microsoft can respond to your feedback by email.</span></span>

![Feedback](../media-draft/5-feedback-blade.png)

### <a name="help-blade"></a><span data-ttu-id="887f8-155">Das Blatt „Hilfe“</span><span class="sxs-lookup"><span data-stu-id="887f8-155">Help blade</span></span>

<span data-ttu-id="887f8-156">Klicken Sie auf das **Fragezeichensymbol**, um das Blatt **Hilfe** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="887f8-156">Click the **question mark** icon to show the **Help** blade.</span></span> <span data-ttu-id="887f8-157">Hier stehen verschiedene Optionen zur Auswahl, darunter Folgende:</span><span class="sxs-lookup"><span data-stu-id="887f8-157">Here you choose from several options, including:</span></span>

- <span data-ttu-id="887f8-158">Neuigkeiten</span><span class="sxs-lookup"><span data-stu-id="887f8-158">What's new</span></span>
- <span data-ttu-id="887f8-159">Azure-Roadmap</span><span class="sxs-lookup"><span data-stu-id="887f8-159">Azure roadmap</span></span>
- <span data-ttu-id="887f8-160">Interaktive Tour starten</span><span class="sxs-lookup"><span data-stu-id="887f8-160">Launch guided tour</span></span>
- <span data-ttu-id="887f8-161">Tastenkombinationen</span><span class="sxs-lookup"><span data-stu-id="887f8-161">Keyboard shortcuts</span></span>
- <span data-ttu-id="887f8-162">Diagnose anzeigen</span><span class="sxs-lookup"><span data-stu-id="887f8-162">Show diagnostics</span></span>
- <span data-ttu-id="887f8-163">Datenschutz und Nutzungsbedingungen</span><span class="sxs-lookup"><span data-stu-id="887f8-163">Privacy + terms</span></span>

### <a name="directory-and-subscription"></a><span data-ttu-id="887f8-164">Verzeichnis und Abonnement</span><span class="sxs-lookup"><span data-stu-id="887f8-164">Directory and subscription</span></span>

<span data-ttu-id="887f8-165">Klicken Sie auf das Symbol **Book and Filter** (Buchen und Filtern), um das Blatt **Directory + subscription** (Verzeichnis und Abonnement) anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="887f8-165">Click the **Book and Filter** icon to show the **Directory + subscription** blade.</span></span>

<span data-ttu-id="887f8-166">In Azure können Sie mehrere Abonnements mit einem einzigen Verzeichnis verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="887f8-166">Azure allows you to have more than one subscription associated with one directory.</span></span> <span data-ttu-id="887f8-167">Auf dem Blatt **Verzeichnis und Abonnement** können Sie zwischen den Abonnements wechseln.</span><span class="sxs-lookup"><span data-stu-id="887f8-167">On the **Directory + subscription** blade, you can change between subscriptions.</span></span> <span data-ttu-id="887f8-168">Hier können Sie das Abonnement ändern oder zu einem anderen Verzeichnis wechseln.</span><span class="sxs-lookup"><span data-stu-id="887f8-168">Here, you can change your subscription or change to another directory.</span></span>

![Verzeichnis](../media-draft/5-directory-blade-1.png)

### <a name="profile-settings"></a><span data-ttu-id="887f8-170">Profileinstellungen</span><span class="sxs-lookup"><span data-stu-id="887f8-170">Profile settings</span></span>

<span data-ttu-id="887f8-171">Wenn Sie in der rechten oberen Ecke auf Ihren Namen klicken, können Sie Ihre Profileinstellungen ändern.</span><span class="sxs-lookup"><span data-stu-id="887f8-171">If you click on your name in the top right-hand corner, you can then change your profile settings.</span></span>
<span data-ttu-id="887f8-172">Diese umfassen:</span><span class="sxs-lookup"><span data-stu-id="887f8-172">Options include:</span></span>

- <span data-ttu-id="887f8-173">Von Azure abmelden</span><span class="sxs-lookup"><span data-stu-id="887f8-173">Sign out of Azure</span></span>
- <span data-ttu-id="887f8-174">Kennwort ändern</span><span class="sxs-lookup"><span data-stu-id="887f8-174">Change password</span></span>
- <span data-ttu-id="887f8-175">Kontaktinformationen ändern</span><span class="sxs-lookup"><span data-stu-id="887f8-175">Change contact information</span></span>
- <span data-ttu-id="887f8-176">Berechtigungen anzeigen</span><span class="sxs-lookup"><span data-stu-id="887f8-176">View permissions</span></span>
- <span data-ttu-id="887f8-177">Eine Idee an das Azure-Team senden</span><span class="sxs-lookup"><span data-stu-id="887f8-177">Submit an idea to the Azure team</span></span>
- <span data-ttu-id="887f8-178">Ihre Rechnung anzeigen</span><span class="sxs-lookup"><span data-stu-id="887f8-178">View your bill</span></span>
- <span data-ttu-id="887f8-179">Verzeichnis wechseln (zeigt wie im vorherigen Abschnitt das Blatt **Verzeichnis und Abonnement** an)</span><span class="sxs-lookup"><span data-stu-id="887f8-179">Switch directory (shows the **Directory + subscription** blade as in the previous section)</span></span>

![Profileinstellungen](../media-draft/5-portal-menu.png)

<span data-ttu-id="887f8-181">Wenn Sie jetzt auf **Meine Rechnung anzeigen** klicken, leitet Azure Sie zur Seite **Kostenverwaltung und Abrechnung – Rechnungen** weiter, auf der Sie analysieren können, wofür Azure-Kosten anfallen.</span><span class="sxs-lookup"><span data-stu-id="887f8-181">If you now click **View my bill**, Azure takes you to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.</span></span>

![Die Seite „Abrechnung“](../media-draft/5-portal-billing.png)

<span data-ttu-id="887f8-183">Azure ist ein sehr umfangreiches Produkt, und die Benutzeroberfläche des Azure-Portals spiegelt dies wider.</span><span class="sxs-lookup"><span data-stu-id="887f8-183">Azure is a large product, and the Azure portal user interface (UI) reflects this.</span></span> <span data-ttu-id="887f8-184">Dank dem Konzept der verschiebbaren Blätter können Sie in den verschiedenen Verwaltungsaufgaben mühelos vor und zurück navigieren.</span><span class="sxs-lookup"><span data-stu-id="887f8-184">The sliding blade approach allows you to navigate back and forth through the various administration tasks with ease.</span></span> <span data-ttu-id="887f8-185">Experimentieren Sie mit dieser Benutzeroberfläche, damit Sie ein wenig Übung bekommen.</span><span class="sxs-lookup"><span data-stu-id="887f8-185">Let's experiment a bit with this UI so you get some practice.</span></span>