<span data-ttu-id="62d92-101">Azure-Produkte weisen eine Hierarchie mit mehreren Ebenen auf.</span><span class="sxs-lookup"><span data-stu-id="62d92-101">Azure products have a deep hierarchy.</span></span> <span data-ttu-id="62d92-102">Nehmen Sie beispielsweise an, dass Sie einen virtuellen Linux-Computer erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="62d92-102">For example, suppose you need to create a Linux virtual machine.</span></span> <span data-ttu-id="62d92-103">Dafür müssen Sie möglicherweise durch diese Ebenen navigieren: **Startseite** > **Virtuelle Computer** > **Compute** > **Ubuntu Server**.</span><span class="sxs-lookup"><span data-stu-id="62d92-103">You might navigate through these levels: **Home** > **Virtual machines** > **Compute** > **Ubuntu Server**.</span></span> <span data-ttu-id="62d92-104">Das Azure-Portal optimiert die Benutzeroberfläche, um solche Navigationssequenzen intuitiv zu gestalten.</span><span class="sxs-lookup"><span data-stu-id="62d92-104">The Azure portal optimizes its UI to make this type of navigation sequence intuitive.</span></span> <span data-ttu-id="62d92-105">In dieser Übung untersuchen Sie die wichtigsten Elemente der Benutzeroberfläche, die dies ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="62d92-105">Here, you will survey the key UI elements that make this possible.</span></span> <span data-ttu-id="62d92-106">Sie navigieren durch Menüs und Untermenüs und verwenden Blätter, um Dienste zu suchen und zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="62d92-106">You will navigate through menus and submenus and use blades to find and configure services.</span></span>

## <a name="azure-portal-layout"></a><span data-ttu-id="62d92-107">Layout des Azure-Portals</span><span class="sxs-lookup"><span data-stu-id="62d92-107">Azure portal layout</span></span>

<span data-ttu-id="62d92-108">Das Azure-Portal ist die grafische Hauptbenutzeroberfläche für die Steuerung von Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="62d92-108">The Azure portal is the main graphical user interface (GUI) for controlling Microsoft Azure.</span></span> <span data-ttu-id="62d92-109">Sie können einen Großteil der Verwaltungsaktionen im Portal ausführen. Das Portal ist in der Regel auch der beste Ort zur Durchführung einzelner Aufgaben oder zum Anzeigen detaillierter Konfigurationsoptionen.</span><span class="sxs-lookup"><span data-stu-id="62d92-109">You can carry out the large majority of management actions on the portal, and the portal is typically the best interface for carrying out single tasks or where you want to look at the configuration options in detail.</span></span>

<span data-ttu-id="62d92-110">Im linken Bereich des Portals befindet sich der Ressourcenbereich, in dem die wichtigsten Ressourcentypen aufgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="62d92-110">In the left-hand pane of the portal is the resource pane, which lists the main resource types.</span></span> <span data-ttu-id="62d92-111">Beachten Sie, dass Azure über wesentlich mehr Ressourcentypen verfügt als in dieser Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="62d92-111">Note that Azure has far many more resource types than just those shown.</span></span>

## <a name="using-blades-in-the-azure-portal"></a><span data-ttu-id="62d92-112">Verwenden von Blättern im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="62d92-112">Using blades in the Azure portal</span></span>

<span data-ttu-id="62d92-113">Die Navigation im Azure-Portal erfolgt über Blätter.</span><span class="sxs-lookup"><span data-stu-id="62d92-113">The Azure portal uses a blades model for navigation.</span></span> <span data-ttu-id="62d92-114">Ein _Blatt_ ist ein einblendbarer Bereich, der die Benutzeroberfläche für eine einzelne Ebene in einer Navigationssequenz enthält.</span><span class="sxs-lookup"><span data-stu-id="62d92-114">A _blade_ is a slide-out panel containing the UI for a single level in a navigation sequence.</span></span> <span data-ttu-id="62d92-115">Beispielsweise wird jedes der Elemente dieser Sequenz durch ein Blatt repräsentiert: **Virtuelle Computer** > **Compute** > **Ubuntu Server**.</span><span class="sxs-lookup"><span data-stu-id="62d92-115">For example, each of these elements in this sequence would be represented by a blade: **Virtual machines** > **Compute** > **Ubuntu Server**.</span></span>

