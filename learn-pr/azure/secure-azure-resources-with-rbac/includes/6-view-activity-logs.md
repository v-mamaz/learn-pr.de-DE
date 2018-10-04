<span data-ttu-id="8c120-101">Aus Gründen der Überwachung und Problembehandlung bewertet First Up Consultants vierteljährlich Änderungen der rollenbasierten Zugriffssteuerung (RBAC).</span><span class="sxs-lookup"><span data-stu-id="8c120-101">First Up Consultants reviews role-based access control (RBAC) changes quarterly for auditing and troubleshooting purposes.</span></span> <span data-ttu-id="8c120-102">Sie wissen, dass Änderungen im [Azure-Aktivitätsprotokoll](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) protokolliert werden.</span><span class="sxs-lookup"><span data-stu-id="8c120-102">You know that changes get logged in [Azure Activity Log](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</span></span> <span data-ttu-id="8c120-103">Ihr Vorgesetzter hat Sie gebeten, einen Bericht über die Rollenzuweisung und Änderungen der benutzerdefinierten Rollen des letzten Monats zu generieren.</span><span class="sxs-lookup"><span data-stu-id="8c120-103">Your manager has asked if you can generate a report of the role assignment and custom role changes for the last month.</span></span>

## <a name="view-activity-logs"></a><span data-ttu-id="8c120-104">Anzeigen von Aktivitätsprotokollen</span><span class="sxs-lookup"><span data-stu-id="8c120-104">View activity logs</span></span>

<span data-ttu-id="8c120-105">Der einfachste Einstieg besteht im Anzeigen der Aktivitätsprotokolle im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="8c120-105">The easiest way to get started is to view the activity logs with the Azure portal.</span></span>

1. <span data-ttu-id="8c120-106">Klicken Sie auf **Alle Dienste**, und suchen Sie dann **Aktivitätsprotokoll**.</span><span class="sxs-lookup"><span data-stu-id="8c120-106">Click **All services** and then find **Activity log**.</span></span>

    ![Aktivitätsprotokolle im Portal](../media/6-all-services-activity-log.png)

1. <span data-ttu-id="8c120-108">Klicken Sie auf **Aktivitätsprotokoll**, um dieses zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="8c120-108">Click **Activity log** to open the activity log.</span></span>

    ![Aktivitätsprotokolle im Portal](../media/6-activity-log-portal.png)

1. <span data-ttu-id="8c120-110">Legen Sie den Filter **TimeSpan** (Zeitraum) auf **Letzter Monat** fest.</span><span class="sxs-lookup"><span data-stu-id="8c120-110">Set the **Timespan** filter to **Last month**.</span></span>

1. <span data-ttu-id="8c120-111">Geben Sie im Filter **Vorgang** zum Filtern der Liste **Rolle** ein.</span><span class="sxs-lookup"><span data-stu-id="8c120-111">Add an **Operation** filter and type **role** to filter the list.</span></span>

1. <span data-ttu-id="8c120-112">Wählen Sie die folgenden RBAC-Vorgänge aus:</span><span class="sxs-lookup"><span data-stu-id="8c120-112">Select the following RBAC operations:</span></span>

    - <span data-ttu-id="8c120-113">Rollenzuweisung erstellen (roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="8c120-113">Create role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="8c120-114">Rollenzuweisung löschen (roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="8c120-114">Delete role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="8c120-115">Benutzerdefinierte Rollendefinition erstellen oder aktualisieren (roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="8c120-115">Create or update custom role definition (roleDefinitions)</span></span>
    - <span data-ttu-id="8c120-116">Benutzerdefinierte Rollendefinition löschen (roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="8c120-116">Delete custom role definition (roleDefinitions)</span></span>

    ![Filter „Vorgang“](../media/6-operation-filter.png)

    <span data-ttu-id="8c120-118">Nach wenigen Augenblicken werden alle Vorgänge für Rollenzuweisungen und Rollendefinitionen des letzten Monats angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8c120-118">After a few moments, you'll see all the role assignment and role definition operations for the last month.</span></span> <span data-ttu-id="8c120-119">Darüber hinaus ist ein Link enthalten, über den das Aktivitätsprotokoll als CSV-Datei heruntergeladen werden kann.</span><span class="sxs-lookup"><span data-stu-id="8c120-119">It also includes a link to download the activity log as a CSV file.</span></span>

<span data-ttu-id="8c120-120">In dieser Einheit haben Sie gelernt, wie Sie das Azure-Aktivitätsprotokoll zum Auflisten von RBAC-Änderungen im Portal verwenden können und wie Sie einen einfachen Bericht generieren.</span><span class="sxs-lookup"><span data-stu-id="8c120-120">In this unit, you learned how to use Azure Activity Log to list RBAC changes in the portal and generate a simple report.</span></span>