In dieser Einheit verwenden Sie das Azure-Portal, um zu überprüfen, ob Ihr Event Hub gemäß den gewünschten Anforderungen funktioniert. Sie testen auch, wie das Event Hub-Messaging arbeitet, wenn es zeitweise nicht verfügbar ist. Des Weiteren testen Sie Event Hubs-Metriken, um die Leistung Ihres Event Hubs zu überprüfen.

## <a name="view-event-hub-activity"></a>Anzeigen der Event Hub-Aktivität

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Suchen Sie über die Suchleiste nach Ihrem Event Hub, und öffnen Sie ihn.

1. Zeigen Sie auf der Übersichtsseite die Nachrichtenanzahl an.

    ![Anzeigen von Event Hub-Nachrichten](../media-draft/6-view-messages.png)

1. Die Anwendungen „SimpleSend“ und „EventProcessorSample“ werden zum Senden bzw. Empfangen von 100 Nachrichten konfiguriert. Sie sehen, dass der Event Hub 100 Nachrichten der SimpleSend-Anwendung verarbeitet und 100 Nachrichten an die EventProcessorSample-Anwendung übertragen hat.

## <a name="test-event-hub-resilience"></a>Testen der Event Hub-Resilienz

Wenn Sie folgende Schritte befolgen, sehen Sie, was passiert, wenn eine Anwendung Nachrichten an einen Event Hub sendet, während dieser vorübergehend nicht verfügbar ist.

1. Senden Sie Nachrichten mithilfe der SimpleSend-Anwendung erneut an den Event Hub. Verwenden Sie den folgenden Befehl:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. Wenn Sie **Send Complete...** (Sendevorgang abgeschlossen) sehen, drücken Sie die EINGABETASTE.

1. Klicken Sie im Azure-Portal auf **Event Hubs-Instanz** > **EINSTELLUNGEN** > **Eigenschaften**.

1. Klicken Sie unter dem Event Hub-Zustand auf **Deaktiviert**.

    ![Deaktivieren des Event Hubs](../media-draft/7-disable-event-hub.png)

Warten Sie mindestens fünf Minuten.

1. Klicken Sie unter dem Event Hub-Zustand auf **Aktiv**, um Ihren Event Hub erneut zu aktivieren und Ihre Änderungen zu speichern.

1. Ausführen der EventProcessorSample-Anwendung zum Empfangen von Nachrichten Verwenden Sie den folgenden Befehl.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. Wenn in der Konsole keine Nachrichten mehr angezeigt werden, drücken Sie die EINGABETASTE.

1. Suchen Sie im Azure-Portal Ihren Event Hub **_namespace_**, und öffnen Sie ihn. 

1. Klicken Sie auf **Event Hubs-Namespace** > **ÜBERWACHUNG** > **Metrik (Vorschau)**.

    ![Verwenden von Event Hub-Metrik](../media-draft/7-event-hub-metrics.png)

1. Wählen Sie aus der **Metrik**-Liste die Option **Eingehende Nachricht** aus, und klicken Sie auf **Metrik hinzufügen**.

1. Wählen Sie aus der **Metrik**-Liste die Option **Ausgehende Nachricht** aus, und klicken Sie auf **Metrik hinzufügen**.

1. Klicken Sie am oberen Rand des Diagramms auf **Letzte 24 Stunden (automatisch)**, um den Zeitraum in **Letzte 30 Minuten** zu ändern.

1. Klicken Sie auf **Anwenden**.

Sie sehen nun, dass alle 100 Nachrichten erfolgreich übermittelt wurden, obwohl diese gesendet wurden, bevor der Event Hub für einen Zeitraum offline war.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie die Event Hubs-Metrik verwenden, um zu testen, ob Ihr Event Hub den Sende- und Empfangsprozess von Nachrichten erfolgreich verarbeitet.
