Angenommen, Sie müssen für die Entwicklungs-, Technik- und Marketingteams den Zugriff auf Ressourcen in Azure verwalten. Sie haben bereits erste Zugriffsanforderungen erhalten und müssen schnell herausfinden, wie die Zugriffsverwaltung bei Ressourcen in Azure funktioniert.

## <a name="what-is-rbac"></a>Was ist RBAC?

Bei der rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) handelt es sich um ein Autorisierungssystem, das auf [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) basiert und eine differenzierte Verwaltung des Zugriffs auf Ressourcen in Azure ermöglicht. Azure bietet viele Ressourcen, wobei sich einige Beispiele auf virtuelle Computer, Websites, Netzwerke und Speicher beziehen.

## <a name="what-can-i-do-with-rbac"></a>Welche Möglichkeiten bietet RBAC?

Mit RBAC können Sie einzelnen Benutzern oder Benutzergruppen Zugriff auf Azure-Ressourcen gewähren, die Sie bestimmen.

Hier einige Beispiele:
- Ein Benutzer kann virtuelle Computer in einem Abonnement verwalten, während ein anderer Benutzer virtuelle Netzwerke verwalten kann
- Eine Datenbankadministratorgruppe kann SQL-Datenbanken in einem Abonnement verwalten
- Ein Benutzer kann sämtliche Ressourcen in einer Ressourcengruppe verwalten, wie z.B. virtuelle Computer, Websites und Subnetze
- Eine Anwendung kann auf sämtliche Ressourcen in einer Ressourcengruppe zugreifen

## <a name="rbac-in-the-azure-portal"></a>RBAC im Azure-Portal

Im Azure-Portal wird in verschiedenen Bereichen ein Blatt mit dem Namen **Zugriffssteuerung (IAM)** (dentity & Access Management, Identitäts- und Zugriffsverwaltung) angezeigt. Auf diesem Blatt werden die Benutzer mit Zugriff auf diesen Bereich sowie deren Rollen angezeigt. Über dieses Blatt können Sie Zugriff gewähren oder den Zugriff aufheben.

Im Folgenden ist ein Beispiel für das Blatt „Zugriffssteuerung (IAM)“ für eine Ressourcengruppe dargestellt. In diesem Beispiel wurde Alain Charon die Rolle „Sicherungsoperator“ für diese Ressourcengruppe zugewiesen.

![„Zugriffssteuerung (IAM)“ im Azure-Portal](../media-draft/2-resource-group-access-control.png)

## <a name="how-does-rbac-work"></a>Funktionsweise von RBAC

Den Zugriff auf Ressourcen steuern Sie mit RBAC, indem Sie Rollenzuweisungen erstellen, mit denen die Durchsetzung von Berechtigungen gesteuert wird. Zum Erstellen einer Rollenzuweisung sind drei Elemente erforderlich: ein Sicherheitsprinzipal, eine Rollendefinition und ein Bereich. Nach diesen drei Elementen können Sie mit „wer“, „was“ und „wo“ fragen.

### <a name="1-security-principal-who"></a>1. Sicherheitsprinzipal (wer)

Ein *Sicherheitsprinzipal* ist nur ein ausgefallener Name für einen Benutzer, eine Gruppe oder eine Anwendung, auf den bzw. die Sie Zugriff gewähren möchten.

![Sicherheitsprinzipal](../media-draft/2-rbac-security-principal.png)

### <a name="2-role-definition-what-you-can-do"></a>2. Rollendefinition (was Sie tun können)

Eine *Rollendefinition* ist eine Sammlung von Berechtigungen. Gelegentlich wird sie auch einfach als Rolle bezeichnet. In einer Rollendefinition sind die Berechtigungen wie etwa Lesen, Schreiben und Löschen aufgelistet. Rollen können auf allgemeiner Ebene erteilt werden (z.B. Besitzer) oder spezifisch sein (z.B. Mitwirkender für virtuelle Computer).

![Rollendefinition](../media-draft/2-rbac-role-definition.png)

Azure umfasst mehrere [integrierte Rollen](/azure/role-based-access-control/built-in-roles), die Sie verwenden können. Im Folgenden werden vier grundlegende integrierte Rollen aufgeführt:

- Besitzer: Verfügen über vollständigen Zugriff auf alle Ressourcen, einschließlich des Rechts, den Zugriff an andere Personen zu delegieren.
- Mitwirkende: Können alle Arten von Azure-Ressourcen erstellen und verwalten, aber keinen anderen Personen Zugriff gewähren.
- Leser: Können vorhandene Azure-Ressourcen anzeigen.
- Benutzerzugriffsadministratoren: Können den Benutzerzugriff auf Azure-Ressourcen verwalten.

