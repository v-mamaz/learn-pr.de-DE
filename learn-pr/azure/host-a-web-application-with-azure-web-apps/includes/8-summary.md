<span data-ttu-id="bb5bc-101">Sie haben erfolgreich eine vollständig funktionsfähige Web-App mithilfe des Web-Apps-Features von Azure App Service erstellt und bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-101">You've successfully created and deployed a full-featured web application using the Web Apps feature of Azure App Service.</span></span>

<span data-ttu-id="bb5bc-102">App Service vereinfacht das Verwalten und Steuern Ihrer Web-App im Vergleich zu herkömmlichen Hostingoptionen.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-102">App Service simplifies managing and controlling your web app in comparison to traditional hosting options.</span></span> <span data-ttu-id="bb5bc-103">Mithilfe von Web-Apps können Sie die Zeit und den Aufwand reduzieren, den Sie mit dem Ausführen und Verwalten Ihrer Web-App verbringen, und erweiterte Cloudfeatures wie die automatische Skalierung und die Git-Integration bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-103">Web Apps can help you reduce the time and effort spent running and managing your web app, and provide advanced cloud features such as auto scaling and Git integration.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="bb5bc-104">Bereinigen von Ressourcen</span><span class="sxs-lookup"><span data-stu-id="bb5bc-104">Clean up resources</span></span>

<span data-ttu-id="bb5bc-105">Wenn Sie mit der Arbeit an dieser Anwendung fertig sind, können Sie die unten stehenden Schritte ausführen, um alle Ressourcen zu löschen, die Sie während dem Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-105">When you are done working with this application, you can follow the steps below to delete all resources created during the tutorial.</span></span>

<span data-ttu-id="bb5bc-106">Wie Sie wissen, steht eine Ressourcengruppe im Zusammenhang mit allen anderen Ressourcen, die erstellt wurden und mit der Web-App verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-106">As you know, a resource group associates all the other resources that are created and related to the web app.</span></span> <span data-ttu-id="bb5bc-107">Also können Sie „aufräumen“, indem Sie die Ressourcengruppe löschen, da dadurch alle in dieser Gruppe erstellten Ressourcen verschwinden.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-107">So, cleaning up after yourself on Azure is a matter of deleting the resource group, and hence, all the resources created under that group disappear.</span></span>

<span data-ttu-id="bb5bc-108">Im Folgenden erfahren Sie, wie Sie eine Ressourcengruppe mithilfe des Azure-Portals löschen:</span><span class="sxs-lookup"><span data-stu-id="bb5bc-108">Let's explore together how you can delete a resource group using the Azure portal:</span></span>

1. <span data-ttu-id="bb5bc-109">Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-109">Log in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="bb5bc-110">Suchen Sie auf der linken Seite des Dashboards nach dem Menüelement **Ressourcengruppen**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-110">Locate and click the **Resource groups** menu item on the left-side of the Dashboard.</span></span> <span data-ttu-id="bb5bc-111">Auf dem Blatt **Ressourcengruppen** werden alle Ressourcengruppen aufgelistet, die Sie im Azure-Portal erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-111">The **Resource groups** blade lists all the resource groups that you have created in the Azure portal.</span></span>

1. <span data-ttu-id="bb5bc-112">Suchen Sie nach dem Namen der Ressourcengruppe, die Sie in Einheit #2 erstellt haben, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-112">Locate and click the resource group name that you created in Unit #2.</span></span> <span data-ttu-id="bb5bc-113">Sie gelangen im Portal zum Blatt „Web-App“.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-113">The portal navigates you to the web app blade.</span></span>

    ![Ressourcengruppen](../media-draft/8-resource-groups.png)

1. <span data-ttu-id="bb5bc-115">Sie gelangen im Azure-Portal zum Blatt **Ressourcengruppe**.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-115">The Azure portal navigates you to the **Resource group** blade.</span></span> <span data-ttu-id="bb5bc-116">Dort finden Sie eine Liste aller Ressourcen, die Sie im Rahmen dieses Moduls in dieser Ressourcengruppe erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-116">There, you can see a list of all the resources that you've created during this module under this resource group.</span></span>

    ![Blatt „Ressourcengruppe“](../media-draft/8-resource-group-blade.png)

1. <span data-ttu-id="bb5bc-118">Klicken Sie anschließend ganz oben auf dem Blatt auf **Ressourcengruppe löschen**.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-118">Locate and click on the **Delete resource group** link at the top of the blade.</span></span>

1. <span data-ttu-id="bb5bc-119">Azure stellt sicher, dass Sie diese Ressourcengruppe wirklich löschen möchten, indem Sie dazu aufgefordert werden, den Namen der Ressourcengruppe einzugeben.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-119">Azure verifies that you really want to delete this resource group by asking you to type the name of it.</span></span> <span data-ttu-id="bb5bc-120">Geben Sie den Namen der Ressourcengruppe ein, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-120">To proceed, type the name of the resource group.</span></span>

    ![Bestätigung zum Löschen der Ressourcengruppe](../media-draft/8-resource-group-delete.png)

1. <span data-ttu-id="bb5bc-122">Klicken Sie ganz unten auf dem Bestätigungsfenster auf die Schaltfläche **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-122">Locate and click on the **Delete** button at the bottom of the confirmation window.</span></span>

1. <span data-ttu-id="bb5bc-123">Azure benötigt einige Sekunden, um die Ressourcengruppe und alle zugehörigen Ressourcen zu löschen.</span><span class="sxs-lookup"><span data-stu-id="bb5bc-123">Azure takes a few seconds to wipe out the resource group and all the related resources.</span></span>
