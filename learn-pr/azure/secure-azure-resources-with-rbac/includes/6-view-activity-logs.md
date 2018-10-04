Aus Gründen der Überwachung und Problembehandlung bewertet First Up Consultants vierteljährlich Änderungen der rollenbasierten Zugriffssteuerung (RBAC). Sie wissen, dass Änderungen im [Azure-Aktivitätsprotokoll](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) protokolliert werden. Ihr Vorgesetzter hat Sie gebeten, einen Bericht über die Rollenzuweisung und Änderungen der benutzerdefinierten Rollen des letzten Monats zu generieren.

## <a name="view-activity-logs"></a>Anzeigen von Aktivitätsprotokollen

Der einfachste Einstieg besteht im Anzeigen der Aktivitätsprotokolle im Azure-Portal.

1. Klicken Sie auf **Alle Dienste**, und suchen Sie dann **Aktivitätsprotokoll**.

    ![Aktivitätsprotokolle im Portal](../media/6-all-services-activity-log.png)

1. Klicken Sie auf **Aktivitätsprotokoll**, um dieses zu öffnen.

    ![Aktivitätsprotokolle im Portal](../media/6-activity-log-portal.png)

1. Legen Sie den Filter **TimeSpan** (Zeitraum) auf **Letzter Monat** fest.

1. Geben Sie im Filter **Vorgang** zum Filtern der Liste **Rolle** ein.

1. Wählen Sie die folgenden RBAC-Vorgänge aus:

    - Rollenzuweisung erstellen (roleAssignments)
    - Rollenzuweisung löschen (roleAssignments)
    - Benutzerdefinierte Rollendefinition erstellen oder aktualisieren (roleDefinitions)
    - Benutzerdefinierte Rollendefinition löschen (roleDefinitions)

    ![Filter „Vorgang“](../media/6-operation-filter.png)

    Nach wenigen Augenblicken werden alle Vorgänge für Rollenzuweisungen und Rollendefinitionen des letzten Monats angezeigt. Darüber hinaus ist ein Link enthalten, über den das Aktivitätsprotokoll als CSV-Datei heruntergeladen werden kann.

In dieser Einheit haben Sie gelernt, wie Sie das Azure-Aktivitätsprotokoll zum Auflisten von RBAC-Änderungen im Portal verwenden können und wie Sie einen einfachen Bericht generieren.