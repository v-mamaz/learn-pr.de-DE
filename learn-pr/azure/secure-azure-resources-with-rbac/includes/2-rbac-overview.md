Angenommen, Sie müssen für die Entwicklungs-, Technik- und Marketingteams den Zugriff auf Ressourcen in Azure verwalten. Sie haben bereits erste Zugriffsanforderungen erhalten und müssen schnell herausfinden, wie die Zugriffsverwaltung bei Ressourcen in Azure funktioniert.

## <a name="what-is-rbac"></a>Was ist die RBAC?

Rollenbasierte Zugriffssteuerung (RBAC) ist eine Autorisierungssystem, das auf Azure Resource Manager, die eine differenzierte zugriffsverwaltung im Azure-Ressourcen bereitstellt. Azure bietet viele Ressourcen, wobei sich einige Beispiele auf virtuelle Computer, Websites, Netzwerke und Speicher beziehen.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvk]

## <a name="what-can-i-do-with-rbac"></a>Welche Möglichkeiten bietet RBAC?

RBAC ermöglicht Ihnen den Zugriff auf Azure-Ressourcen zu gewähren, die Sie steuern.

Hier einige Beispiele:

- Ein Benutzer kann virtuelle Computer in einem Abonnement verwalten, während ein anderer Benutzer virtuelle Netzwerke verwalten kann
- Eine Datenbankadministratorgruppe kann SQL-Datenbanken in einem Abonnement verwalten
- Ein Benutzer kann sämtliche Ressourcen in einer Ressourcengruppe verwalten, wie z.B. virtuelle Computer, Websites und Subnetze
- Eine Anwendung kann auf sämtliche Ressourcen in einer Ressourcengruppe zugreifen

## <a name="rbac-in-the-azure-portal"></a>RBAC im Azure-Portal

Im Azure-Portal wird in verschiedenen Bereichen ein Blatt mit dem Namen **Zugriffssteuerung (IAM)** (dentity & Access Management, Identitäts- und Zugriffsverwaltung) angezeigt. Auf diesem Blatt werden die Benutzer mit Zugriff auf diesen Bereich sowie deren Rollen angezeigt. Über dieses Blatt können Sie Zugriff gewähren oder den Zugriff aufheben.

Im Folgenden ist ein Beispiel für das Blatt „Zugriffssteuerung (IAM)“ für eine Ressourcengruppe dargestellt. In diesem Beispiel wurde Alain Charon die Sicherungs-Operator-Rolle für diese Ressourcengruppe zugewiesen.

![„Zugriffssteuerung (IAM)“ im Azure-Portal](../media/2-resource-group-access-control.png)

## <a name="how-does-rbac-work"></a>Funktionsweise von RBAC

Den Zugriff auf Ressourcen steuern Sie mit RBAC, indem Sie Rollenzuweisungen erstellen, mit denen die Durchsetzung von Berechtigungen gesteuert wird. Zum Erstellen einer Rollenzuweisung sind drei Elemente erforderlich: ein Sicherheitsprinzipal, eine Rollendefinition und ein Bereich. Sie können diese Elemente wie "Wer", "Was" und "where" vorstellen.

### <a name="1-security-principal-who"></a>1. Sicherheitsprinzipal (wer)

Ein *Sicherheitsprinzipal* ist nur ein ausgefallener Name für einen Benutzer, eine Gruppe oder eine Anwendung, auf den bzw. die Sie Zugriff gewähren möchten.

![Sicherheitsprinzipal](../media/2-rbac-security-principal.png)

### <a name="2-role-definition-what-you-can-do"></a>2. Rollendefinition (was Sie tun können)

Eine *Rollendefinition* ist eine Sammlung von Berechtigungen. Gelegentlich wird sie auch einfach als Rolle bezeichnet. In einer Rollendefinition sind die Berechtigungen wie etwa Lesen, Schreiben und Löschen aufgelistet. Rollen können auf allgemeiner Ebene erteilt werden (z.B. Besitzer) oder spezifisch sein (z.B. Mitwirkender für virtuelle Computer).

