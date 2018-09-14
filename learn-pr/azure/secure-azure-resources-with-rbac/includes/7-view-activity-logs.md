Aus Gründen der Überwachung und Problembehandlung bewertet First Up Consultants vierteljährlich Änderungen der rollenbasierten Zugriffssteuerung (RBAC). Sie wissen, dass Änderungen im [Azure-Aktivitätsprotokoll](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) protokolliert werden. Ihr Vorgesetzter hat Sie gebeten, einen Bericht über die Rollenzuweisung und Änderungen der benutzerdefinierten Rollen des letzten Monats zu generieren.

## <a name="view-activity-logs"></a>Anzeigen von Aktivitätsprotokollen

Der einfachste Einstieg besteht im Anzeigen der Aktivitätsprotokolle im Azure-Portal.

1. Klicken Sie auf **Alle Dienste**, und suchen Sie dann **Aktivitätsprotokoll**.

    ![Aktivitätsprotokolle im Portal](../media-draft/7-all-services-activity-log.png)

1. Klicken Sie auf **Aktivitätsprotokoll**.

    ![Aktivitätsprotokolle im Portal](../media-draft/7-activity-log-portal.png)

1. Legen Sie den Filter **TimeSpan** (Zeitraum) auf **Letzten Monat** fest.

1. Legen Sie den Filter **Ereigniskategorie** auf **Administrativ** fest.

1. Geben Sie **Rolle** im Filter **Vorgang** ein, um die Liste zu filtern.

1. Wählen Sie die folgenden RBAC-Vorgänge aus:

    - Rollenzuweisung erstellen (roleAssignments)
    - Rollenzuweisung löschen (roleAssignments)
    - Benutzerdefinierte Rollendefinition erstellen oder aktualisieren (roleDefinitions)
    - Benutzerdefinierte Rollendefinition löschen (roleDefinitions)

    ![Filter „Vorgang“](../media-draft/7-operation-filter.png)

1. Klicken Sie auf **Anwenden**, um Ihre Filter anzuwenden.

    Alle Vorgänge für Rollenzuweisung und Rollendefinition des letzten Monats werden angezeigt. Außerdem ist ein Link enthalten, um das Aktivitätsprotokoll als CSV-Datei herunterzuladen.

    ![RBAC-Aktivitätsprotokolle](../media-draft/7-activity-log-portal-filter.png)

## <a name="end-lab"></a>Aufgabe beenden

1. Um die Aufgabe zu beenden, klicken Sie auf das Hamburger-Menü in der oberen rechten Ecke dieses Fensters, und klicken Sie dann auf **Beenden**.

1. Klicken Sie auf **Ja, Aufgabe beenden**.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie Azure-Aktivitätsprotokoll zum Auflisten von RBAC-Änderungen im Portal verwenden können und wie Sie einen einfachen Bericht generieren.
