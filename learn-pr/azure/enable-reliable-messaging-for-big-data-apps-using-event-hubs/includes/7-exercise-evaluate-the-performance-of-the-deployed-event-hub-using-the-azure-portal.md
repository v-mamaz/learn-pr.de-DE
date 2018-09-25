In dieser Einheit verwenden Sie das Azure-Portal, um zu überprüfen, ob Ihr Event Hub gemäß den gewünschten Anforderungen funktioniert. Sie testen auch, wie das Event Hub-Messaging arbeitet, wenn es zeitweise nicht verfügbar ist. Des Weiteren testen Sie Event Hubs-Metriken, um die Leistung Ihres Event Hubs zu überprüfen.

## <a name="view-event-hub-activity"></a>Anzeigen der Event Hub-Aktivität

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

1. Suchen Sie über die Suchleiste nach Ihrem Event Hub, und öffnen Sie ihn.

1. Zeigen Sie auf der Übersichtsseite die Nachrichtenanzahl an.

    ![Screenshot des Azure-Portals mit Anzeige des Event Hub-Namespaces und der Nachrichtenanzahl.](../media/6-view-messages.png)

1. Die Anwendungen „SimpleSend“ und „EventProcessorSample“ werden zum Senden bzw. Empfangen von 100 Nachrichten konfiguriert. Sie sehen, dass der Event Hub 100 Nachrichten der SimpleSend-Anwendung verarbeitet und 100 Nachrichten an die EventProcessorSample-Anwendung übertragen hat.

## <a name="test-event-hub-resilience"></a>Testen der Event Hub-Resilienz

Wenn Sie die folgenden Schritte ausführen, sehen Sie, was passiert, wenn eine Anwendung Nachrichten an einen Event Hub sendet, während dieser vorübergehend nicht verfügbar ist.

1. Senden Sie Nachrichten mithilfe der SimpleSend-Anwendung erneut an den Event Hub. Verwenden Sie den folgenden Befehl:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. Wenn **Send Complete...** (Sendevorgang abgeschlossen) angezeigt wird, drücken Sie die <kbd>EINGABETASTE</kbd>.

1. Wählen Sie Ihren Event Hub im Bildschirm **Übersicht** aus. Nun werden für den Event Hub spezifische Details angezeigt. Sie können zu diesem Bildschirm auch über den Eintrag **Event Hubs** auf der Namespaceseite gelangen.

1. Wählen Sie **Einstellungen** > **Eigenschaften** aus.

1. Klicken Sie unter dem Event Hub-Zustand auf **Deaktiviert**. Speichern Sie die Änderungen.

    ![Deaktivieren des Event Hubs](../media/7-disable-event-hub.png)

    **Warten Sie mindestens fünf Minuten.**

1. Klicken Sie unter dem Event Hub-Zustand auf **Aktiv**, um Ihren Event Hub erneut zu aktivieren und Ihre Änderungen zu speichern.

1. Ausführen der EventProcessorSample-Anwendung zum Empfangen von Nachrichten Verwenden Sie den folgenden Befehl.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. Wenn in der Konsole keine Nachrichten mehr angezeigt werden, drücken Sie die <kbd>EINGABETASTE</kbd>.

1. Zurück im Azure-Portal navigieren Sie zurück zu Ihrem Event Hub-Namespace. Wenn Sie sich noch auf der Seite „Event Hub“ befinden, können Sie mit dem Breadcrumb oben auf dem Bildschirm zurücknavigieren. Sie können auch nach dem Namespace suchen und ihn auswählen.

1. Klicken Sie auf **ÜBERWACHUNG** > **Metriken (Vorschau)**.

    ![Screenshot mit den Event Hub-Metriken und der angezeigten Anzahl der ein- und ausgehenden Nachrichten.](../media/7-event-hub-metrics.png)

1. Wählen Sie aus der Liste **Metrik** die Option **Eingehende Nachricht** aus, und klicken Sie auf **Metrik hinzufügen**.

1. Wählen Sie aus der Liste **Metrik** die Option **Ausgehende Nachricht** aus, und klicken Sie auf **Metrik hinzufügen**.

1. Klicken Sie am oberen Rand des Diagramms auf **Letzte 24 Stunden (automatisch)**, um den Zeitraum in **Letzte 30 Minuten** zu ändern und das Datendiagramm zu erweitern.

Sie sehen nun, dass alle 100 Nachrichten erfolgreich übermittelt wurden, obwohl diese gesendet wurden, bevor der Event Hub für einen Zeitraum offline war.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie die Event Hubs-Metriken verwendet, um zu testen, ob Ihr Event Hub den Sende- und Empfangsvorgang von Nachrichten erfolgreich verarbeitet.