![Rollendefinition](../media/2-rbac-role-definition.png)

Azure umfasst verschiedene integrierte Rollen, die Sie verwenden können. Im Folgenden werden vier grundlegende integrierte Rollen aufgeführt:

- Besitzer: Verfügen über vollständigen Zugriff auf alle Ressourcen, einschließlich des Rechts, den Zugriff an andere Personen zu delegieren.
- Mitwirkende: Können alle Arten von Azure-Ressourcen erstellen und verwalten, aber keinen anderen Personen Zugriff gewähren.
- Leser: Können vorhandene Azure-Ressourcen anzeigen.
- Benutzerzugriffsadministratoren: Können den Benutzerzugriff auf Azure-Ressourcen verwalten.

Wenn die integrierten Rollen nicht die spezifischen Anforderungen Ihres Unternehmens entsprechen, können Sie eigene benutzerdefinierten Rollen erstellen.

### <a name="3-scope-where"></a>3. Bereich (wo)

*Bereich* ist der Ort, für den die Zugriffsberechtigung gilt. Dies ist hilfreich, wenn Sie einem Benutzer die Rolle „Mitwirkender von Website“ zuweisen möchten, jedoch nur für eine Ressourcengruppe.

In Azure können Sie auf mehreren Ebenen einen Bereich angeben: Verwaltungsgruppe, Abonnement, Ressourcengruppe oder Ressource. Bereiche sind in einer Beziehung zwischen über- und untergeordneten Elementen strukturiert. Wenn Sie den Zugriff in einem übergeordneten Bereich gewähren, werden diese Berechtigungen vom untergeordneten Bereich übernommen. Wenn Sie beispielsweise einer Gruppe im Abonnementbereich die Rolle „Mitwirkender“ zuweisen, wird diese Rolle von allen Ressourcengruppen und Ressourcen im Abonnement übernommen.

![Bereich](../media/2-rbac-scope.png)

### <a name="role-assignment"></a>Rollenzuweisung

Nachdem Sie wer, was und wo bestimmt haben, können Sie diese Elemente vereinen, um Zugriff zu gewähren. Eine *Rollenzuweisung* ist der Prozess, in dem eine Rolle zum Zwecke der Zugriffserteilung in einem bestimmten Bereich an einen Sicherheitsprinzipal gebunden wird. Erstellen Sie zum Gewähren des Zugriffs eine Rollenzuweisung. Entfernen Sie zum Widerrufen des Zugriffs eine Rollenzuweisung.

Im folgenden Beispiel wird gezeigt, wie der Gruppe „Marketing“ die Rolle „Mitwirkender“ im Bereich der Vertriebsressourcengruppe zugewiesen wurde.

![Rollenzuweisung](../media/2-rbac-overview.png)

## <a name="rbac-is-allow-only"></a>RBAC ist nur zulassen

RBAC ist ein Modell nur zulassen. Das bedeutet, dass RBAC zulässt, dass Sie bestimmte Aktionen wie Lesen, Schreiben oder Löschen durchführen können, wenn Ihnen eine entsprechende Rolle zugewiesen wurde. Wenn also eine rollenzuweisung gewährt Leseberechtigungen in einer Ressourcengruppe und eine andere rollenzuweisung erteilt, dass Sie Berechtigungen in der gleichen Ressourcengruppe schreiben, Sie Schreibberechtigungen für diese Ressourcengruppe.

Bei RBAC gibt es sogenannte `NotActions`-Berechtigungen. `NotActions` ist keine Verweigerungsregel. Es ist lediglich eine bequeme Möglichkeit, eine Gruppe zulässiger Berechtigungen zu erstellen, wenn bestimmte Berechtigungen ausgeschlossen werden müssen.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie die Grundlagen der Funktionsweise von RBAC kennengelernt. Nachdem Sie die grundlegenden Dinge über RBAC wissen, können Sie RBAC in der Praxis ausprobieren. Die einfachste Möglichkeit zum Einstieg ist die Verwendung des Azure-Portals. Im restlichen Teil dieses Moduls werden Sie praktische Übungen im Zusammenhang mit RBAC durchführen.
