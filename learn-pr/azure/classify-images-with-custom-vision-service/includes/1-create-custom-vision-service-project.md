### <a name="exercise-1-create-a-custom-vision-service-project"></a><span data-ttu-id="4904c-101">Übung 1: Erstellen eines Custom Vision Service-Projekts</span><span class="sxs-lookup"><span data-stu-id="4904c-101">Exercise 1: Create a Custom Vision Service project</span></span>

<span data-ttu-id="4904c-102">Wenn Sie mithilfe von Custom Vision Service ein Modell zur Bildklassifizierung erstellen möchten, müssen Sie in einem ersten Schritt ein Projekt erstellen.</span><span class="sxs-lookup"><span data-stu-id="4904c-102">The first step in building an image-classification model with the Custom Vision Service is to create a project.</span></span> <span data-ttu-id="4904c-103">In dieser Übung erfahren Sie, wie Sie das Custom Vision Service-Portal verwenden, um ein Custom Vision Service-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="4904c-103">In this exercise, you will use the Custom Vision Service portal to create a Custom Vision Service project.</span></span>

1. <span data-ttu-id="4904c-104">Öffnen Sie das [Custom Vision Service-Portal](https://www.customvision.ai/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="4904c-104">Open the [Custom Vision Service portal](https://www.customvision.ai/) in your browser.</span></span> <span data-ttu-id="4904c-105">Klicken Sie anschließend auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="4904c-105">Then click **Sign In**.</span></span> 
 
    ![Anmelden im Custom Vision Service-Portal](../images/portal-sign-in.png)

    <span data-ttu-id="4904c-107">_Anmelden im Custom Vision Service-Portal_</span><span class="sxs-lookup"><span data-stu-id="4904c-107">_Signing in to the Custom Vision Service portal_</span></span>

1. <span data-ttu-id="4904c-108">Wenn Sie aufgefordert werden, sich anzumelden, geben Sie die Anmeldeinformationen für Ihr Microsoft-Konto ein.</span><span class="sxs-lookup"><span data-stu-id="4904c-108">If you are asked to sign in, do so using the credentials for your Microsoft account.</span></span> <span data-ttu-id="4904c-109">Wenn Sie zustimmen sollen, dass diese App auf Ihre Daten zugreifen kann, klicken Sie auf **Ja**, und stimmen Sie den Vertragsbedingungen zu, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="4904c-109">If you are asked to let this app access your info, click **Yes**, and if prompted, agree to the terms of service.</span></span>

1. <span data-ttu-id="4904c-110">Klicken Sie auf **Neues Projekt**, um ein neues Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="4904c-110">Click **New Project** to create a new project.</span></span>
  
    ![Erstellen eines Custom Vision Service-Projekts](../images/portal-click-new-project.png)

    <span data-ttu-id="4904c-112">_Erstellen eines Custom Vision Service-Projekts_</span><span class="sxs-lookup"><span data-stu-id="4904c-112">_Creating a Custom Vision Service project_</span></span>

1. <span data-ttu-id="4904c-113">Geben Sie dem Projekt im Dialogfeld „Neues Projekt“ den Namen „Kunstwerke“, prüfen Sie, ob **Allgemein** als Domäne ausgewählt ist, und klicken Sie auf **Projekt erstellen**.</span><span class="sxs-lookup"><span data-stu-id="4904c-113">In the "New project" dialog, name the project "Artworks," ensure that **General** is selected as the domain, and click **Create project**.</span></span>

    > <span data-ttu-id="4904c-114">Domänen optimieren Modelle für bestimmte Bildtypen.</span><span class="sxs-lookup"><span data-stu-id="4904c-114">A domain optimizes a model for specific types of images.</span></span> <span data-ttu-id="4904c-115">Wenn Sie z.B. Bilder von Essen nach dargestellter Essensart oder nach Landesküche klassifizieren möchten, sollten Sie die Domäne „Essen“ auswählen.</span><span class="sxs-lookup"><span data-stu-id="4904c-115">For example, if your goal is to classify food images by the types of food they contain or the ethnicity of the dishes, then it might be helpful to select the Food domain.</span></span> <span data-ttu-id="4904c-116">In Szenarios, die nicht im Zusammenhang mit einer der angebotenen Domänen stehen, oder wenn Sie unsicher sind, welche Domäne die Richtige ist, wählen Sie die Domäne „Allgemein“ aus.</span><span class="sxs-lookup"><span data-stu-id="4904c-116">For scenarios that don't match any of the offered domains, or if you are unsure of which domain to choose, select the General domain.</span></span>

    ![Erstellen eines Custom Vision Service-Projekts](../images/portal-create-project.png)

    <span data-ttu-id="4904c-118">_Erstellen eines Custom Vision Service-Projekts_</span><span class="sxs-lookup"><span data-stu-id="4904c-118">_Creating a Custom Vision Service project_</span></span>

<span data-ttu-id="4904c-119">Laden Sie in einem nächsten Schritt Bilder in das Projekt, und weisen Sie diesen zur Klassifizierung Markierungen zu.</span><span class="sxs-lookup"><span data-stu-id="4904c-119">The next step is to upload images to the project and assign tags to those images to classify them.</span></span>