Angenommen, Sie müssen für die Entwicklungs-, Technik- und Marketingteams den Zugriff auf Ressourcen in Azure verwalten. Nun erhalten Sie Zugriffsanforderungen und müssen in kurzer Zeit lernen, wie Zugriffe auf Azure-Ressourcen verwaltet werden.

## <a name="what-is-rbac"></a>Was ist die RBAC?

Bei der rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) handelt es sich um ein Autorisierungssystem, das auf Azure Resource Manager basiert und eine differenzierte Verwaltung des Zugriffs auf Ressourcen in Azure ermöglicht. Azure bietet viele Ressourcen, z.B. VMs, Websites, Netzwerke und Speicher.

#### <a name="what-is-role-based-access-control"></a>Was ist die rollenbasierte Zugriffssteuerung?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvk]

## <a name="what-can-i-do-with-rbac"></a>Welche Möglichkeiten bietet RBAC?

Mit RBAC können Sie Zugriff auf Azure-Ressourcen gewähren, für die Sie verantwortlich sind.

Hier einige Beispiele:

- Ein Benutzer kann virtuelle Computer in einem Abonnement verwalten, während ein anderer Benutzer virtuelle Netzwerke verwalten kann
- Eine Datenbankadministratorgruppe kann SQL-Datenbanken in einem Abonnement verwalten
- Ein Benutzer kann sämtliche Ressourcen in einer Ressourcengruppe verwalten, wie z.B. virtuelle Computer, Websites und Subnetze
- Eine Anwendung kann auf sämtliche Ressourcen in einer Ressourcengruppe zugreifen

## <a name="rbac-in-the-azure-portal"></a>RBAC im Azure-Portal

Im Azure-Portal wird in verschiedenen Bereichen ein Blatt mit dem Namen **Zugriffssteuerung (IAM)** (dentity & Access Management, Identitäts- und Zugriffsverwaltung) angezeigt. Auf diesem Blatt werden die Benutzer mit Zugriff auf diesen Bereich sowie deren Rollen angezeigt. Über dieses Blatt können Sie Zugriff gewähren oder den Zugriff aufheben.

Im Folgenden sehen Sie ein Beispiel für das Blatt „Zugriffssteuerung (IAM)“ für eine Ressourcengruppe. In diesem Beispiel wurde Alain Charon die Rolle „Sicherungsoperator“ für diese Ressourcengruppe zugewiesen.

![„Zugriffssteuerung (IAM)“ im Azure-Portal](../media/2-resource-group-access-control.png)

## <a name="how-does-rbac-work"></a>Funktionsweise von RBAC

Den Zugriff auf Ressourcen steuern Sie mit RBAC, indem Sie Rollenzuweisungen erstellen, mit denen die Durchsetzung von Berechtigungen gesteuert wird. Zum Erstellen einer Rollenzuweisung sind drei Elemente erforderlich: ein Sicherheitsprinzipal, eine Rollendefinition und ein Bereich. Nach diesen drei Elementen können Sie mit „wer“, „was“ und „wo“ fragen.

### <a name="1-security-principal-who"></a>1. Sicherheitsprinzipal (wer)

Ein *Sicherheitsprinzipal* ist nur ein ausgefallener Name für einen Benutzer, eine Gruppe oder eine Anwendung, auf den bzw. die Sie Zugriff gewähren möchten.

![Abbildung: Sicherheitsprinzipal mit Benutzer, Gruppe und Dienstprinzipal.](../media/2-rbac-security-principal.png)

### <a name="2-role-definition-what-you-can-do"></a>2. Rollendefinition (was Sie tun können)

Eine *Rollendefinition* ist eine Sammlung von Berechtigungen. Gelegentlich wird sie auch einfach als Rolle bezeichnet. In einer Rollendefinition sind die Berechtigungen wie etwa Lesen, Schreiben und Löschen aufgelistet. Rollen können auf allgemeiner Ebene erteilt werden (z.B. Besitzer) oder spezifisch sein (z.B. Mitwirkender für virtuelle Computer).

![Abbildung: Auflistung verschiedener integrierter und benutzerdefinierter Rollen mit vergrößerter Definition für die Rolle des Mitwirkenden](../media/2-rbac-role-definition.png)

Azure umfasst mehrere integrierte Rollen, die Sie verwenden können. Im Folgenden werden vier grundlegende integrierte Rollen aufgeführt:

