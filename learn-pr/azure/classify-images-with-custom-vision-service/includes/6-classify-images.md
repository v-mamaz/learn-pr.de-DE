### <a name="exercise-6-use-the-app-to-classify-images"></a><span data-ttu-id="c87d9-101">Übung 6: Verwenden der App zum Klassifizieren von Bildern</span><span class="sxs-lookup"><span data-stu-id="c87d9-101">Exercise 6: Use the app to classify images</span></span>

<span data-ttu-id="c87d9-102">In dieser Übung verwenden Sie die Artworks-App, um Bilder zur Klassifizierung an den Custom Vision Service zu senden.</span><span class="sxs-lookup"><span data-stu-id="c87d9-102">In this exercise, you will use the Artworks app to submit images to the Custom Vision Service for classification.</span></span> <span data-ttu-id="c87d9-103">Die App nutzt JSON-Informationen, die von Aufrufen der [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814)-Methode der Custom Vision-Vorhersage-API zurückgegeben wurden. Diese teilt mit, ob ein Bild ein Gemälde von Picasso, Rembrandt, Pollock oder von keinem der genannten Maler darstellt.</span><span class="sxs-lookup"><span data-stu-id="c87d9-103">The app uses the JSON information returned from calls to the Custom Vision Prediction API's [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) method to tell you whether an image represents a painting by Picasso, Rembrandt, Pollock, or none of the above.</span></span> <span data-ttu-id="c87d9-104">Es wird auch die Wahrscheinlichkeit angegeben, dass die Klassifizierung, die dem Bild zugewiesen ist, richtig ist.</span><span class="sxs-lookup"><span data-stu-id="c87d9-104">It also shows the probability that the classification assigned to the image is correct.</span></span>

1. <span data-ttu-id="c87d9-105">Klicken Sie auf die Schaltfläche **Browse (...)** (Durchsuchen) in der Artworks-App.</span><span class="sxs-lookup"><span data-stu-id="c87d9-105">Click the **Browse (...)** button in the Artworks app.</span></span> 

    ![Suche nach lokalen Bildern in der Artworks-App](../images/app-click-browse.png)

    <span data-ttu-id="c87d9-107">_Suche nach lokalen Bildern in der Artworks-App_</span><span class="sxs-lookup"><span data-stu-id="c87d9-107">_Browsing for local images in the Artworks app_</span></span> 

1. <span data-ttu-id="c87d9-108">Navigieren Sie dann in den Ressourcen für die Aufgaben zum Ordner „Quick Tests“.</span><span class="sxs-lookup"><span data-stu-id="c87d9-108">Browse to the "Quick Tests" folder in the lab resources.</span></span> <span data-ttu-id="c87d9-109">Wählen Sie die Datei mit der Bezeichnung **PicassoTest_02.jpg** aus, und klicken Sie auf **Open** (Öffnen).</span><span class="sxs-lookup"><span data-stu-id="c87d9-109">Select the file named **PicassoTest_02.jpg**, and then click **Open**.</span></span>

1. <span data-ttu-id="c87d9-110">Klicken Sie auf die Schaltfläche **Predict** (Vorhersagen), um das Bild an den Custom Vision Service zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="c87d9-110">Click the **Predict** button to submit the image to the Custom Vision Service.</span></span>

    ![Übermitteln des Bilds an den Custom Vision Service](../images/app-click-predict.png)

    <span data-ttu-id="c87d9-112">_Übermitteln des Bilds an den Custom Vision Service_</span><span class="sxs-lookup"><span data-stu-id="c87d9-112">_Submitting the image to the Custom Vision Service_</span></span> 

1. <span data-ttu-id="c87d9-113">Bestätigen Sie, dass die App das Gemälde als einen Picasso erkennt.</span><span class="sxs-lookup"><span data-stu-id="c87d9-113">Confirm that the app identifies the painting as a Picasso.</span></span>

    ![Klassifizieren des Bilds als einen Picasso](../images/app-prediction-01.png)

    <span data-ttu-id="c87d9-115">_Klassifizieren des Bilds als einen Picasso_</span><span class="sxs-lookup"><span data-stu-id="c87d9-115">_Classifying an image as a Picasso_</span></span> 