<span data-ttu-id="62d92-116">Jedes Blatt der Benutzeroberfläche enthält in der Regel eine Reihe von konfigurierbaren Optionen.</span><span class="sxs-lookup"><span data-stu-id="62d92-116">Each blade within the UI typically contains a number of configurable options.</span></span> <span data-ttu-id="62d92-117">Einige dieser Optionen generieren ein weiteres Blatt, das rechts neben vorhandenen Blättern angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="62d92-117">Some of these options generate another blade, which reveals itself to the right of any existing blade.</span></span> <span data-ttu-id="62d92-118">Auch auf dem neuen Blatt erzeugen konfigurierbare Optionen ein weiteres Blatt usw.</span><span class="sxs-lookup"><span data-stu-id="62d92-118">On the new blade, any further configurable options will spawn another blade, and so on.</span></span> <span data-ttu-id="62d92-119">So ist möglicherweise bereits nach kurzer Zeit eine Vielzahl verschiedener Blätter geöffnet.</span><span class="sxs-lookup"><span data-stu-id="62d92-119">Pretty soon, you can end up with several blades open at the same time.</span></span> <span data-ttu-id="62d92-120">Sie können Blätter auch maximieren, sodass sie den gesamten Bildschirm ausfüllen.</span><span class="sxs-lookup"><span data-stu-id="62d92-120">You can maximize blades as well so that they fill the entire screen.</span></span>

<span data-ttu-id="62d92-121">Wenn Sie versuchen, ein Blatt zu schließen, ohne Konfigurationsänderungen zu speichern, werden Sie in einer Meldung dazu aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="62d92-121">If you try to close a blade without saving any configuration changes that you have made, you will receive a prompt.</span></span>

## <a name="configuring-settings-in-the-azure-portal"></a><span data-ttu-id="62d92-122">Konfigurieren von Einstellungen im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="62d92-122">Configuring settings in the Azure portal</span></span>

<span data-ttu-id="62d92-123">Das Azure-Portal zeigt eine Reihe von Konfigurationsoptionen an, die meisten davon in der Statusleiste im oberen rechten Bereich des Bildschirms.</span><span class="sxs-lookup"><span data-stu-id="62d92-123">The Azure portal displays several configuration options, mostly in the status bar to the top-right of the screen.</span></span>

### <a name="notifications"></a><span data-ttu-id="62d92-124">Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="62d92-124">Notifications</span></span>

<span data-ttu-id="62d92-125">Durch Klicken auf das Glockensymbol wird der **Benachrichtigungsbereich** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="62d92-125">Clicking the bell icon displays the **Notifications** pane.</span></span> <span data-ttu-id="62d92-126">In diesem Bereich werden die letzten ausgeführten Aktionen mit dem zugehörigen Status aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="62d92-126">This pane lists the last actions that have been carried out, along with their status.</span></span>

![Das Blatt „Benachrichtigungen“](../media-draft/2-notifications-blade.PNG)

### <a name="cloud-shell"></a><span data-ttu-id="62d92-128">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="62d92-128">Cloud Shell</span></span>

<span data-ttu-id="62d92-129">Wenn Sie auf das **Cloud Shell-Symbol** (>_) klicken, erstellen Sie eine neue Azure Cloud Shell-Sitzung.</span><span class="sxs-lookup"><span data-stu-id="62d92-129">If you click the **Cloud Shell** icon (>_), you will create a new Azure Cloud Shell session.</span></span> <span data-ttu-id="62d92-130">Sie werden aufgefordert, in dieser Sitzung entweder Linux Bash oder PowerShell unter Linux zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="62d92-130">You are prompted to use either Linux Bash or PowerShell on Linux in that session.</span></span>

![Cloud Shell](../media-draft/2-choose-shell.PNG)

### <a name="settings"></a><span data-ttu-id="62d92-132">Einstellungen</span><span class="sxs-lookup"><span data-stu-id="62d92-132">Settings</span></span>

<span data-ttu-id="62d92-133">Klicken Sie auf das **Zahnradsymbol**, um die Einstellungen des Azure-Portals zu ändern.</span><span class="sxs-lookup"><span data-stu-id="62d92-133">Click the **gear** icon to change the Azure portal settings.</span></span> <span data-ttu-id="62d92-134">Diese umfassen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="62d92-134">These settings include:</span></span>