- Besitzer: Verfügen über vollständigen Zugriff auf alle Ressourcen, einschließlich des Rechts, den Zugriff an andere Personen zu delegieren.
- Mitwirkende: Können alle Arten von Azure-Ressourcen erstellen und verwalten, aber keinen anderen Personen Zugriff gewähren.
- Leser: Können vorhandene Azure-Ressourcen anzeigen.
- Benutzerzugriffsadministratoren: Können den Benutzerzugriff auf Azure-Ressourcen verwalten.

Wenn die integrierten Rollen den besonderen Ansprüchen Ihrer Organisation nicht genügen, können Sie Ihre eigenen benutzerdefinierten Rollen erstellen.

### <a name="3-scope-where"></a>3. Bereich (wo)

*Bereich* ist der Ort, für den die Zugriffsberechtigung gilt. Dies ist hilfreich, wenn Sie einem Benutzer die Rolle „Mitwirkender von Website“ zuweisen möchten, jedoch nur für eine Ressourcengruppe.

In Azure können Sie auf mehreren Ebenen einen Bereich angeben: Verwaltungsgruppe, Abonnement, Ressourcengruppe oder Ressource. Bereiche sind in einer Beziehung zwischen über- und untergeordneten Elementen strukturiert. Wenn Sie den Zugriff in einem übergeordneten Bereich gewähren, werden diese Berechtigungen vom untergeordneten Bereich übernommen. Wenn Sie beispielsweise einer Gruppe im Abonnementbereich die Rolle „Mitwirkender“ zuweisen, wird diese Rolle von allen Ressourcengruppen und Ressourcen im Abonnement übernommen.

![Abbildung: hierarchische Darstellung verschiedener Azure-Ebenen für den Gültigkeitsbereich Die Hierarchie weist, beginnend mit der höchsten Ebene, folgende Reihenfolge auf: Verwaltungsgruppe, Abonnement, Ressourcengruppe und Ressource.](../media/2-rbac-scope.png)

### <a name="role-assignment"></a>Rollenzuweisung

Nachdem Sie wer, was und wo bestimmt haben, können Sie diese Elemente vereinen, um Zugriff zu gewähren. Eine *Rollenzuweisung* ist der Prozess, in dem eine Rolle zum Zwecke der Zugriffserteilung in einem bestimmten Bereich an einen Sicherheitsprinzipal gebunden wird. Erstellen Sie zum Gewähren des Zugriffs eine Rollenzuweisung. Entfernen Sie zum Widerrufen des Zugriffs eine Rollenzuweisung.

Im folgenden Beispiel wird gezeigt, wie der Gruppe „Marketing“ die Rolle „Mitwirkender“ im Bereich der Vertriebsressourcengruppe zugewiesen wurde.

![Abbildung: Beispiel für die Rollenzuweisung bei der Gruppe „Marketing“, die eine Kombination aus Sicherheitsprinzipal, Rollendefinition und Bereich darstellt. Die Gruppe „Marketing“ fällt unter den Sicherheitsprinzipal „Gruppe“. Ihr ist für den Bereich „Ressourcengruppe“ die Rolle „Mitwirkender“ zugewiesen.](../media/2-rbac-overview.png)

## <a name="rbac-is-an-allow-model"></a>RBAC ist ein Modell, das Zulassen ermöglicht

RBAC ist ein Modell, das Zulassen ermöglicht. Das bedeutet, dass RBAC zulässt, dass Sie bestimmte Aktionen wie Lesen, Schreiben oder Löschen durchführen können, wenn Ihnen eine entsprechende Rolle zugewiesen wurde. Wenn Ihnen also durch eine Rollenzuweisung Leseberechtigungen für eine Ressourcengruppe und durch eine andere Rollenzuweisung Schreibberechtigungen für dieselbe Ressourcengruppe erteilt wurden, verfügen Sie über Schreibberechtigungen für diese Ressourcengruppe.

Bei RBAC gibt es sogenannte `NotActions`-Berechtigungen. `NotActions` ist keine Ablehnungsregel. Es ist lediglich eine bequeme Möglichkeit, mehrere zulässige Berechtigungen zu erstellen, wenn bestimmte Berechtigungen ausgeschlossen werden müssen.

In dieser Einheit haben Sie die Grundlagen der RBAC kennengelernt. Nachdem Sie die grundlegenden Dinge über RBAC wissen, können Sie RBAC in der Praxis ausprobieren. Die einfachste Möglichkeit zum Einstieg ist die Verwendung des Azure-Portals. Im restlichen Teil dieses Moduls werden Sie praktische Übungen im Zusammenhang mit RBAC durchführen.