1. <span data-ttu-id="c87d9-116">Wiederholen Sie die Schritte 1 bis 3 für die Bilder **RembrandtTest_01.jpg** und **PollockTest_01.jpg**, und bestätigen Sie, dass die App Gemälde von Rembrandt und Pollock identifizieren kann.</span><span class="sxs-lookup"><span data-stu-id="c87d9-116">Repeat steps 1 through 3 for **RembrandtTest_01.jpg** and **PollockTest_01.jpg** and confirm that the app can identify paintings by Rembrandt and Pollock.</span></span>

    ![Klassifizieren des Bilds als einen Rembrandt](../images/app-prediction-02.png)

    <span data-ttu-id="c87d9-118">_Klassifizieren des Bilds als einen Rembrandt_</span><span class="sxs-lookup"><span data-stu-id="c87d9-118">_Classifying an image as a Rembrandt_</span></span> 

1. <span data-ttu-id="c87d9-119">Wiederholen Sie die Schritte 1 bis 3 für **VanGoghTest_01.png** und **VanGoghTest_02.png**, und bestätigen Sie, dass die App diese Meisterwerke von Van Gogh nicht als Gemälde von Picasso, Rembrandt oder Pollock identifiziert.</span><span class="sxs-lookup"><span data-stu-id="c87d9-119">Repeat steps 1 through 3 for **VanGoghTest_01.png** and **VanGoghTest_02.png** and confirm that the app does not identify these Van Gogh masterworks as paintings by Picasso, Rembrandt, or Pollock.</span></span>

    ![Kein Picasso, Rembrandt oder Pollock](../images/app-prediction-03.png)

    <span data-ttu-id="c87d9-121">_Kein Picasso, Rembrandt oder Pollock_</span><span class="sxs-lookup"><span data-stu-id="c87d9-121">_Not a Picasso, Rembrandt, or Pollock_</span></span> 

1. <span data-ttu-id="c87d9-122">Wie Sie sehen können, ist die Verwendung einer Vorhersage-API einer App genauso verlässlich wie das Custom Vision Service-Portal, aber es macht noch viel mehr Spaß.</span><span class="sxs-lookup"><span data-stu-id="c87d9-122">As you can see, using the Prediction API from an app is as reliable as through the Custom Vision Service portal — and way more fun!</span></span> <span data-ttu-id="c87d9-123">Wenn Sie dann noch zu den Vorhersageseiten im Portal navigieren, finden Sie jedes Bild, das über die App hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="c87d9-123">What's more, if you go to the Predictions page in the portal, you'll find each of the images uploaded via the app shown there as well.</span></span>
 
    ![Bild, das an den Custom Vision Service gesendet wurde](../images/portal-all-predictions.png)

    <span data-ttu-id="c87d9-125">_Bild, das an den Custom Vision Service gesendet wurde_</span><span class="sxs-lookup"><span data-stu-id="c87d9-125">_image submitted to the Custom Vision Service_</span></span> 

<span data-ttu-id="c87d9-126">Probieren Sie es einfach selbst mit eigenen Bildern aus, und beurteilen Sie die Erfahrenheit des Modells beim Identifizieren von Künstlern oder der Bestimmung, dass ein Bild keinen Picasso, Rembrandt oder Pollock darstellt.</span><span class="sxs-lookup"><span data-stu-id="c87d9-126">Feel free to test with images of your own and gauge the model's adeptness at identifying artists or determining that an image is not a Picasso, Rembrandt, or Pollock.</span></span> <span data-ttu-id="c87d9-127">Wenn Sie das Modell trainieren möchten, sodass es auch Van Goghs erkennt, laden Sie einige Gemälde von Van Gogh hoch, markieren Sie diese mit „Van Gogh“, und trainieren Sie das Modell weiter.</span><span class="sxs-lookup"><span data-stu-id="c87d9-127">If you'd like to train it to recognize Van Goghs, too, upload some Van Gogh paintings, tag them with "Van Gogh," and retrain the model.</span></span> <span data-ttu-id="c87d9-128">Der Intelligenz des Modells sind keine Grenzen gesetzt, wenn Sie bereit sind, es zu trainieren.</span><span class="sxs-lookup"><span data-stu-id="c87d9-128">There is no limit to the intelligence you can add if you're willing to do the training.</span></span> <span data-ttu-id="c87d9-129">Und denken Sie daran: je mehr Bilder Sie zum Trainieren zur Verfügung stellen, desto intelligenter wird das Modell.</span><span class="sxs-lookup"><span data-stu-id="c87d9-129">And remember that in general, the more images you train with, the smarter the model will be.</span></span>