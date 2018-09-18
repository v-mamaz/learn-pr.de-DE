<span data-ttu-id="2e2b2-101">Als Nächstes schauen wir uns an, wie Sie Dashboards mithilfe des Azure-Portals und durch direktes Bearbeiten der zugrunde liegenden JSON-Datei erstellen und ändern können.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-101">Next, let's look at how to create and modify dashboards using the Azure Portal, and by editing the underlying JSON file directly.</span></span>

## <a name="what-is-a-dashboard"></a><span data-ttu-id="2e2b2-102">Was ist ein Dashboard?</span><span class="sxs-lookup"><span data-stu-id="2e2b2-102">What is a dashboard?</span></span>

<span data-ttu-id="2e2b2-103">Ein _Dashboard_ ist eine anpassbare Sammlung von Benutzeroberflächenkacheln, die im Azure-Portal angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-103">A _dashboard_ is a customizable collection of UI tiles displayed in the Azure portal.</span></span> <span data-ttu-id="2e2b2-104">Sie können Kacheln hinzufügen, entfernen und anordnen, um genau die gewünschte Ansicht zu erstellen und sie dann als Dashboard zu speichern.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-104">You add, remove, and position tiles to create the exact view you want, and then save that view as a dashboard.</span></span> <span data-ttu-id="2e2b2-105">Es werden mehrere Dashboards unterstützt, und Sie können nach Bedarf zwischen ihnen wechseln.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-105">Multiple dashboards are supported, and you can switch between them as needed.</span></span> <span data-ttu-id="2e2b2-106">Sie können Ihre Dashboards auch für andere Teammitglieder freigeben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-106">You can even share your dashboards with other team members.</span></span>

<span data-ttu-id="2e2b2-107">Dashboards bieten Ihnen viel Flexibilität bei der Verwaltung von Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-107">Dashboards give you considerable flexibility regarding how you manage Azure.</span></span> <span data-ttu-id="2e2b2-108">Sie können z.B. Dashboards für bestimmte Rollen innerhalb der Organisation erstellen und dann die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) verwenden, um zu steuern, wer auf das jeweilige Dashboard zugreifen darf.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-108">For example, you can create dashboards for specific roles within the organization, and then use role-based access control (RBAC) to control who can access that dashboard.</span></span> <span data-ttu-id="2e2b2-109">So kann Ihr Datenbankadministrator ein Dashboard einrichten, das Ansichten des SQL-Datenbank-Diensts enthält, und Ihr Azure Active Directory-Administrator kann Ansichten der Benutzer und Gruppen in Azure AD erhalten.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-109">Hence, your database administrator would have a dashboard that contains views of the SQL database service, whereas your Azure Active Directory administrator would have views of the users and groups within Azure AD.</span></span> <span data-ttu-id="2e2b2-110">Sie können das Portal auch für Ihre Produktions- und Entwicklungsumgebung anpassen – dabei erstellen Sie ein spezielles Dashboard für jede Umgebung, die Sie verwalten.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-110">You can even customize the portal between your production and development environments within the portal - creating a specific dashboard for each environment you are managing.</span></span>

<span data-ttu-id="2e2b2-111">Dashboards werden als JSON-Dateien (JavaScript Object Notation) gespeichert.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-111">Dashboards are stored as JavaScript Object Notation (JSON) files.</span></span> <span data-ttu-id="2e2b2-112">Das bedeutet, dass sie auf andere Computer hoch- und heruntergeladen oder mit Mitgliedern des Azure Active Directory gemeinsam genutzt werden können.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-112">This means they can be uploaded and downloaded to other computers, or shared with members of the Azure directory.</span></span> <span data-ttu-id="2e2b2-113">Azure speichert Dashboards in Ressourcengruppen genauso wie virtuelle Computer oder Speicherkonten, die Sie im Portal verwalten können.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-113">Azure stores dashboards within resource groups, just like virtual machines or storage accounts that you can manage within the portal.</span></span>

> [!TIP]
> <span data-ttu-id="2e2b2-114">Da Dashboards JSON-Dateien sind, können Sie sie auch [programmgesteuert anpassen](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-create-programmatically) und zu faszinierenden Verwaltungstools machen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-114">Because dashboards are JSON files, you can also [customize them programmatically](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-create-programmatically), making them compelling administrative tools.</span></span> <span data-ttu-id="2e2b2-115">Darüber hinaus können einige Kacheltypen abfragebasiert sein und bei Änderung der Quelldaten automatisch aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-115">Also, some tile types can be query-based, so they update automatically when the source data changes.</span></span>

