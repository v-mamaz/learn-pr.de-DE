### <a name="exercise-2-upload-tagged-images"></a><span data-ttu-id="c2fee-101">Übung 2: Hochladen von markierten Bildern</span><span class="sxs-lookup"><span data-stu-id="c2fee-101">Exercise 2: Upload tagged images</span></span>

<span data-ttu-id="c2fee-102">In dieser Übung fügen Sie Bilder berühmter Originalwerke von Picasso, Pollock und Rembrandt dem Artworks-Projekt hinzu und markieren die Bilder, damit der Custom Vision Service lernen kann, die Künstler voneinander zu unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="c2fee-102">In this exercise, you will add images of famous paintings by Picasso, Pollock, and Rembrandt to the Artworks project, and tag the images so the Custom Vision Service can learn to differentiate one artist from another.</span></span>
  
1. <span data-ttu-id="c2fee-103">Klicken Sie auf **Bilder hinzufügen**, um dem Projekt Bilder hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c2fee-103">Click **Add images** to add images to the project.</span></span>

    ![Hinzufügen von Bildern zum Artworks-Projekt](../images/portal-click-add-images.png)

    <span data-ttu-id="c2fee-105">_Hinzufügen von Bildern zum Artworks-Projekt_</span><span class="sxs-lookup"><span data-stu-id="c2fee-105">_Adding images to the Artworks project_</span></span> 
 
1. <span data-ttu-id="c2fee-106">Klicken Sie auf **Lokale Dateien durchsuchen**.</span><span class="sxs-lookup"><span data-stu-id="c2fee-106">Click **Browse local files**.</span></span>

    ![Suchen nach lokalen Bildern](../images/portal-click-browse-local-files.png)

    <span data-ttu-id="c2fee-108">_Suchen nach lokalen Bildern_</span><span class="sxs-lookup"><span data-stu-id="c2fee-108">_Browsing for local images_</span></span> 
 