* <span data-ttu-id="62d92-135">Uhrzeit der Abmeldung</span><span class="sxs-lookup"><span data-stu-id="62d92-135">Logout time</span></span>
* <span data-ttu-id="62d92-136">Farbschema</span><span class="sxs-lookup"><span data-stu-id="62d92-136">Color scheme</span></span>
* <span data-ttu-id="62d92-137">Designs mit hohem Kontrast</span><span class="sxs-lookup"><span data-stu-id="62d92-137">High contrast themes</span></span>
* <span data-ttu-id="62d92-138">Popupbenachrichtigungen (auf einem mobilen Gerät)</span><span class="sxs-lookup"><span data-stu-id="62d92-138">Toast notifications (to a mobile device)</span></span>
* <span data-ttu-id="62d92-139">Doppelklicken zum Ändern des Themas</span><span class="sxs-lookup"><span data-stu-id="62d92-139">Double-click to change theme</span></span>
* <span data-ttu-id="62d92-140">Sprache</span><span class="sxs-lookup"><span data-stu-id="62d92-140">Language</span></span>
* <span data-ttu-id="62d92-141">Regionales Format</span><span class="sxs-lookup"><span data-stu-id="62d92-141">Regional format</span></span>

![Portaleinstellungen](../media-draft/2-settings-blade.PNG)

<span data-ttu-id="62d92-143">Wenn Sie die Einstellungen geändert haben, klicken Sie auf **Übernehmen**, um die Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="62d92-143">When you have changed settings, click **Apply** to accept your changes.</span></span>

### <a name="feedback-blade"></a><span data-ttu-id="62d92-144">Das Blatt „Feedback“</span><span class="sxs-lookup"><span data-stu-id="62d92-144">Feedback blade</span></span>

<span data-ttu-id="62d92-145">Klicken Sie auf das **Smiley-Symbol**, um das Blatt **Senden Sie uns Feedback** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="62d92-145">The **smiley face** icon opens the **Send us feedback** blade.</span></span> <span data-ttu-id="62d92-146">Hier können Sie Feedback zu Azure an Microsoft zu senden.</span><span class="sxs-lookup"><span data-stu-id="62d92-146">Here you can send feedback to Microsoft about Azure.</span></span> <span data-ttu-id="62d92-147">Sie können angeben, ob Microsoft per E-Mail auf Ihr Feedback antworten darf.</span><span class="sxs-lookup"><span data-stu-id="62d92-147">Note that you can specify whether Microsoft can respond to your feedback by email.</span></span>

![Feedback](../media-draft/2-feedback-blade.PNG)

### <a name="help-blade"></a><span data-ttu-id="62d92-149">Das Blatt „Hilfe“</span><span class="sxs-lookup"><span data-stu-id="62d92-149">Help blade</span></span>

<span data-ttu-id="62d92-150">Klicken Sie auf das **Fragezeichensymbol**, um das Blatt **Hilfe** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="62d92-150">Click the **question mark** icon to show the **Help** blade.</span></span> <span data-ttu-id="62d92-151">Hier können Sie aus einer Reihe von Themen wie z.B. den folgenden auswählen:</span><span class="sxs-lookup"><span data-stu-id="62d92-151">Here you choose from a number of topics, including:</span></span>

* <span data-ttu-id="62d92-152">Neuigkeiten</span><span class="sxs-lookup"><span data-stu-id="62d92-152">What's new</span></span>
* <span data-ttu-id="62d92-153">Azure-Roadmap</span><span class="sxs-lookup"><span data-stu-id="62d92-153">Azure roadmap</span></span>
* <span data-ttu-id="62d92-154">Interaktive Tour starten</span><span class="sxs-lookup"><span data-stu-id="62d92-154">Launch guided tour</span></span>
* <span data-ttu-id="62d92-155">Tastenkombinationen</span><span class="sxs-lookup"><span data-stu-id="62d92-155">Keyboard shortcuts</span></span>
* <span data-ttu-id="62d92-156">Diagnose anzeigen</span><span class="sxs-lookup"><span data-stu-id="62d92-156">Show diagnostics</span></span>
* <span data-ttu-id="62d92-157">Datenschutz und Nutzungsbedingungen</span><span class="sxs-lookup"><span data-stu-id="62d92-157">Privacy + terms</span></span>

### <a name="directory-and-subscription"></a><span data-ttu-id="62d92-158">Verzeichnis und Abonnement</span><span class="sxs-lookup"><span data-stu-id="62d92-158">Directory and subscription</span></span>

<span data-ttu-id="62d92-159">Klicken Sie auf das Symbol **Book and Filter** (Buchen und Filtern), um das Blatt **Directory + subscription** (Verzeichnis und Abonnement) anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="62d92-159">Click the **Book and Filter** icon to show the **Directory + subscription** blade.</span></span>