## <a name="explore-the-default-dashboard"></a><span data-ttu-id="2e2b2-116">Untersuchen des Standarddashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-116">Explore the default dashboard</span></span>

<span data-ttu-id="2e2b2-117">Das Standarddashboard wird als „Dashboard“ bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-117">The default dashboard is named "Dashboard".</span></span> <span data-ttu-id="2e2b2-118">Wenn Sie sich beim Portal anmelden, wird Ihnen dieses Dashboard mit fünf Webparts angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-118">When you log into the portal, you are presented with this dashboard containing five web parts.</span></span>

![Standardwebparts](../media-draft/8-dashboard-default-webparts.png)

<span data-ttu-id="2e2b2-120">Dies sind die Standardwebparts:</span><span class="sxs-lookup"><span data-stu-id="2e2b2-120">These default web parts are</span></span>

1. <span data-ttu-id="2e2b2-121">Alle Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-121">All resources</span></span>

1. <span data-ttu-id="2e2b2-122">Erste Schritte mit Azure</span><span class="sxs-lookup"><span data-stu-id="2e2b2-122">Azure Getting Started</span></span>

1. <span data-ttu-id="2e2b2-123">Schnellstarts + Tutorials</span><span class="sxs-lookup"><span data-stu-id="2e2b2-123">Quickstarts + tutorials</span></span>

1. <span data-ttu-id="2e2b2-124">Marketplace</span><span class="sxs-lookup"><span data-stu-id="2e2b2-124">Marketplace</span></span>

1. <span data-ttu-id="2e2b2-125">Service Health</span><span class="sxs-lookup"><span data-stu-id="2e2b2-125">Service Health</span></span>

## <a name="creating-and-managing-dashboards"></a><span data-ttu-id="2e2b2-126">Erstellen und Verwalten von Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-126">Creating and managing dashboards</span></span>

<span data-ttu-id="2e2b2-127">Oberhalb des Dashboards befinden sich die Steuerelemente, mit denen Sie ein Dashboard erstellen, hochladen, herunterladen, bearbeiten und freigeben können.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-127">Along the top of the dashboard are the controls that enable you to create, upload, download, edit, and share a dashboard.</span></span> <span data-ttu-id="2e2b2-128">Sie können ein Dashboard auch in den Vollbildmodus schalten oder es klonen oder löschen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-128">You can also switch a dashboard to full screen, clone it, or delete it.</span></span>

![Anpassen von Dashboardsteuerelementen](../media-draft/8-customise-dashboard-controls.png)