1. <span data-ttu-id="c2fee-109">Navigieren Sie in den [Ressourcen, die diese Übung begleiten](https://a4r.blob.core.windows.net/public/cvs-resources.zip), zum Ordner „Artists\Picasso“, wählen Sie alle Dateien im Ordner aus, und klicken Sie auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="c2fee-109">Browse to the "Artists\Picasso" folder in the [resources that accompany this lab](https://a4r.blob.core.windows.net/public/cvs-resources.zip), select all of the files in the folder, and click **Open**.</span></span>

    ![Auswahl eines Bildes](../images/fe-browse-picasso-01.png)

    <span data-ttu-id="c2fee-111">_Auswahl eines Bildes_</span><span class="sxs-lookup"><span data-stu-id="c2fee-111">_Selecting an image_</span></span> 
 
1. <span data-ttu-id="c2fee-112">Geben Sie „painting“ (Gemälde) (ohne Anführungszeichen) in das Feld **Ein paar Tags hinzufügen...** ein.</span><span class="sxs-lookup"><span data-stu-id="c2fee-112">Type "painting" (without quotation marks) into the **Add some tags...** box.</span></span> <span data-ttu-id="c2fee-113">Klicken Sie dann auf **+**, um das Tag den Bildern zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="c2fee-113">Then click **+** to assign the tag to the images.</span></span>

    ![Hinzufügen eines „painting“-Tags zu den Bildern](../images/portal-add-tags-01.png)

    <span data-ttu-id="c2fee-115">_Hinzufügen eines „painting“-Tags zu den Bildern_</span><span class="sxs-lookup"><span data-stu-id="c2fee-115">_Adding a "painting" tag to the images_</span></span> 

1. <span data-ttu-id="c2fee-116">Wiederholen Sie Schritt 4, um den Bildern ein „Picasso“-Tag hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c2fee-116">Repeat Step 4 to add a "Picasso" tag to the images.</span></span>

1. <span data-ttu-id="c2fee-117">Klicken Sie auf **7 Dateien hochladen**, um die Bilder hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="c2fee-117">Click **Upload 7 files** to upload the images.</span></span> <span data-ttu-id="c2fee-118">Nachdem der Upload abgeschlossen ist, klicken Sie auf **Fertig**.</span><span class="sxs-lookup"><span data-stu-id="c2fee-118">Once the upload has completed, click **Done**.</span></span>

    ![Hochladen von markierten Bildern](../images/upload-picasso-images.png)

    <span data-ttu-id="c2fee-120">_Hochladen von markierten Bildern_</span><span class="sxs-lookup"><span data-stu-id="c2fee-120">_Uploading tagged images_</span></span> 

1. <span data-ttu-id="c2fee-121">Vergewissern Sie sich, dass die Bilder, die Sie hochgeladen haben, zusammen mit den ihnen zugewiesenen Tags im Portal angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c2fee-121">Confirm that the images you uploaded appear in the portal, along with the tags assigned to them.</span></span>

    ![Die hochgeladenen Bildern](../images/portal-tagged-01.png)

    <span data-ttu-id="c2fee-123">_Die hochgeladenen Bildern_</span><span class="sxs-lookup"><span data-stu-id="c2fee-123">_The uploaded images_</span></span> 

1. <span data-ttu-id="c2fee-124">Mit sieben Bildern von Picasso kann der Custom Vision Service Originalwerke von Picasso einigermaßen zuverlässig identifizieren.</span><span class="sxs-lookup"><span data-stu-id="c2fee-124">With seven Picasso images, the Custom Vision Service can do a decent job of identifying paintings by Picasso.</span></span> <span data-ttu-id="c2fee-125">Aber wenn Sie das Modell gerade jetzt trainiert haben, würde es nur verstehen, wie ein Picasso aussieht, und wäre nicht in der Lage, Originalwerke anderer Künstler zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="c2fee-125">But if you trained the model right now, it would only understand what a Picasso looks like, and it would not be able to identify paintings by other artists.</span></span>

    <span data-ttu-id="c2fee-126">Im nächsten Schritt werden einige Originalwerke eines anderen Künstlers hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="c2fee-126">The next step is to upload some paintings by another artist.</span></span> <span data-ttu-id="c2fee-127">Klicken Sie auf **Bilder hinzufügen**, und wählen Sie alle Bilder im Ordner „Artists\Rembrandt“ in den Lab-Ressourcen aus.</span><span class="sxs-lookup"><span data-stu-id="c2fee-127">Click **Add images** and select all of the images in the "Artists\Rembrandt" folder in the lab resources.</span></span> <span data-ttu-id="c2fee-128">Markieren Sie sie mit den Bezeichnungen „painting“ und „Rembrandt“ (nicht „Picasso“), und laden Sie sie in das Projekt hoch.</span><span class="sxs-lookup"><span data-stu-id="c2fee-128">Tag them with the labels "painting" and "Rembrandt" (not "Picasso"), and upload them to the project.</span></span>

    > <span data-ttu-id="c2fee-129">Wenn Sie das Tag „painting“ hinzufügen, müssen Sie es nicht erneut eingeben.</span><span class="sxs-lookup"><span data-stu-id="c2fee-129">When you add the tag "painting," you don't have to type it in again.</span></span> <span data-ttu-id="c2fee-130">Sie können es aus der Dropdownliste auswählen, die dem Feld **Ein paar Tags hinzufügen...** angefügt ist, wie unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c2fee-130">You can select it from the drop-down list attached to the **Add some tags...** box, as shown below.</span></span> <span data-ttu-id="c2fee-131">Sie **müssen** „Rembrandt“ eingeben und auf **+** klicken, um ein „Rembrandt“-Tag hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c2fee-131">You **will** have to type "Rembrandt" and click **+** to add a "Rembrandt" tag.</span></span>

    ![Auswahl eines vorhandenen Tags](../images/select-painting-tag.png)

    <span data-ttu-id="c2fee-133">_Auswahl eines vorhandenen Tags_</span><span class="sxs-lookup"><span data-stu-id="c2fee-133">_Selecting an existing tag_</span></span> 

1. <span data-ttu-id="c2fee-134">Vergewissern Sie sich, dass die Bilder Rembrandts zusammen mit den Bildern Picassos im Projekt angezeigt werden, und dass „Rembrandt“ in der Liste der Tags angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="c2fee-134">Confirm that the Rembrandt images appear alongside the Picasso images in the project, and that "Rembrandt" appears in the list of tags.</span></span>

    ![Bilder von Picasso und Rembrandt](../images/portal-tagged-02.png)

    <span data-ttu-id="c2fee-136">_Bilder von Picasso und Rembrandt_</span><span class="sxs-lookup"><span data-stu-id="c2fee-136">_Picasso and Rembrandt images_</span></span> 

1. <span data-ttu-id="c2fee-137">Fügen Sie nun Originalwerke des geheimnisvollen Künstlers Jackson Pollock hinzu, damit der Custom Vision Service Originalwerke Pollocks ebenfalls erkennen kann.</span><span class="sxs-lookup"><span data-stu-id="c2fee-137">Now add paintings by the enigmatic artist Jackson Pollock to enable the Custom Vision Service to recognize Pollock paintings, too.</span></span> <span data-ttu-id="c2fee-138">Wählen Sie alle Bilder im Ordner „Artists\Pollock“ in den Lab-Ressourcen aus, markieren Sie sie mit den Begriffen „painting“ und „Pollock“, und laden Sie sie in das Projekt hoch.</span><span class="sxs-lookup"><span data-stu-id="c2fee-138">Select all of the images in the "Artists\Pollock" folder in the lab resources, tag them with the terms "painting" and "Pollock", and upload them to the project.</span></span>

<span data-ttu-id="c2fee-139">Wenn die markierten Bilder hochgeladen sind, trainieren Sie im nächsten Schritt das Modell mit diesen Bildern, damit es sowohl zwischen Originalwerken von Picasso, Rembrandt und Pollock unterscheiden als auch bestimmen kann, ob ein Gemälde eine Arbeit eines dieser berühmten Künstler ist.</span><span class="sxs-lookup"><span data-stu-id="c2fee-139">With the tagged images uploaded, the next step is to train the model with these images so it can distinguish between paintings by Picasso, Rembrandt, and Pollock, as well as determine whether a painting is a work by one of these famous artists.</span></span>