<span data-ttu-id="62d92-160">In Azure können Sie mehrere Abonnements mit einem einzigen Verzeichnis verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="62d92-160">Azure allows you to have more than one subscription associated with one directory.</span></span> <span data-ttu-id="62d92-161">Auf dem Blatt **Verzeichnis und Abonnement** können Sie zwischen den Abonnements wechseln.</span><span class="sxs-lookup"><span data-stu-id="62d92-161">On the **Directory + subscription** blade, you can change between subscriptions.</span></span> <span data-ttu-id="62d92-162">Hier können Sie das Abonnement ändern oder zu einem anderen Verzeichnis wechseln.</span><span class="sxs-lookup"><span data-stu-id="62d92-162">Here, you can change your subscription or change to another directory.</span></span>

![Verzeichnis](../media-draft/2-directory-blade-1.PNG)

### <a name="profile-settings"></a><span data-ttu-id="62d92-164">Profileinstellungen</span><span class="sxs-lookup"><span data-stu-id="62d92-164">Profile settings</span></span>

<span data-ttu-id="62d92-165">Wenn Sie in der rechten oberen Ecke auf Ihren Namen klicken, können Sie Ihre Profileinstellungen ändern.</span><span class="sxs-lookup"><span data-stu-id="62d92-165">If you click on your name in the top right-hand corner, you can then change your profile settings.</span></span>
<span data-ttu-id="62d92-166">Diese umfassen:</span><span class="sxs-lookup"><span data-stu-id="62d92-166">Options include:</span></span>

* <span data-ttu-id="62d92-167">Von Azure abmelden</span><span class="sxs-lookup"><span data-stu-id="62d92-167">Sign out of Azure</span></span>
* <span data-ttu-id="62d92-168">Kennwort ändern</span><span class="sxs-lookup"><span data-stu-id="62d92-168">Change password</span></span>
* <span data-ttu-id="62d92-169">Kontaktinformationen ändern</span><span class="sxs-lookup"><span data-stu-id="62d92-169">Change contact information</span></span>
* <span data-ttu-id="62d92-170">Berechtigungen anzeigen</span><span class="sxs-lookup"><span data-stu-id="62d92-170">View permissions</span></span>
* <span data-ttu-id="62d92-171">Eine Idee an das Azure-Team senden</span><span class="sxs-lookup"><span data-stu-id="62d92-171">Submit an idea to the Azure team</span></span>
* <span data-ttu-id="62d92-172">Ihre Rechnung anzeigen</span><span class="sxs-lookup"><span data-stu-id="62d92-172">View your bill</span></span>
* <span data-ttu-id="62d92-173">Verzeichnis wechseln (zeigt wie im vorherigen Abschnitt das Blatt **Verzeichnis und Abonnement** an)</span><span class="sxs-lookup"><span data-stu-id="62d92-173">Switch directory (shows the **Directory + subscription** blade as in the previous section)</span></span>

![Profileinstellungen](../media-draft/2-portal-menu.png)

<span data-ttu-id="62d92-175">Wenn Sie jetzt auf **Meine Rechnung anzeigen** klicken, leitet Azure Sie zur Seite **Kostenverwaltung und Abrechnung – Rechnungen** weiter, auf der Sie analysieren können, wofür Azure-Kosten anfallen.</span><span class="sxs-lookup"><span data-stu-id="62d92-175">If you now click **View my bill**, Azure takes you to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.</span></span>

![Die Seite „Abrechnung“](../media-draft/2-portal-billing.PNG)

## <a name="summary"></a><span data-ttu-id="62d92-177">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="62d92-177">Summary</span></span>

<span data-ttu-id="62d92-178">Azure ist ein sehr umfangreiches Produkt, und die Benutzeroberfläche des Azure-Portals spiegelt dies wider.</span><span class="sxs-lookup"><span data-stu-id="62d92-178">Azure is a large product, and the Azure portal UI reflects this.</span></span> <span data-ttu-id="62d92-179">Das Portal unterstützt Sie dabei, sich in dieser komplexen Struktur zurechtzufinden, indem es Blätter für die verschiedenen Ebenen der Hierarchie bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="62d92-179">The primary way that the portal helps you navigate this complexity is with blades to indicate hierarchy.</span></span> <span data-ttu-id="62d92-180">Dank der Blätter können Sie sich auf eine bestimmte Aufgabe konzentrieren, und sie zeigen außerdem eindeutig an, auf welchem Weg Sie zu dieser Aufgabe gelangt sind.</span><span class="sxs-lookup"><span data-stu-id="62d92-180">Blades let you focus on a specific task while clearly indicating the path you took to reach that point.</span></span>