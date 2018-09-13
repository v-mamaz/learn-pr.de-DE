<span data-ttu-id="aa359-101">In dieser Übung fügen Sie Bilder berühmter Originalwerke von Picasso, Pollock und Rembrandt dem Artworks-Projekt hinzu und markieren die Bilder, damit der Custom Vision Service lernen kann, die Künstler voneinander zu unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="aa359-101">In this unit, you will add images of famous paintings by Picasso, Pollock, and Rembrandt to the Artworks project, and tag the images so the Custom Vision Service can learn to differentiate one artist from another.</span></span>
  
1. <span data-ttu-id="aa359-102">Klicken Sie auf **Bilder hinzufügen**, um dem Projekt Bilder hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="aa359-102">Click **Add images** to add images to the project.</span></span>

    ![Hinzufügen von Bildern zum Artworks-Projekt](../media-draft/2-portal-click-add-images.png)

1. <span data-ttu-id="aa359-104">Klicken Sie auf **Lokale Dateien durchsuchen**.</span><span class="sxs-lookup"><span data-stu-id="aa359-104">Click **Browse local files**.</span></span>

    ![Suchen nach lokalen Bildern](../media-draft/2-portal-click-browse-local-files.png)

    <span data-ttu-id="aa359-106">_Suchen nach lokalen Bildern_</span><span class="sxs-lookup"><span data-stu-id="aa359-106">_Browsing for local images_</span></span> 
 
