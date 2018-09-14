<span data-ttu-id="22f28-101">Aus Gründen der Überwachung und Problembehandlung bewertet First Up Consultants vierteljährlich Änderungen der rollenbasierten Zugriffssteuerung (RBAC).</span><span class="sxs-lookup"><span data-stu-id="22f28-101">First Up Consultants reviews role-based access control (RBAC) changes quarterly for auditing and troubleshooting purposes.</span></span> <span data-ttu-id="22f28-102">Sie wissen, dass Änderungen im [Azure-Aktivitätsprotokoll](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) protokolliert werden.</span><span class="sxs-lookup"><span data-stu-id="22f28-102">You know that changes get logged in [Azure Activity Log](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</span></span> <span data-ttu-id="22f28-103">Ihr Vorgesetzter hat Sie gebeten, einen Bericht über die Rollenzuweisung und Änderungen der benutzerdefinierten Rollen des letzten Monats zu generieren.</span><span class="sxs-lookup"><span data-stu-id="22f28-103">Your manager has asked if you can generate a report of the role assignment and custom role changes for the last month.</span></span>

## <a name="view-activity-logs"></a><span data-ttu-id="22f28-104">Anzeigen von Aktivitätsprotokollen</span><span class="sxs-lookup"><span data-stu-id="22f28-104">View activity logs</span></span>

<span data-ttu-id="22f28-105">Der einfachste Einstieg besteht im Anzeigen der Aktivitätsprotokolle im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="22f28-105">The easiest way to get started is to view the activity logs with the Azure portal.</span></span>

1. <span data-ttu-id="22f28-106">Klicken Sie auf **Alle Dienste**, und suchen Sie dann **Aktivitätsprotokoll**.</span><span class="sxs-lookup"><span data-stu-id="22f28-106">Click **All services** and then find **Activity log**.</span></span>

    ![Aktivitätsprotokolle im Portal](../media-draft/7-all-services-activity-log.png)

1. <span data-ttu-id="22f28-108">Klicken Sie auf **Aktivitätsprotokoll**.</span><span class="sxs-lookup"><span data-stu-id="22f28-108">Click **Activity log**.</span></span>

    ![Aktivitätsprotokolle im Portal](../media-draft/7-activity-log-portal.png)

1. <span data-ttu-id="22f28-110">Legen Sie den Filter **TimeSpan** (Zeitraum) auf **Letzten Monat** fest.</span><span class="sxs-lookup"><span data-stu-id="22f28-110">Set the **Timespan** filter to **Last month**.</span></span>

1. <span data-ttu-id="22f28-111">Legen Sie den Filter **Ereigniskategorie** auf **Administrativ** fest.</span><span class="sxs-lookup"><span data-stu-id="22f28-111">Set the **Event category** filter to **Administrative**.</span></span>

1. <span data-ttu-id="22f28-112">Geben Sie **Rolle** im Filter **Vorgang** ein, um die Liste zu filtern.</span><span class="sxs-lookup"><span data-stu-id="22f28-112">In the **Operation** filter, type **role** to filter the list.</span></span>

1. <span data-ttu-id="22f28-113">Wählen Sie die folgenden RBAC-Vorgänge aus:</span><span class="sxs-lookup"><span data-stu-id="22f28-113">Select the following RBAC operations:</span></span>

    - <span data-ttu-id="22f28-114">Rollenzuweisung erstellen (roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="22f28-114">Create role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="22f28-115">Rollenzuweisung löschen (roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="22f28-115">Delete role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="22f28-116">Benutzerdefinierte Rollendefinition erstellen oder aktualisieren (roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="22f28-116">Create or update custom role definition (roleDefinitions)</span></span>
    - <span data-ttu-id="22f28-117">Benutzerdefinierte Rollendefinition löschen (roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="22f28-117">Delete custom role definition (roleDefinitions)</span></span>

    ![Filter „Vorgang“](../media-draft/7-operation-filter.png)

1. <span data-ttu-id="22f28-119">Klicken Sie auf **Anwenden**, um Ihre Filter anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="22f28-119">Click **Apply** to apply your filters.</span></span>

    <span data-ttu-id="22f28-120">Alle Vorgänge für Rollenzuweisung und Rollendefinition des letzten Monats werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="22f28-120">You'll see all the role assignment and role definition operations for the last month.</span></span> <span data-ttu-id="22f28-121">Außerdem ist ein Link enthalten, um das Aktivitätsprotokoll als CSV-Datei herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="22f28-121">It also includes a link to download the activity log as a CSV file.</span></span>

    ![RBAC-Aktivitätsprotokolle](../media-draft/7-activity-log-portal-filter.png)

## <a name="end-lab"></a><span data-ttu-id="22f28-123">Aufgabe beenden</span><span class="sxs-lookup"><span data-stu-id="22f28-123">End lab</span></span>

1. <span data-ttu-id="22f28-124">Um die Aufgabe zu beenden, klicken Sie auf das Hamburger-Menü in der oberen rechten Ecke dieses Fensters, und klicken Sie dann auf **Beenden**.</span><span class="sxs-lookup"><span data-stu-id="22f28-124">To end the lab, click the hamburger menu in the upper-right corner of this window and then click **End**.</span></span>

1. <span data-ttu-id="22f28-125">Klicken Sie auf **Ja, Aufgabe beenden**.</span><span class="sxs-lookup"><span data-stu-id="22f28-125">Click **Yes, end my lab**.</span></span>

## <a name="summary"></a><span data-ttu-id="22f28-126">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="22f28-126">Summary</span></span>

<span data-ttu-id="22f28-127">In dieser Einheit haben Sie gelernt, wie Sie Azure-Aktivitätsprotokoll zum Auflisten von RBAC-Änderungen im Portal verwenden können und wie Sie einen einfachen Bericht generieren.</span><span class="sxs-lookup"><span data-stu-id="22f28-127">In this unit, you learned how to use Azure Activity Log to list RBAC changes in the portal and generate a simple report.</span></span>
