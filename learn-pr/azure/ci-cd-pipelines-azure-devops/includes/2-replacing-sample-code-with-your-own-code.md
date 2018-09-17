<span data-ttu-id="ce207-101">Nach der Erstellung eines Azure DevOps-Projekts stellt sich natürlich die Frage, wie sich die Beispiel-App durch eine eigene App ersetzen lässt.</span><span class="sxs-lookup"><span data-stu-id="ce207-101">After creating an Azure DevOps project, the first thing everyone ask is how do you replace the sample app with your own app?</span></span> <span data-ttu-id="ce207-102">In dieser Einheit lernen Sie zwei einfache Methoden dafür kennen.</span><span class="sxs-lookup"><span data-stu-id="ce207-102">It's quite simple and in this unit, you will learn two ways to do it.</span></span>

1. <span data-ttu-id="ce207-103">Ersetzen des Codes im VSTS-Git-Repository durch Ihren eigenen Code</span><span class="sxs-lookup"><span data-stu-id="ce207-103">Replacing the code in the VSTS git repository with your real code</span></span>

2. <span data-ttu-id="ce207-104">Verweisen Ihrer Buildpipeline auf ein externes Git-Repository mit Ihrem eigenen Code</span><span class="sxs-lookup"><span data-stu-id="ce207-104">Pointing your build pipeline to an external git repo holding your real code</span></span>

## <a name="replacing-code-in-vsts-git-repository"></a><span data-ttu-id="ce207-105">Ersetzen des Codes im VSTS-Git-Repository</span><span class="sxs-lookup"><span data-stu-id="ce207-105">Replacing code in VSTS git repository</span></span>

<span data-ttu-id="ce207-106">Eine Möglichkeit besteht darin, einfach das Git-Repository in VSTS auf Ihrer Festplatte zu klonen, alles durch Ihren eigenen Code zu ersetzen und es anschließend wieder in VSTS hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="ce207-106">One simple way is by cloning the git repo in VSTS onto your hard drive, replacing everything with your own code, uploading back to VSTS and voila.</span></span> <span data-ttu-id="ce207-107">Daraufhin wird Ihr Code über die CI/CD-Pipeline erstellt und bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="ce207-107">Your code will now be built and deployed through the CI/CD pipeline.</span></span>

<span data-ttu-id="ce207-108">In dieser Einheit laden Sie zunächst den Quellcode der Node.js-App herunter und speichern ihn auf Ihrer Festplatte.</span><span class="sxs-lookup"><span data-stu-id="ce207-108">For this unit, you will start by downloading and storing the source code to the node.js app onto your hard drive.</span></span>

1. <span data-ttu-id="ce207-109">Herunterladen des Quellcodes von <https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip></span><span class="sxs-lookup"><span data-stu-id="ce207-109">Download the source code from <https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip></span></span>

