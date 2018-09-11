### <a name="exercise-4-test-the-model"></a><span data-ttu-id="d090b-101">Übung 4: Testen des Modells</span><span class="sxs-lookup"><span data-stu-id="d090b-101">Exercise 4: Test the model</span></span>

<span data-ttu-id="d090b-102">In [Übung 5](../5-build-app.yml) erstellen Sie eine Node.js-App, die das Modell verwendet, um den Künstler von Bildern zu identifizieren, die ihr vorgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d090b-102">In [Exercise 5](../5-build-app.yml), you will create a Node.js app that uses the model to identify the artist of paintings presented to it.</span></span> <span data-ttu-id="d090b-103">Sie müssen jedoch keine App schreiben, um das Modell zu testen. Sie können Ihre Tests im Portal ausführen und das Modell mithilfe der Bilder, die Sie zum Testen verwenden, weiter optimieren.</span><span class="sxs-lookup"><span data-stu-id="d090b-103">But you don't have to write an app to test the model; you can do your testing in the portal, and you can further refine the model using the images that you test with.</span></span> <span data-ttu-id="d090b-104">In dieser Übung testen Sie mithilfe für Sie bereitgestellter Bilder die Fähigkeit des Modells, den Künstler eines Gemäldes zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="d090b-104">In this exercise, you will test the model's ability to identify the artist of a painting using test images provided for you.</span></span>

1. <span data-ttu-id="d090b-105">Klicken Sie ganz oben auf der Seite auf **Quick Test** (Schnelltest).</span><span class="sxs-lookup"><span data-stu-id="d090b-105">Click **Quick Test** at the top of the page.</span></span>
 
    ![Testen des Modells](../images/portal-click-quick-test.png)

    <span data-ttu-id="d090b-107">_Testen des Modells_</span><span class="sxs-lookup"><span data-stu-id="d090b-107">_Testing the model_</span></span> 

1. <span data-ttu-id="d090b-108">Klicken Sie auf **Lokale Dateien durchsuchen**, und navigieren Sie dann in den Ressourcen für die Aufgaben zum Ordner „Quick Tests“.</span><span class="sxs-lookup"><span data-stu-id="d090b-108">Click **Browse local files**, and then browse to the "Quick Tests" folder in the lab resources.</span></span> <span data-ttu-id="d090b-109">Wählen Sie **PicassoTest_01.jpg** aus, und klicken Sie auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="d090b-109">Select **PicassoTest_01.jpg**, and click **Open**.</span></span>

    ![Auswählen eines Picasso-Testbilds](../images/portal-select-test-01.png)

    <span data-ttu-id="d090b-111">_Auswählen eines Picasso-Testbilds_</span><span class="sxs-lookup"><span data-stu-id="d090b-111">_Selecting a Picasso test image_</span></span> 

1. <span data-ttu-id="d090b-112">Überprüfen Sie die Ergebnisse des Tests im Dialogfeld „Quick Test“.</span><span class="sxs-lookup"><span data-stu-id="d090b-112">Examine the results of the test in the "Quick Test" dialog.</span></span> <span data-ttu-id="d090b-113">Mit welcher Wahrscheinlichkeit ist das Gemälde von Picasso?</span><span class="sxs-lookup"><span data-stu-id="d090b-113">What is the probability that the painting is a Picasso?</span></span> <span data-ttu-id="d090b-114">Mit welcher Wahrscheinlichkeit ist es von Rembrandt oder Pollock?</span><span class="sxs-lookup"><span data-stu-id="d090b-114">What is the probability that it is a Rembrandt or Pollock?</span></span>

1. <span data-ttu-id="d090b-115">Schließen Sie das Dialogfeld „Quick Test“.</span><span class="sxs-lookup"><span data-stu-id="d090b-115">Close the "Quick Test" dialog.</span></span> <span data-ttu-id="d090b-116">Klicken Sie dann am oberen Rand der Seite auf **Vorhersagen**.</span><span class="sxs-lookup"><span data-stu-id="d090b-116">Then click **Predictions** at the top of the page.</span></span>
 
    ![Anzeigen der Tests, die durchgeführt wurden](../images/portal-select-predictions.png)

    <span data-ttu-id="d090b-118">_Anzeigen der Tests, die durchgeführt wurden_</span><span class="sxs-lookup"><span data-stu-id="d090b-118">_Viewing the tests that have been performed_</span></span> 

1. <span data-ttu-id="d090b-119">Klicken Sie auf das Testbild, das Sie hochgeladen haben, um eine Detailansicht anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="d090b-119">Click the test image that you uploaded to show a detail of it.</span></span> <span data-ttu-id="d090b-120">Markieren Sie das Bild dann als ein „Picasso“, indem Sie in der Dropdownliste **Picasso** auswählen und auf **Speichern und schließen** klicken.</span><span class="sxs-lookup"><span data-stu-id="d090b-120">Then tag the image as a "Picasso" by selecting **Picasso** from the drop-down list and clicking **Save and close**.</span></span>

    > <span data-ttu-id="d090b-121">Indem Sie die Testbilder auf diese Weise markieren, können Sie das Modell optimieren, ohne zusätzliche Trainingsbilder hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="d090b-121">By tagging test images this way, you can refine the model without uploading additional training images.</span></span>
 
    ![Markieren des Testbilds](../images/tag-test-image.png)

    <span data-ttu-id="d090b-123">_Markieren des Testbilds_</span><span class="sxs-lookup"><span data-stu-id="d090b-123">_Tagging the test image_</span></span> 

1. <span data-ttu-id="d090b-124">Führen Sie einen weiteren Schnelltest mit der Datei **FlowersTest.jpg** im Ordner „Quick Test“ durch.</span><span class="sxs-lookup"><span data-stu-id="d090b-124">Perform another quick test using the file named **FlowersTest.jpg** in the "Quick Test" folder.</span></span> <span data-ttu-id="d090b-125">Vergewissern Sie sich, dass diesem Bild eine niedrige Wahrscheinlichkeit zugeordnet ist, von Picasso, Rembrandt oder Pollock zu stammen.</span><span class="sxs-lookup"><span data-stu-id="d090b-125">Confirm that this image is assigned a low probability of being a Picasso, a Rembrandt, or a Pollock.</span></span>

<span data-ttu-id="d090b-126">Das Modell wurde trainiert und ist einsatzbereit, es scheint erfahren im Identifizieren von Gemälden gewisser Künstler zu sein.</span><span class="sxs-lookup"><span data-stu-id="d090b-126">The model is trained and ready to go and appears to be adept at identifying paintings by certain artists.</span></span> <span data-ttu-id="d090b-127">Gehen Sie nun einen Schritt weiter, und integrieren Sie die Intelligenz des Modells in eine App.</span><span class="sxs-lookup"><span data-stu-id="d090b-127">Now let's go a step further and incorporate the model's intelligence into an app.</span></span>