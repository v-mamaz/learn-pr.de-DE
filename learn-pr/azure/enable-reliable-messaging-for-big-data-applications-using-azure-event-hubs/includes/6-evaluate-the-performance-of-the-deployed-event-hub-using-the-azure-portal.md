Wenn Sie Event Hubs verwenden, ist es sehr wichtig, dass Sie Ihren Hub überwachen, um sicherzustellen, dass dieser wie erwartet funktioniert.

Wir fahren nun mit dem Banking-Beispiel fort und nehmen an, dass Sie Azure Event Hubs bereitgestellt sowie Absender- und Empfängeranwendungen konfiguriert haben. Ihre Anwendungen sind zum Testen der Zahlungsverarbeitungslösung bereit. Die Absenderanwendung sammelt die Kreditkartendaten des Kunden, und die Empfängeranwendung überprüft, ob die Kreditkarte gültig ist. Aufgrund der sensiblen Informationen des Unternehmens Ihres Arbeitgebers ist es wichtig, dass Ihre Zahlungsverarbeitung robust und zuverlässig ist, auch wenn sie vorübergehend nicht verfügbar ist.

Sie müssen Ihren Event Hub auswerten, indem Sie überprüfen, ob Ihr Event Hub Daten wie erwartet verarbeitet. Mit den in den Event Hubs verfügbaren Metriken können Sie sicherstellen, dass alles perfekt funktioniert.

## <a name="how-do-you-use-the-azure-portal-to-view-your-event-hub-activity"></a>Wie können Sie das Azure-Portal verwenden, um Ihre Event Hub-Aktivität anzuzeigen?

Die Übersichtsseite für Ihren Event Hub im Azure-Portal zeigt die Nachrichtenmenge an. Diese Nachrichtenanzahl stellt die Daten (Ereignisse) dar, die vom Event Hub empfangen und von diesem gesendet werden. Sie können diese Ereignisse über die Zeitskala anzeigen.

![Anzeigen von Event Hub-Nachrichten](../media-draft/6-view-messages.png)

## <a name="how-can-you-test-event-hub-resilience"></a>Wie können Sie Ihre Event Hub-Resilienz testen?

Azure Event Hubs empfängt ständig Nachrichten von der Absenderanwendung, auch wenn der Dienst nicht verfügbar ist. Die während diesem Zeitraum empfangenen Nachrichten werden erfolgreich übertragen, sobald der Hub wieder verfügbar ist.

Sie können das Azure-Portal verwenden, um Ihren Event Hub zu deaktivieren, damit Sie diese Funktionalität testen können.

Wenn Sie Ihren Event Hub erneut aktivieren, können Sie Ihre Absenderanwendung erneut ausführen und Event Hubs-Metrik für Ihren Namespace verwenden. So können Sie überprüfen, ob alle Absendernachrichten erfolgreich übertragen und anschließend empfangen wurden.

Andere nützliche Metriken, die in den Event Hubs zur Verfügung stehen, sind folgende:

- Gedrosselte Anforderungen: die Anzahl von Anforderungen, die gedrosselt wurden, da der Grenzwert für die Nutzung der Durchsatzeinheit überschritten wurde
- ActiveConnections: die Anzahl der aktiven Verbindungen in einem Namespace oder Event Hub
- Eingehende/Ausgehende Bytes: die Anzahl von Bytes, die in einem bestimmten Zeitraum an den Azure Event Hubs-Dienst gesendet wurden

## <a name="summary"></a>Zusammenfassung

Das Azure-Portal stellt Nachrichtenmengen und andere Metriken bereit, die Sie als Integritätsprüfung für Ihre Event Hubs verwenden können.