2. <span data-ttu-id="ce207-110">Extrahieren Sie den Inhalt von „MicrosoftLearnDevOps.zip“ an einem beliebigen Ort auf Ihrer Festplatte.</span><span class="sxs-lookup"><span data-stu-id="ce207-110">Extract the contents of MicrosoftLearnDevOps.zip somewhere on your hard drive.</span></span> <span data-ttu-id="ce207-111">In diesem Beispiel wurde `C:\users\abel\Downloads\MicrosoftLearnDevOps` verwendet.</span><span class="sxs-lookup"><span data-stu-id="ce207-111">For this example `C:\users\abel\Downloads\MicrosoftLearnDevOps` was used</span></span>  
<span data-ttu-id="ce207-112">![Entzipptes Verzeichnis](/media-draft/2-unzippedfolder.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-112">![Unzipped Directory](/media-draft/2-unzippedfolder.png)</span></span>

<span data-ttu-id="ce207-113">Als Nächstes müssen Sie das Repository auf Ihrer Festplatte klonen und die Beispiel-App durch Ihre eigene Node.js-App ersetzen.</span><span class="sxs-lookup"><span data-stu-id="ce207-113">Next, you need to clone the repo onto your hard drive and replace the sample app with the real node.js app.</span></span> <span data-ttu-id="ce207-114">In dieser Einheit wird davon ausgegangen, dass Git bereits auf Ihrem Computer installiert ist.</span><span class="sxs-lookup"><span data-stu-id="ce207-114">This unit assumes you already have git installed on your computer.</span></span>

1. <span data-ttu-id="ce207-115">Navigieren Sie im Azure-Portal zu Ihrem Azure DevOps-Projekt, und klicken Sie auf den Link zum Coderepository.</span><span class="sxs-lookup"><span data-stu-id="ce207-115">From Azure portal browse to your Azure DevOps Project and click on the code repository link.</span></span>  
![](/media-draft/2-browsetorepolink.png)

2. <span data-ttu-id="ce207-116">Klicken Sie auf „Klonen“, und kopieren Sie die URL für das Git-Repository (in der rechten oberen Ecke).</span><span class="sxs-lookup"><span data-stu-id="ce207-116">Click on Clone and copy the url for the git repo in the upper right-hand side.</span></span>  
![Kopieren der Klon-URL](/media-draft/2-copycloneurl.png)  
<span data-ttu-id="ce207-118">Daraufhin wird die Repository-URL in die Zwischenablage kopiert.</span><span class="sxs-lookup"><span data-stu-id="ce207-118">This will copy the repo url to your clipboard</span></span>

3. <span data-ttu-id="ce207-119">Klonen des Repositorys auf Ihrer Festplatte</span><span class="sxs-lookup"><span data-stu-id="ce207-119">Clone the repo to your hard drive</span></span>  
![Git Clone](/media-draft/2-gitclone.png)  
<span data-ttu-id="ce207-121">In diesem Beispiel wurde das Repository in „C:\Users\abel\Source\TripleCrown\DevOps“ geklont.</span><span class="sxs-lookup"><span data-stu-id="ce207-121">In this example the repo was cloned to C:\Users\abel\Source\TripleCrown\DevOps</span></span>

4. <span data-ttu-id="ce207-122">Löschen Sie alles aus Ihrem lokalen Repository (mit Ausnahme des Verzeichnisses `.git`).</span><span class="sxs-lookup"><span data-stu-id="ce207-122">Delete everything from your local repo except for the `.git` directory</span></span>  
<span data-ttu-id="ce207-123">![Löschen aller Inhalte aus dem Repository](/media-draft/2-deleterepoofeverything.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-123">![Delete Repo of Everything](/media-draft/2-deleterepoofeverything.png)</span></span>

5. <span data-ttu-id="ce207-124">Kopieren Sie den Quellcode für die heruntergeladene Node.js-App in den Repositoryordner.</span><span class="sxs-lookup"><span data-stu-id="ce207-124">Copy the source code for the downloaded node.js app into the repo folder</span></span>  
![Ersetzter Code](/media-draft/2-replacedeverything.png)

6. <span data-ttu-id="ce207-126">Fügen Sie Ihrem lokalen Repository sämtliche Änderungen hinzu, indem Sie `git add *` über die Befehlszeile eingeben.</span><span class="sxs-lookup"><span data-stu-id="ce207-126">Add all the changes to your local repo by typing `git add *` from the command line</span></span>  
<span data-ttu-id="ce207-127">![Git: Alles hinzufügen](/media-draft/2-gitaddall.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-127">![Git Add All](/media-draft/2-gitaddall.png)</span></span>

7. <span data-ttu-id="ce207-128">Geben Sie `git commit -m "replace sample app with real code"` ein, um die Änderungen an Ihrem lokalen Repository zu committen.</span><span class="sxs-lookup"><span data-stu-id="ce207-128">Commit changes to your local repo by typing `git commit -m "replace sample app with real code"`</span></span>  
<span data-ttu-id="ce207-129">![Git: Committen](/media-draft/2-gitcommit.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-129">![Git Commit](/media-draft/2-gitcommit.png)</span></span>

8. <span data-ttu-id="ce207-130">Pushen Sie Änderungen mithilfe von `git push` wieder an das Git-Repository in VSTS.</span><span class="sxs-lookup"><span data-stu-id="ce207-130">Push changes back to the git repo in VSTS with `git push`</span></span>  
<span data-ttu-id="ce207-131">![Git: Pushen](/media-draft/2-gitpush.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-131">![Git Push](/media-draft/2-gitpush.png)</span></span>

9. <span data-ttu-id="ce207-132">Nach dem Pushen der Änderungen an VSTS sollte der Code Ihrer eigenen App den Buildvorgang durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="ce207-132">After pushing changes back to VSTS, this should send the real app code through the build</span></span>  
<span data-ttu-id="ce207-133">![Buildvorgang gestartet](/media-draft/2-buildkickedoff.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-133">![Build Kicked Off](/media-draft/2-buildkickedoff.png)</span></span>  
<span data-ttu-id="ce207-134">![Buildvorgang in Aktion](/media-draft/2-buildinaction.png) und Releasepipeline bis Azure</span><span class="sxs-lookup"><span data-stu-id="ce207-134">![Build in Action](/media-draft/2-buildinaction.png) and release pipeline all the way to azure</span></span>  
 <span data-ttu-id="ce207-135">![Releasevorgang](/media-draft/2-releaserunning.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-135">![Release Running](/media-draft/2-releaserunning.png)</span></span>

 <span data-ttu-id="ce207-136">Nach Abschluss der Bereitstellung können Sie sich im Azure-Portal vergewissern, dass Ihre eigene App bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="ce207-136">After the deployment finishes, you can verify the real app was deployed by going back to the Azure portal</span></span>

 1. <span data-ttu-id="ce207-137">Navigieren Sie im Azure-Portal zu Ihrem Azure DevOps-Projekt, und klicken Sie auf der rechten Seite auf Ihre bereitgestellte App.</span><span class="sxs-lookup"><span data-stu-id="ce207-137">Go to the Azure portal, browse to your Azure DevOps project, and click on your deployed app on the right-hand side</span></span>  
 ![Link zum Starten der Beispiel-App](/media-draft/2-launchapp.png)

 2. <span data-ttu-id="ce207-139">Daraufhin wird die ausgeführte App in Ihrem Browser gestartet.</span><span class="sxs-lookup"><span data-stu-id="ce207-139">This launches the running app in your browser</span></span>  
 ![Ausgeführte App](/media-draft/2-apprunning.png)

## <a name="using-external-git-repo"></a><span data-ttu-id="ce207-141">Verwenden eines externen Git-Repositorys</span><span class="sxs-lookup"><span data-stu-id="ce207-141">Using external git repo</span></span>

<span data-ttu-id="ce207-142">Eine weitere Möglichkeit, die Beispiel-App durch Ihren eigenen App-Code zu ersetzen, besteht darin, die Buildpipeline auf ein externes Git-Repository mit Ihrem App-Code zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="ce207-142">Another way to swap out the sample app with your real app code is by pointing the build pipeline to an external git repository that holds your app code.</span></span> <span data-ttu-id="ce207-143">In diesem Beispiel laden Sie Ihren eigenen App-Code in ein GitHub-Repository hoch.</span><span class="sxs-lookup"><span data-stu-id="ce207-143">For this example, upload the real app code to a github repository.</span></span>

<span data-ttu-id="ce207-144">Gehen Sie anschließend wie folgt vor, um die Buildpipeline auf dieses GitHub-Repository zu verweisen:</span><span class="sxs-lookup"><span data-stu-id="ce207-144">After uploading the real code to github, do the following to point the build pipeline to this github repository</span></span>

1. <span data-ttu-id="ce207-145">Navigieren Sie im Azure-Portal zu Ihrem Azure DevOps-Projekt, und klicken Sie auf den Build-Link.</span><span class="sxs-lookup"><span data-stu-id="ce207-145">From the Azure portal, browse to your Azure DevOps project and click on the build link</span></span>  
![Build-Link](/media-draft/2-buildlink.png)

2. <span data-ttu-id="ce207-147">Dadurch gelangen Sie zu den Buildpipelines. Klicken Sie dort auf Ihre Buildpipeline und anschließend auf `Edit`.</span><span class="sxs-lookup"><span data-stu-id="ce207-147">This takes you to the build pipelines, click your build pipeline and then `Edit`</span></span>  
<span data-ttu-id="ce207-148">![Klicken auf „Build bearbeiten“](/media-draft/2-clickeditbuildlink.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-148">![Click Edit Build](/media-draft/2-clickeditbuildlink.png)</span></span>

3. <span data-ttu-id="ce207-149">Dadurch gelangen Sie zum Build-Editor. Klicken Sie auf `Get sources`.</span><span class="sxs-lookup"><span data-stu-id="ce207-149">This takes you to the build editor, click on `Get sources`</span></span>  
<span data-ttu-id="ce207-150">![Klicken auf „Get sources“ (Quellen abrufen)](/media-draft/2-clickgetsource.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-150">![Click Get Source](/media-draft/2-clickgetsource.png)</span></span>

4. <span data-ttu-id="ce207-151">Dadurch gelangen Sie zur Seite zum Auswählen einer Quelle.</span><span class="sxs-lookup"><span data-stu-id="ce207-151">This takes you to the Select a source page.</span></span> <span data-ttu-id="ce207-152">Beachten Sie, dass Sie für die Buildpipeline nicht nur VSTS-Git, sondern auch GitHub, GitHub Enterprise, Subversion, Bitbucket Cloud sowie jedes andere externe Repository auf Git-Basis verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ce207-152">Notice how you can not only use VSTS Git, but also GitHub, GitHub Enterprise, Subversion, Bitbucket Cloud, and any external Git based repo for the build pipeline.</span></span> <span data-ttu-id="ce207-153">Wählen Sie für diese Übung „GitHub“ aus.</span><span class="sxs-lookup"><span data-stu-id="ce207-153">For this exercise, select GitHub</span></span>  
![Auswählen von GitHub](/media-draft/2-selectgithub.png)

5. <span data-ttu-id="ce207-155">Dadurch gelangen Sie zur GitHub-Verbindungsseite.</span><span class="sxs-lookup"><span data-stu-id="ce207-155">This takes you to the GitHub connection page.</span></span> <span data-ttu-id="ce207-156">Verwenden Sie entweder OAuth oder ein persönliches Zugriffstoken, um eine Verbindung mit Ihrem GitHub-Konto herzustellen.</span><span class="sxs-lookup"><span data-stu-id="ce207-156">Either use OAuth or a Personal Access Token to connect with your GitHub account</span></span>

6. <span data-ttu-id="ce207-157">Wählen Sie das GitHub-Repository mit Ihrem eigenen App-Code aus, und klicken Sie auf `Save & queue`.</span><span class="sxs-lookup"><span data-stu-id="ce207-157">Select the github repo holding the real app code and click `Save & queue`</span></span>  
<span data-ttu-id="ce207-158">![Speichern und in Warteschlange einreihen](/media-draft/2-saveandqueue.png)</span><span class="sxs-lookup"><span data-stu-id="ce207-158">![Save and Queue](/media-draft/2-saveandqueue.png)</span></span>

7. <span data-ttu-id="ce207-159">Klicken Sie auf die Schaltfläche `Save & queue`.</span><span class="sxs-lookup"><span data-stu-id="ce207-159">Click the `Save & queue` button</span></span>  
![](/media-draft/2-saveandqueuedialog.png)

8. <span data-ttu-id="ce207-160">Daraufhin wird ein Speichervorgang ausgeführt und der Buildvorgang gestartet, sodass Ihr eigener, in GitHub gehosteter App-Code unsere Build- und Releasepipelines bis Azure durchläuft.</span><span class="sxs-lookup"><span data-stu-id="ce207-160">This action saves and kicks off the build, sending the real app code hosted in GitHub through our build and release pipelines all the way to Azure</span></span>  
![Ausgeführter Buildvorgang](/media-draft/2-buildrunning.png)

## <a name="summary"></a><span data-ttu-id="ce207-162">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="ce207-162">Summary</span></span>

<span data-ttu-id="ce207-163">In dieser Einheit haben Sie zwei Möglichkeiten kennengelernt, um den Beispielcode des DevOps-Projekts durch eigenen App-Code zu ersetzen:</span><span class="sxs-lookup"><span data-stu-id="ce207-163">In this unit, you learned two different ways to replace the sample code in the DevOps project with real app code.</span></span> <span data-ttu-id="ce207-164">Sie können entweder den Code im VSTS-Git-Repository ersetzen oder die Buildpipeline mit einem anderen externen Repository verknüpfen, in dem sich Ihr App-Code befindet.</span><span class="sxs-lookup"><span data-stu-id="ce207-164">This can be done either by replacing the code in the VSTS git repo, or by linking the build pipeline with another external repo which holds your app code.</span></span>

<span data-ttu-id="ce207-165">Als Nächstes erfahren Sie, wie Sie die Build- und Releasepipelines anpassen.</span><span class="sxs-lookup"><span data-stu-id="ce207-165">Next learn how to customize the build and release pipelines.</span></span>