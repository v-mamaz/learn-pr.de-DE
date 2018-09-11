## <a name="train-your-first-deep-learning-model-using-pytorch-and-jupyter"></a><span data-ttu-id="71cee-101">Trainieren Ihres ersten Deep Learning-Modells mithilfe von PyTorch und Jupyter</span><span class="sxs-lookup"><span data-stu-id="71cee-101">Train your first deep learning model using PyTorch and Jupyter</span></span>

![PyTorch-Logo](../media/5-image1.PNG) 

<span data-ttu-id="71cee-103">Im Normalfall codieren Deep Learning-Techniker Matrixalgebraoperationen nicht durchgängig manuell.</span><span class="sxs-lookup"><span data-stu-id="71cee-103">Typically deep learning engineers do not hard code matrix algebra operations all by hand.</span></span> <span data-ttu-id="71cee-104">Stattdessen verwenden sie Frameworks, wie etwa PyTorch oder TensorFlow.</span><span class="sxs-lookup"><span data-stu-id="71cee-104">They instead use frameworks such as PyTorch or TensorFlow.</span></span>  

<span data-ttu-id="71cee-105">PyTorch ist ein Python-basiertes Framework, das Flexibilität als Entwicklungsplattform für Deep Learning bietet.</span><span class="sxs-lookup"><span data-stu-id="71cee-105">PyTorch is a python-based framework that provides flexibility as a deep learning development platform.</span></span> <span data-ttu-id="71cee-106">Der Workflow von PyTorch baut auf der wissenschaftlichen Computingbibliothek numpy von Python auf.</span><span class="sxs-lookup"><span data-stu-id="71cee-106">PyTorch's workflow is built on top of python scientific computing library numpy.</span></span> 

<span data-ttu-id="71cee-107">Sie fragen sich jetzt vielleicht, warum wir PyTorch zum Erstellen von Deep Learning-Modellen verwenden?</span><span class="sxs-lookup"><span data-stu-id="71cee-107">Now you might ask, why would we use PyTorch to build deep learning models?</span></span>  

- <span data-ttu-id="71cee-108">Einfach zu verwendende API – so einfach, wie Python nur sein kann.</span><span class="sxs-lookup"><span data-stu-id="71cee-108">Easy to use API – It's as simple as python can be.</span></span>
- <span data-ttu-id="71cee-109">Python-Unterstützung – PyTorch integriert sich reibungslos in den wissenschaftlichen Computingstapel.</span><span class="sxs-lookup"><span data-stu-id="71cee-109">Python support – PyTorch smoothly integrates with the scientific computing stack.</span></span>
- <span data-ttu-id="71cee-110">Dynamische Computergraphen – Anstelle vordefinierter Graphen mit bestimmter Funktionalität erstellt PyTorch Computergraphen dynamisch, die zur Laufzeit verändert werden können.</span><span class="sxs-lookup"><span data-stu-id="71cee-110">Dynamic computation graphs – Instead of predefined graphs with specific functionalities, PyTorch build computational graphs dynamically that can be modified during runtime.</span></span> <span data-ttu-id="71cee-111">Dynamische Computergraphen sind für die verschachtelte Batchverarbeitung und in Fällen nützlich, in denen der Speicherplatzbedarf zum Erstellen eines bestimmten Netzwerks unbekannt ist.</span><span class="sxs-lookup"><span data-stu-id="71cee-111">Dynamic computation graphs are valuable for nested batching and when we do not know how much memory will be needed for creating a given network.</span></span>

## <a name="run-your-first-pytorch-model"></a><span data-ttu-id="71cee-112">Ausführen Ihres ersten PyTorch-Modells</span><span class="sxs-lookup"><span data-stu-id="71cee-112">Run your first PyTorch model</span></span>

<span data-ttu-id="71cee-113">Navigieren Sie zum Jupyter Notebook, das Sie im letzten Kapitel eingerichtet haben.</span><span class="sxs-lookup"><span data-stu-id="71cee-113">Navigate to the Jupyter Notebook that you set up in the last chapter.</span></span>

- <span data-ttu-id="71cee-114">[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com:8888/?token={eintoken}</span><span class="sxs-lookup"><span data-stu-id="71cee-114">[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com:8888/?token={sometoken}</span></span>

<span data-ttu-id="71cee-115">Wählen Sie das Notebook first_pytorch_classifier.ipynb aus</span><span class="sxs-lookup"><span data-stu-id="71cee-115">Select the first_pytorch_classifier.ipynb notebook</span></span>

![Wählen Sie first_pytorch_classifier.ipynb aus](../media/5-image2.PNG)

<span data-ttu-id="71cee-117">Befolgen Sie die Anweisungen im Notebook, um Ihren ersten PyTorch-Klassifizierer zu trainieren.</span><span class="sxs-lookup"><span data-stu-id="71cee-117">Follow the instructions in the notebook to train your first PyTorch classifer.</span></span>

![Screenshot des Notebooks](../media/5-image3.PNG)