- [<span data-ttu-id="2e2b2-130">Auswählen eines Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-130">Select dashboard</span></span>](#select-dashboard)
- [<span data-ttu-id="2e2b2-131">Erstellen eines neuen Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-131">Create a new dashboard</span></span>](#create-new)
- [<span data-ttu-id="2e2b2-132">Hochladen und Herunterladen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-132">Upload and Download</span></span>](#upload-download)
- [<span data-ttu-id="2e2b2-133">Bearbeiten</span><span class="sxs-lookup"><span data-stu-id="2e2b2-133">Edit</span></span>](#edit-dashboard)
- [<span data-ttu-id="2e2b2-134">Freigeben</span><span class="sxs-lookup"><span data-stu-id="2e2b2-134">Share</span></span>](#share-dashboard)
- [<span data-ttu-id="2e2b2-135">Vollbild</span><span class="sxs-lookup"><span data-stu-id="2e2b2-135">Full screen</span></span>](#full-screen)
- [<span data-ttu-id="2e2b2-136">Klonen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-136">Clone</span></span>](#clone-dashboard)
- [<span data-ttu-id="2e2b2-137">Löschen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-137">Delete</span></span>](#delete-dashboard)

<a name="select-dashboard"></a>

## <a name="select-dashboard"></a><span data-ttu-id="2e2b2-138">Auswählen eines Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-138">Select dashboard</span></span>

<span data-ttu-id="2e2b2-139">Ganz links in der Symbolleiste befindet sich das Dropdownsteuerelement **Dashboard auswählen**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-139">To the far left of the toolbar is the **Select Dashboard** drop-down control.</span></span> <span data-ttu-id="2e2b2-140">Wenn Sie auf dieses Steuerelement klicken, können Sie aus Dashboards auswählen, die Sie bereits für Ihr Konto definiert haben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-140">Clicking this control enables you to select from dashboards that you have already defined for your account.</span></span> <span data-ttu-id="2e2b2-141">Mit diesem Steuerelement können Sie ganz einfach mehrere Dashboards für verschiedene Zwecke definieren und dann zwischen den Dashboards wechseln, je nachdem, welche Aufgabe Sie gerade erledigen möchten.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-141">This control makes it simple for you to define multiple dashboards for different purposes and then switch from one to another and back again, depending on what you are trying to do at the time.</span></span>

<span data-ttu-id="2e2b2-142">Beachten Sie, dass alle von Ihnen erstellten Dashboards zunächst privat sind, also nur Sie diese anzeigen können.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-142">Note that any dashboards that you create will initially be private; that is, only you can see them.</span></span> <span data-ttu-id="2e2b2-143">Um ein Dashboard weiteren Personen in Ihrem Unternehmen zur Verfügung zu stellen, müssen Sie es freigeben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-143">To make a dashboard available across your enterprise, you need to share it.</span></span> <span data-ttu-id="2e2b2-144">Wir gehen in Kürze auf diese Option ein.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-144">We'll look at that option shortly.</span></span>

<a name="create-new"></a>

## <a name="create-a-new-dashboard"></a><span data-ttu-id="2e2b2-145">Erstellen eines neuen Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-145">Create a new dashboard</span></span>

<span data-ttu-id="2e2b2-146">Um ein neues Dashboard zu erstellen, klicken Sie einfach auf **Neues Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-146">To create a new dashboard, click **New dashboard**.</span></span> <span data-ttu-id="2e2b2-147">Der Dashboardarbeitsbereich wird ohne Kacheln angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-147">The dashboard workspace appears, with no tiles present.</span></span> <span data-ttu-id="2e2b2-148">Sie können dann wie gewünscht Kacheln hinzufügen, entfernen und anpassen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-148">You can then add, remove and adjust tiles however you like.</span></span> <span data-ttu-id="2e2b2-149">Wenn Sie mit der Anpassung des Dashboards fertig sind, klicken Sie auf **Anpassung abgeschlossen**, um die Änderungen zu speichern und zum Dashboard zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-149">When you are finished customizing the dashboard, click **Done customizing** to save and switch to that dashboard.</span></span>

<a name="upload-download"></a>

## <a name="upload-and-download"></a><span data-ttu-id="2e2b2-150">Hochladen und Herunterladen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-150">Upload and Download</span></span>

<span data-ttu-id="2e2b2-151">Mit den Schaltflächen **Hochladen** und **Herunterladen** können Sie Ihr aktuelles Dashboard als JSON-Datei herunterladen, es anpassen und dann verteilen und hochladen. Auch eine andere Person kann diese Datei wieder in das Azure-Portal hochladen und dadurch ihr eigenes aktuelles Dashboard ersetzen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-151">The **Upload** and **Download** buttons enable you to download your current dashboard as a JSON file, customize it, and then distribute it and upload it or have someone else upload that file back to the Azure portal, thereby replacing their current dashboard.</span></span>

<span data-ttu-id="2e2b2-152">Wenn Sie auf **Herunterladen** klicken, wird das aktuelle Dashboard in Ihren standardmäßigen Ordner für Downloads heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-152">If you click **Download**, the current dashboard downloads into your default Downloads folder.</span></span> <span data-ttu-id="2e2b2-153">Wenn Sie die heruntergeladene Datei öffnen, wird der JSON-Code angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-153">Opening the downloaded file then shows the JSON code.</span></span>

![JSON-Code des Dashboards](../media-draft/8-dashboard-json-code.png)

<span data-ttu-id="2e2b2-155">Sie können diesen Code manuell bearbeiten, indem Sie z.B. Kachelgrößen ändern und den Code dann per Klick auf die Schaltfläche **Hochladen** wieder in Azure hochladen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-155">You can then edit that code manually (for example, by changing tile sizes) and then upload it back to Azure by clicking the **Upload** button.</span></span>

<a name="edit-dashboard"></a>

### <a name="edit-a-dashboard"></a><span data-ttu-id="2e2b2-156">Bearbeiten eines Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-156">Edit a dashboard</span></span>

<span data-ttu-id="2e2b2-157">Sie können zwar ein Dashboard bearbeiten, indem Sie die JSON-Datei herunterladen, Werte in der Datei ändern und die Datei wieder in Azure hochladen. Allerdings ist diese Vorgehensweise für den Entwurf einer Benutzeroberfläche nicht intuitiv.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-157">Although you can edit a dashboard by downloading the JSON file, changing values in the file, and uploading the file back to Azure, that approach isn't intuitive for designing a user interface.</span></span> <span data-ttu-id="2e2b2-158">Um die grafische Benutzeroberfläche zum Konfigurieren Ihres aktuellen Dashboards zu verwenden, können Sie auf verschiedene Weise in den Bearbeitungsmodus wechseln:</span><span class="sxs-lookup"><span data-stu-id="2e2b2-158">To use the GUI to configure your current dashboard you can enter edit mode in several ways:</span></span>

1. <span data-ttu-id="2e2b2-159">Klicken Sie auf die Schaltfläche **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-159">Click the **Edit** button</span></span>
1. <span data-ttu-id="2e2b2-160">Klicken Sie mit der rechten Maustaste auf das Dashboard, und klicken Sie auf **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-160">Right-click on the dashboard and click **Edit**.</span></span> 
1. <span data-ttu-id="2e2b2-161">Bewegen Sie den Mauszeiger auf dem Dashboard auf eine Kachel, sodass ein `...`-Menü mit Bearbeitungsoptionen in der oberen rechten Ecke angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-161">Hover over a tile on the dashboard - a `...` menu will appear on the top/right corner with edit options.</span></span>

<span data-ttu-id="2e2b2-162">Das Dashboard wechselt in den Bearbeitungsmodus.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-162">The dashboard switches to edit mode.</span></span>

![Dashboard bearbeiten](../media-draft/8-edit-dashboard.png)

<span data-ttu-id="2e2b2-164">Auf der linken Seite wird der Kachelkatalog mit einer Reihe möglicher Kacheln angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-164">On the left-hand side appears the Tile Gallery, with several possible tiles.</span></span> <span data-ttu-id="2e2b2-165">Sie können den Kachelkatalog nach Kategorie und Ressourcentyp filtern:</span><span class="sxs-lookup"><span data-stu-id="2e2b2-165">You can filter the Tile Gallery by category and resource type:</span></span>

![Kachelkatalog](../media-draft/8-tile-gallery.png)

<span data-ttu-id="2e2b2-167">Um Kacheln hinzuzufügen, wählen Sie einfach aus der Liste links eine Kachel aus und ziehen sie in den Arbeitsbereich.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-167">Adding tiles is as easy as selecting the tile from the list on the left and then dragging it to the work area.</span></span> <span data-ttu-id="2e2b2-168">Sie können jede Kachel verschieben, ihre Größe oder die darin angezeigten Daten ändern.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-168">You can then move each tile about, resize it, or change the data that it displays.</span></span>

> [!TIP]
> <span data-ttu-id="2e2b2-169">Ein interessantes Feature, das viele Benutzer nicht kennen, ist die Möglichkeit, dass Sie Elemente von untergeordneten Blättern auf Ihrem Dashboard platzieren können.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-169">One cool feature a lot of people are unaware of is that you can take elements on child blades and put them on your dashboard.</span></span> <span data-ttu-id="2e2b2-170">Bewegen Sie einfach den Mauszeiger auf das Element, und platzieren Sie mit der „An Dashboard anheften“-Option des `...`-Kachelbearbeitungsmenüs schnell eine Kachel aus einem Dienst auf dem Dashboard.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-170">Just hover over the item and look for the `...` tile edit menu - this will have a "Pin to Dashboard" option which lets you quickly grab a tile from a service and put it onto the dashboard.</span></span>

<span data-ttu-id="2e2b2-171">Der Arbeitsbereich ist im Bearbeitungsmodus in Quadrate unterteilt.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-171">The work area in edit mode is divided into squares.</span></span> <span data-ttu-id="2e2b2-172">Jede Kachel muss mindestens ein Quadrat belegen, wobei Kacheln an den nächstgelegenen Trennlinien ausgerichtet werden.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-172">Each tile must occupy at least one square, and tiles will snap to the nearest largest set of tile dividers.</span></span> <span data-ttu-id="2e2b2-173">Überlappenden Kacheln werden beiseite verschoben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-173">Any overlapping tiles are moved out of the way.</span></span> <span data-ttu-id="2e2b2-174">Wenn Sie eine Kachel verkleinern, werden die umgebenden Kacheln wieder in die Nähe geschoben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-174">When you make a tile smaller, the surrounding tiles will move back up against it.</span></span>

#### <a name="change-tile-sizes"></a><span data-ttu-id="2e2b2-175">Ändern der Kachelgrößen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-175">Change tile sizes</span></span>

<span data-ttu-id="2e2b2-176">Einige Kacheln verfügen über eine festgelegte Größe, die Sie nur programmgesteuert bearbeiten können.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-176">Some tiles have a set size, and you can edit their size only programmatically.</span></span> <span data-ttu-id="2e2b2-177">Sie können jedoch Kacheln mit einer grauen Ecke rechts unten bearbeiten, indem Sie die Eckmarkierung mit der Maus ziehen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-177">However, you can edit tiles with a gray bottom right-hand corner by dragging the corner indicator.</span></span>

![Kachel mit veränderbarer Größe](../media-draft/8-resizable-tile.png)

<span data-ttu-id="2e2b2-179">Alternativ dazu können Sie auch mit der rechten Maustaste auf das Kontextmenü klicken und die gewünschte Größe angeben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-179">Alternatively, right-click the context menu and specify the size you want.</span></span>

![Kachelgröße](../media-draft/8-tile-size.png)

<span data-ttu-id="2e2b2-181">Um ein Dashboard zu erstellen, ziehen Sie Kacheln aus dem Kachelkatalog in den Arbeitsbereich und ordnen sie an.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-181">To create your dashboard, pull tiles from the Tile Gallery onto the workspace and then rearrange them.</span></span>

#### <a name="change-tile-settings"></a><span data-ttu-id="2e2b2-182">Ändern der Kacheleinstellungen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-182">Change tile settings</span></span>

<span data-ttu-id="2e2b2-183">Einige Kacheln weisen Einstellungen auf, die sich bearbeiten lassen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-183">Some tiles have editable settings.</span></span> <span data-ttu-id="2e2b2-184">Wenn Sie z.B. die Kachel „Uhr“ in den Arbeitsbereich ziehen, wird die Kachel **Uhr bearbeiten** geöffnet.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-184">For example, with the clock tile, when you drag it onto the workspace, it opens the **Edit clock** tile.</span></span> <span data-ttu-id="2e2b2-185">Dort können Sie die Zeitzone sowie die Anzeige im 12- oder 24-Stunden-Format festlegen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-185">You can then set the time zone, which it displays, and also set whether it displays in 12- or 24-hour format.</span></span>

![Bearbeiten der Uhr](../media-draft/8-edit-clock.png)

<span data-ttu-id="2e2b2-187">In multinationalen oder transkontinentalen Unternehmen können Sie Uhren hinzufügen, die jeweils unterschiedliche Zeitzonen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-187">For multi-national or transcontinental companies, you can add clocks, each in a different time zone.</span></span>

#### <a name="accepting-your-edits"></a><span data-ttu-id="2e2b2-188">Übernehmen der Änderungen</span><span class="sxs-lookup"><span data-stu-id="2e2b2-188">Accepting your edits</span></span>

<span data-ttu-id="2e2b2-189">Wenn Sie die Kacheln nach Wunsch angeordnet haben, klicken Sie auf **Anpassung abgeschlossen**, oder klicken Sie mit der rechten Maustaste und klicken dann auf **Anpassung abgeschlossen**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-189">When you have arranged the tiles as you want them, either click **Done customizing**, or right-click and then click **Done customizing**.</span></span>

## <a name="edit-a-dashboard-by-changing-the-json-file"></a><span data-ttu-id="2e2b2-190">Bearbeiten eines Dashboards durch Ändern der JSON-Datei</span><span class="sxs-lookup"><span data-stu-id="2e2b2-190">Edit a dashboard by changing the JSON file</span></span>

<span data-ttu-id="2e2b2-191">Sie können ein Dashboard auch durch Ändern der JSON-Datei bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-191">You can also edit a dashboard by changing the JSON file.</span></span> <span data-ttu-id="2e2b2-192">Diese Vorgehensweise bietet mehr Optionen für das Ändern von Einstellungen, aber Sie können die Änderungen erst sehen, nachdem Sie die Datei wieder in Azure hochgeladen haben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-192">This approach provides more options for changing settings, but you cannot see the changes until you upload the file back into Azure.</span></span>

![JSON-Einstellungen](../media-draft/8-json-code.png)

<span data-ttu-id="2e2b2-194">Um im Beispiel oben die Größe der Kachel zu ändern, bearbeiten Sie die Variablen **colSpan** und **rowSpan**. Speichern Sie dann die Datei, und laden Sie sie wieder in Azure hoch.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-194">In the example above, to change the size of the tile, edit the **colSpan** and **rowSpan** variables, then save the file and upload it back to Azure.</span></span> <span data-ttu-id="2e2b2-195">Sie können die Datei auch an andere Benutzer verteilen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-195">You can also distribute the file to other users.</span></span>

## <a name="reset-a-dashboard"></a><span data-ttu-id="2e2b2-196">Zurücksetzen eines Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-196">Reset a dashboard</span></span>

<span data-ttu-id="2e2b2-197">Sie können jedes Dashboard auf den Standardstil zurücksetzen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-197">You can reset any dashboard to the default style.</span></span> <span data-ttu-id="2e2b2-198">Klicken Sie im Bearbeitungsmodus mit der rechten Maustaste, und wählen Sie **Auf Standardzustand zurücksetzen** aus.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-198">In edit mode, right-click and select **Reset to default state**.</span></span> <span data-ttu-id="2e2b2-199">Sie werden in einem Dialogfeld aufgefordert, zu bestätigen, dass Sie dieses Dashboard zurücksetzen möchten.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-199">A dialog box will ask you to confirm that you want to reset that dashboard.</span></span>

<a name="share-dashboard"></a>

## <a name="share-or-unshare-a-dashboard"></a><span data-ttu-id="2e2b2-200">Freigeben bzw. Aufheben der Freigabe eines Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-200">Share or unshare a dashboard</span></span>

<span data-ttu-id="2e2b2-201">Wenn Sie ein neues Dashboard definieren, ist es privat und nur für Ihr Konto sichtbar.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-201">When you define a new dashboard, it is private and visible only to your account.</span></span> <span data-ttu-id="2e2b2-202">Um anderen Benutzer die Ansicht des Dashboards zu ermöglichen, müssen Sie es freigeben.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-202">To make it visible to others, you need to share a dashboard.</span></span> <span data-ttu-id="2e2b2-203">Sie müssen jedoch, wie bei jeder anderen Azure-Ressource auch, eine Ressourcengruppe angeben (oder eine vorhandenen Ressourcengruppe verwenden), in der freigegebene Dashboards gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-203">However, as with any other Azure resource, you need to specify a resource group (or use an existing resource group) to store shared dashboards in.</span></span> <span data-ttu-id="2e2b2-204">Wenn Sie nicht über eine vorhandene Ressourcengruppe verfügen, erstellt Azure die Ressourcengruppe *Dashboards* an einem von Ihnen angegebenen Speicherort.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-204">If you do not have an existing resource group, Azure will create a *dashboards* resource group in whichever location you specify.</span></span> <span data-ttu-id="2e2b2-205">Wenn Sie über eine Ressourcengruppe verfügen, können Sie diese verwenden, um die Dashboards zu speichern.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-205">If you have existing resource groups, you can specify that resource group to store the dashboards.</span></span>

![Freigabe und Zugriffssteuerung 1](../media-draft/8-share-dashboards-default.png)

<span data-ttu-id="2e2b2-207">Wenn Sie die Vorlage freigegeben haben, sehen Sie ein zweites Blatt: **Freigabe + Zugriffssteuerung**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-207">When you have shared the template, you will see a second **Sharing + access control** blade.</span></span>

![Freigabe und Zugriffssteuerung 2](../media-draft/8-share-dashboards-access-control.png)

<span data-ttu-id="2e2b2-209">Sie können dann auf **Benutzer verwalten** klicken, um die Benutzer anzugeben, die auf dieses Dashboard zugreifen dürfen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-209">You can then click **Manage users** to specify the users who have access to that dashboard.</span></span>

### <a name="switching-to-a-shared-dashboard"></a><span data-ttu-id="2e2b2-210">Wechsel zu einem freigegebenen Dashboard</span><span class="sxs-lookup"><span data-stu-id="2e2b2-210">Switching to a shared dashboard</span></span>

<span data-ttu-id="2e2b2-211">Um zu einem freigegebenen Dashboard zu wechseln, klicken Sie auf die Liste der Dashboards und dann auf **Alle Dashboards durchsuchen**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-211">To switch to a shared dashboard, you click on the list of dashboards, and then click **Browse all dashboards**.</span></span>

![Alle Dashboards durchsuchen](../media-draft/8-browse-dashboards.png)

<span data-ttu-id="2e2b2-213">Sie sehen das Blatt **Alle Dashboards**, auf dem die Namen aller freigegebenen Dashboards angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-213">You will now see the **All dashboards** blade, with the names of any shared dashboards displayed.</span></span> <span data-ttu-id="2e2b2-214">Klicken Sie auf ein Dashboard, um es auf das Azure-Portal anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-214">Just click on a dashboard to apply it to the Azure portal.</span></span>

![Freigegebene Dashboards](../media-draft/8-select-shared-dashboard.png)

<a name="full-screen"></a>

## <a name="display-a-dashboard-as-a-full-screen"></a><span data-ttu-id="2e2b2-216">Anzeigen eines Dashboards im Vollbildmodus</span><span class="sxs-lookup"><span data-stu-id="2e2b2-216">Display a dashboard as a full screen</span></span>

<span data-ttu-id="2e2b2-217">Wenn Sie das Dashboard möglichst groß anzeigen möchten, klicken Sie auf die Schaltfläche **Vollbild**, um Ihr aktuelles Dashboard ohne Browsermenüs anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-217">If you want the largest dashboard real estate, click the **Full screen** button to display your current dashboard without any browser menus.</span></span> <span data-ttu-id="2e2b2-218">Falls sich Kacheln außerhalb der Bildschirmanzeige befinden, werden rechts und unten auf dem Bildschirm Schieberegler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-218">If you have any tiles outside the boundaries of your screen display, slider bars will appear at the right and bottom of your screen.</span></span>

<span data-ttu-id="2e2b2-219">Um den Vollbildmodus zu beenden, drücken Sie die ESC-Taste, oder klicken Sie am oberen Bildschirmrand neben dem Dashboardnamen auf **Vollbildmodus beenden**.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-219">When you have finished working in full-screen mode, press the ESC key or click **Exit Full Screen** next to the Dashboard name at the top of the screen.</span></span>

<a name="clone-dashboard"></a>

## <a name="clone-a-dashboard"></a><span data-ttu-id="2e2b2-220">Klonen eines Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-220">Clone a dashboard</span></span>

<span data-ttu-id="2e2b2-221">Beim Klonen eines Dashboards wird eine Sofortkopie namens „Klon von \<Dashboardname>“ erstellt, wobei diese Kopie zum aktuellen Dashboard wird.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-221">Cloning a dashboard creates an instant copy called "Clone of \<dashboard name>" and switches to that copy as the current dashboard.</span></span> <span data-ttu-id="2e2b2-222">Klonen ist auch eine einfache Möglichkeit, Dashboards zu erstellen, bevor sie freigegeben werden.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-222">Cloning is also an easy way to create dashboards before sharing them.</span></span> <span data-ttu-id="2e2b2-223">Wenn Sie z.B. über ein Dashboard verfügen, das bereits fast Ihren Wünschen entspricht, klonen Sie es, nehmen die notwendigen Änderungen vor und geben es dann frei.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-223">For example, if you have a dashboard that is almost as you want it, clone it, make the changes that you need, and then share it.</span></span>

<a name="delete-dashboard"></a>

## <a name="delete-a-dashboard"></a><span data-ttu-id="2e2b2-224">Löschen eines Dashboards</span><span class="sxs-lookup"><span data-stu-id="2e2b2-224">Delete a dashboard</span></span>

<span data-ttu-id="2e2b2-225">Durch Löschen eines Dashboards wird es aus der Liste der verfügbaren Dashboards entfernt.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-225">Deleting a dashboard removes it from your list of available dashboards.</span></span> <span data-ttu-id="2e2b2-226">Sie werden aufgefordert zu bestätigen, dass Sie das Dashboard löschen möchten. Beachten Sie aber, dass es keine Möglichkeit gibt, ein gelöschtes Dashboard wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-226">You are prompted to confirm that you want to delete the dashboard, but there is no facility to recover a dashboard that has been deleted.</span></span>

<span data-ttu-id="2e2b2-227">Wir werden nun einige dieser Optionen ausprobieren, indem wir ein neues Dashboard erstellen.</span><span class="sxs-lookup"><span data-stu-id="2e2b2-227">Let's try out some of these options by creating a new dashboard.</span></span>