Wenn die integrierten Rollen den Ansprüchen Ihrer Organisation nicht entsprechen, können Sie Ihre eigenen [benutzerdefinierten Rollen](/azure/role-based-access-control/custom-roles) erstellen.

### <a name="3-scope-where"></a>3. Bereich (wo)

*Bereich* ist der Ort, für den die Zugriffsberechtigung gilt. Dies ist hilfreich, wenn Sie einem Benutzer die Rolle „Mitwirkender von Website“ zuweisen möchten, jedoch nur für eine Ressourcengruppe.

In Azure können Sie auf mehreren Ebenen einen Bereich angeben: Verwaltungsgruppe, Abonnement, Ressourcengruppe oder Ressource. Bereiche sind in einer Beziehung zwischen über- und untergeordneten Elementen strukturiert. Wenn Sie den Zugriff in einem übergeordneten Bereich gewähren, werden diese Berechtigungen vom untergeordneten Bereich übernommen. Wenn Sie beispielsweise einer Gruppe im Abonnementbereich die Rolle „Mitwirkender“ zuweisen, wird diese Rolle von allen Ressourcengruppen und Ressourcen im Abonnement übernommen.

![Bereich](../media-draft/2-rbac-scope.png)

### <a name="role-assignment"></a>Rollenzuweisung

Nachdem Sie wer, was und wo bestimmt haben, können Sie diese Elemente vereinen, um Zugriff zu gewähren. Eine *Rollenzuweisung* ist der Prozess, in dem eine Rolle zum Zwecke der Zugriffserteilung in einem bestimmten Bereich an einen Sicherheitsprinzipal gebunden wird. Erstellen Sie zum Gewähren des Zugriffs eine Rollenzuweisung. Entfernen Sie zum Widerrufen des Zugriffs eine Rollenzuweisung.

Im folgenden Beispiel wird gezeigt, wie der Gruppe „Marketing“ die Rolle „Mitwirkender“ im Bereich der Vertriebsressourcengruppe zugewiesen wurde.

![Rollenzuweisung](../media-draft/2-rbac-overview.png)

## <a name="rbac-is-allow-only-with-no-deny"></a>RBAC – nur zulassen, nicht verweigern

Derzeit ist RBAC ein Modell, das nur Zulassen und kein Verweigern ermöglicht. Das bedeutet, dass RBAC zulässt, dass Sie bestimmte Aktionen wie Lesen, Schreiben oder Löschen durchführen können, wenn Ihnen eine entsprechende Rolle zugewiesen wurde. Den Zugriff explizit verweigern kann RBAC nicht. Wenn Ihnen also durch eine Rollenzuweisung Leseberechtigungen für eine Ressourcengruppe und durch eine andere Rollenzuweisung Schreibberechtigungen für dieselbe Ressourcengruppe erteilt wurden, verfügen Sie über Schreibberechtigungen für diese Ressourcengruppe.

Bei RBAC gibt es sogenannte `NotActions`-Berechtigungen. `NotActions` ist keine Verweigerungsregel. Es ist lediglich eine bequeme Möglichkeit, eine Gruppe zulässiger Berechtigungen zu erstellen, wenn bestimmte Berechtigungen ausgeschlossen werden müssen.

## <a name="other-roles-in-azure"></a>Weitere Rollen in Azure

Bei Ihrer Arbeit mit Azure werden Ihnen weitere Rollen begegnen wie etwa die Rollen „Globaler Administrator“, „Kontoadministrator“ und verschiedene andere. Viele dieser Rollen werden für die Azure Active Directory-Verwaltung verwendet, etwa zum Erstellen von Benutzern, zum Zurücksetzen von Kennwörtern, zum Verwalten von Benutzerlizenzen sowie zum Verwalten von Domänen. Es gibt weitere Informationen, die Sie lesen können, wenn Sie weitere Details erfahren möchten. Wichtig ist jedoch, dass Sie sich merken, dass RBAC-Rollen zum Verwalten des Zugriffs auf Azure-Ressourcen verwendet wird.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie die Grundlagen der Funktionsweise von RBAC kennengelernt. Nachdem Sie die grundlegenden Dinge über RBAC wissen, können Sie RBAC in der Praxis ausprobieren. Die einfachste Möglichkeit zum Einstieg ist die Verwendung des Azure-Portals. Im restlichen Teil dieses Moduls werden Sie praktische Übungen im Zusammenhang mit RBAC durchführen.