1. <span data-ttu-id="aa359-107">Navigieren Sie in den [Ressourcen, die dieses Modul begleiten](https://a4r.blob.core.windows.net/public/cvs-resources.zip), zum Ordner „Artists\Picasso“, wählen Sie alle Dateien im Ordner aus, und klicken Sie auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="aa359-107">Browse to the "Artists\Picasso" folder in the [resources that accompany this module](https://a4r.blob.core.windows.net/public/cvs-resources.zip), select all of the files in the folder, and click **Open**.</span></span>

    ![Auswahl eines Bildes](../media-draft/2-fe-browse-picasso-01.png)

1. <span data-ttu-id="aa359-109">Geben Sie „painting“ (Gemälde) (ohne Anführungszeichen) in das Feld **Ein paar Tags hinzufügen...** ein.</span><span class="sxs-lookup"><span data-stu-id="aa359-109">Type "painting" (without quotation marks) into the **Add some tags...** box.</span></span> <span data-ttu-id="aa359-110">Klicken Sie dann auf **+**, um das Tag den Bildern zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="aa359-110">Then click **+** to assign the tag to the images.</span></span>

    ![Hinzufügen eines „painting“-Tags zu den Bildern](../media-draft/2-portal-add-tags-01.png)

1. <span data-ttu-id="aa359-112">Wiederholen Sie Schritt 4, um den Bildern ein „Picasso“-Tag hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="aa359-112">Repeat Step 4 to add a "Picasso" tag to the images.</span></span>

1. <span data-ttu-id="aa359-113">Klicken Sie auf **7 Dateien hochladen**, um die Bilder hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="aa359-113">Click **Upload 7 files** to upload the images.</span></span> <span data-ttu-id="aa359-114">Nachdem der Upload abgeschlossen ist, klicken Sie auf **Fertig**.</span><span class="sxs-lookup"><span data-stu-id="aa359-114">Once the upload has finished, click **Done**.</span></span>

    ![Hochladen von markierten Bildern](../media-draft/2-upload-picasso-images.png)

1. <span data-ttu-id="aa359-116">Vergewissern Sie sich, dass die Bilder, die Sie hochgeladen haben, zusammen mit den ihnen zugewiesenen Tags im Portal angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="aa359-116">Confirm that the images you uploaded appear in the portal, along with the tags assigned to them.</span></span>

    ![Die hochgeladenen Bildern](../media-draft/2-portal-tagged-01.png)

1. <span data-ttu-id="aa359-118">Mit sieben Bildern von Picasso kann der Custom Vision Service Originalwerke von Picasso einigermaßen zuverlässig identifizieren.</span><span class="sxs-lookup"><span data-stu-id="aa359-118">With seven Picasso images, the Custom Vision Service can do a decent job of identifying paintings by Picasso.</span></span> <span data-ttu-id="aa359-119">Aber wenn Sie das Modell gerade jetzt trainiert haben, würde es nur verstehen, wie ein Picasso aussieht, und wäre nicht in der Lage, Originalwerke anderer Künstler zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="aa359-119">But if you trained the model right now, it would only understand what a Picasso looks like, and it would not be able to identify paintings by other artists.</span></span>

    <span data-ttu-id="aa359-120">Im nächsten Schritt werden einige Originalwerke eines anderen Künstlers hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="aa359-120">The next step is to upload some paintings by another artist.</span></span> <span data-ttu-id="aa359-121">Klicken Sie auf **Bilder hinzufügen**, und wählen Sie alle Bilder im Ordner „Artists\Rembrandt“ in den Modulressourcen aus.</span><span class="sxs-lookup"><span data-stu-id="aa359-121">Click **Add images** and select all of the images in the "Artists\Rembrandt" folder in the module resources.</span></span> <span data-ttu-id="aa359-122">Markieren Sie sie mit den Bezeichnungen „painting“ und „Rembrandt“ (nicht „Picasso“), und laden Sie sie in das Projekt hoch.</span><span class="sxs-lookup"><span data-stu-id="aa359-122">Tag them with the labels "painting" and "Rembrandt" (not "Picasso"), and upload them to the project.</span></span>

    > <span data-ttu-id="aa359-123">Wenn Sie das Tag „painting“ hinzufügen, müssen Sie es nicht erneut eingeben.</span><span class="sxs-lookup"><span data-stu-id="aa359-123">When you add the tag "painting," you don't have to type it in again.</span></span> <span data-ttu-id="aa359-124">Sie können es aus der Dropdownliste auswählen, die dem Feld **Ein paar Tags hinzufügen...** angefügt ist, wie unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="aa359-124">You can select it from the drop-down list attached to the **Add some tags...** box, as shown below.</span></span> <span data-ttu-id="aa359-125">Sie **müssen** „Rembrandt“ eingeben und auf **+** klicken, um ein „Rembrandt“-Tag hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="aa359-125">You **will** have to type "Rembrandt" and click **+** to add a "Rembrandt" tag.</span></span>

    ![Auswahl eines vorhandenen Tags](../media-draft/2-select-painting-tag.png)

1. <span data-ttu-id="aa359-127">Vergewissern Sie sich, dass die Bilder Rembrandts zusammen mit den Bildern Picassos im Projekt angezeigt werden, und dass „Rembrandt“ in der Liste der Tags angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="aa359-127">Confirm that the Rembrandt images appear alongside the Picasso images in the project, and that "Rembrandt" appears in the list of tags.</span></span>

    ![Bilder von Picasso und Rembrandt](../media-draft/2-portal-tagged-02.png)

1. <span data-ttu-id="aa359-129">Fügen Sie nun Originalwerke des geheimnisvollen Künstlers Jackson Pollock hinzu, damit der Custom Vision Service Originalwerke Pollocks ebenfalls erkennen kann.</span><span class="sxs-lookup"><span data-stu-id="aa359-129">Now add paintings by the enigmatic artist Jackson Pollock to enable the Custom Vision Service to recognize Pollock paintings, too.</span></span> <span data-ttu-id="aa359-130">Wählen Sie alle Bilder im Ordner „Artists\Pollock“ in den Modulressourcen aus, markieren Sie sie mit den Begriffen „painting“ und „Pollock“, und laden Sie sie in das Projekt hoch.</span><span class="sxs-lookup"><span data-stu-id="aa359-130">Select all of the images in the "Artists\Pollock" folder in the module resources, tag them with the terms "painting" and "Pollock", and upload them to the project.</span></span>

<span data-ttu-id="aa359-131">Wenn die markierten Bilder hochgeladen sind, trainieren Sie im nächsten Schritt das Modell mit diesen Bildern, damit es sowohl zwischen Originalwerken von Picasso, Rembrandt und Pollock unterscheiden als auch bestimmen kann, ob ein Gemälde eine Arbeit eines dieser berühmten Künstler ist.</span><span class="sxs-lookup"><span data-stu-id="aa359-131">With the tagged images uploaded, the next step is to train the model with these images so it can distinguish between paintings by Picasso, Rembrandt, and Pollock, as well as determine whether a painting is a work by one of these famous artists.</span></span>