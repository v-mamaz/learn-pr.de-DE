Moderne Anwendungen setzen sich häufig aus mehreren Komponenten zusammen, die auf separaten Computern und Geräten auf der ganzen Welt ausgeführt werden. Diese Komponenten können durch komplexe Netzwerke mit unterschiedlicher Geschwindigkeit und Verfügbarkeit verbunden sein. Eine wesentliche Herausforderung bei diesen verteilten Anwendungen ist die zuverlässige Kommunikation zwischen den Komponenten.

Angenommen, Sie sind Cloudentwickler bei Contoso Slices – einer weltweiten Kette von Pizzalieferanten. Ihr Arbeitgeber aktualisiert die verwendete Technologie, damit Benutzer Bestellungen über das Web oder über mobile Apps aufgeben können. Die Bestellungen werden an die vom Benutzer bevorzugte Filiale gesendet, wo die Pizza zubereitet wird. Während der Teig ausgerollt und die Pizza in den Ofen geschoben, verpackt und in das Lieferfahrzeug geladen wird, werden immer wieder Updates an die mobile App des Benutzers gesendet. Die Benutzer erhalten sogar immer wieder Informationen zum aktuellen Standort, während sich der Fahrer auf dem Weg zu ihnen befindet. 

Contoso Slices hatte bereits ein Onlinebestellsystem erstellt, bei dem die Bestelldaten sofort in einer SQL Server-Datenbank gespeichert wurden. Die Seite mit den Webbestellungen musste allerdings von jeder Filiale manuell aktualisiert werden, um zu prüfen, ob neue Bestellungen vorliegen. Zu Spitzenzeiten (etwa bei Sportübertragungen im Fernsehen) traten außerdem häufig Deadlock-Ausnahmen und Timeouts auf. Darüber hinaus verfügte das vorherige System über keine zentrale Zahlungsverarbeitung und bot keine Statusaktualisierungen für den Benutzer.

Für das neue ambitionierte Projekt hat Contoso einen Cloudarchitekten eingestellt und möchte eine entkoppelte Architektur verwenden. 

In diesem Modul erfahren Sie, wie Sie mit Azure Service Bus eine Anwendung erstellen können, die auch zu Spitzenzeiten zuverlässig funktioniert. Außerdem erfahren Sie, wie Azure Service Bus das Hinzufügen von Funktionen zu Anwendungen vereinfacht. Im Rahmen dieses Moduls erstellen wir den erforderlichen C#-Code, um diese Lektionen umzusetzen. Hier sehen Sie, wie Sie Azure Service Bus-Themen und -Warteschlangen in einer verteilten Architektur verwenden, um auch bei hoher Nachfrage eine zuverlässige Kommunikation zu gewährleisten. Außerdem schreiben Sie C#-Code für die Kommunikation über Service Bus.

## <a name="learning-objectives"></a>Lernziele

Dieses Modul umfasst Folgendes:
- Wählen zwischen Service Bus-Warteschlangen, -Themen und -Relays für die Kommunikation in einer verteilten Anwendung
- Konfigurieren eines Azure Service Bus-Namespace in einem Azure-Abonnement
- Erstellen eines Service Bus-**Themas** zum Senden und Empfangen von Nachrichten
- Erstellen einer Service Bus-**Warteschlange** zum Senden und Empfangen von Nachrichten
