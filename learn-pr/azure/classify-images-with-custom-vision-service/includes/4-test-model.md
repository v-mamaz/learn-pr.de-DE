<span data-ttu-id="3a220-101">Nachdem Sie das Modell trainiert haben, ist es an der Zeit, es zu testen.</span><span class="sxs-lookup"><span data-stu-id="3a220-101">Now that we've trained our model, it's time to test it.</span></span> <span data-ttu-id="3a220-102">Sie stellen dem Modell neue Bilder zur Verfügung und sehen, wie gut es diese klassifiziert.</span><span class="sxs-lookup"><span data-stu-id="3a220-102">We'll give the model new images and see how well it classifies it.</span></span>

1. <span data-ttu-id="3a220-103">Klicken Sie oben auf der Seite auf **Quick Test** (Schnelltest).</span><span class="sxs-lookup"><span data-stu-id="3a220-103">Click **Quick Test** at the top of the page.</span></span>

    ![Testen des Modells](../media/4-portal-click-quick-test.png)

1. <span data-ttu-id="3a220-105">Klicken Sie auf **Lokale Dateien durchsuchen**, und navigieren Sie dann in den Modulressourcen zum Ordner „Quick Tests“, den Sie zuvor heruntergeladen haben.</span><span class="sxs-lookup"><span data-stu-id="3a220-105">Click **Browse local files**, and then browse to the "Quick Tests" folder in the module resources folder you download previously.</span></span> <span data-ttu-id="3a220-106">Wählen Sie **PicassoTest_01.jpg** aus, und klicken Sie auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="3a220-106">Select **PicassoTest_01.jpg**, and click **Open**.</span></span>

    ![Auswählen eines Picasso-Testbilds](../media/4-portal-select-test-01.png)

1. <span data-ttu-id="3a220-108">Überprüfen Sie die Ergebnisse des Tests im Dialogfeld „Quick Test“.</span><span class="sxs-lookup"><span data-stu-id="3a220-108">Examine the results of the test in the "Quick Test" dialog.</span></span> <span data-ttu-id="3a220-109">Mit welcher Wahrscheinlichkeit ist das Gemälde von Picasso?</span><span class="sxs-lookup"><span data-stu-id="3a220-109">What is the probability that the painting is a Picasso?</span></span> <span data-ttu-id="3a220-110">Mit welcher Wahrscheinlichkeit ist es von Rembrandt oder Pollock?</span><span class="sxs-lookup"><span data-stu-id="3a220-110">What is the probability that it's a Rembrandt or Pollock?</span></span>

    ![Auswählen eines Picasso-Testbilds](../media/4-quick-test-result.png)

1. <span data-ttu-id="3a220-112">Schließen Sie das Dialogfeld „Quick Test“.</span><span class="sxs-lookup"><span data-stu-id="3a220-112">Close the "Quick Test" dialog.</span></span> <span data-ttu-id="3a220-113">Klicken Sie dann am oberen Rand der Seite auf **Vorhersagen**.</span><span class="sxs-lookup"><span data-stu-id="3a220-113">Then click **Predictions** at the top of the page.</span></span>

    ![Anzeigen der Tests, die durchgeführt wurden](../media/4-portal-select-predictions.png)

1. <span data-ttu-id="3a220-115">Klicken Sie auf das Testbild, das Sie hochgeladen haben, um eine Detailansicht anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="3a220-115">Click the test image that you uploaded to show a detail of it.</span></span> <span data-ttu-id="3a220-116">Markieren Sie das Bild dann als ein „Picasso“, indem Sie in der Dropdownliste **Picasso** auswählen und auf **Speichern und schließen** klicken.</span><span class="sxs-lookup"><span data-stu-id="3a220-116">Then tag the image as a "Picasso" by selecting **Picasso** from the drop-down list and clicking **Save and close**.</span></span>

    > <span data-ttu-id="3a220-117">Indem Sie die Testbilder auf diese Weise markieren, können Sie das Modell optimieren, ohne zusätzliche Trainingsbilder hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="3a220-117">By tagging test images this way, you can refine the model without uploading additional training images.</span></span>

    ![Markieren des Testbilds](../media/4-tag-test-image.png)

1. <span data-ttu-id="3a220-119">Führen Sie einen weiteren Schnelltest durch, und verwenden Sie dieses Mal im Ordner „Quick Test“ die Datei **FlowersTest.jpg**.</span><span class="sxs-lookup"><span data-stu-id="3a220-119">Run another quick test, this time using the file named **FlowersTest.jpg** in the "Quick Test" folder.</span></span> <span data-ttu-id="3a220-120">Vergewissern Sie sich, dass diesem Bild eine niedrige Wahrscheinlichkeit zugeordnet ist, von Picasso, Rembrandt oder Pollock zu stammen.</span><span class="sxs-lookup"><span data-stu-id="3a220-120">Confirm that this image is assigned a low probability of being a Picasso, a Rembrandt, or a Pollock.</span></span>

<span data-ttu-id="3a220-121">Das Modell wurde trainiert und ist einsatzbereit, es scheint erfahren im Identifizieren von Gemälden gewisser Künstler zu sein.</span><span class="sxs-lookup"><span data-stu-id="3a220-121">The model is trained and ready to go and appears to be skilled at identifying paintings by certain artists.</span></span> <span data-ttu-id="3a220-122">Rufen Sie den Vorhersageendpunkt über HTTP auf, und sehen Sie, was passiert.</span><span class="sxs-lookup"><span data-stu-id="3a220-122">Let's call the prediction endpoint over HTTP and see what happens.</span></span>