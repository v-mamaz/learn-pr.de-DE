Viele Anwendungen bestehen aus Programmen, die auf mehreren Computern oder Geräten ausgeführt werden. In solchen verteilten Anwendungen müssen Nachrichten zwischen den Komponenten über Netzwerke und große Entfernungen gesendet werden. Selbst auf dem gleichen Server oder im gleichen Rechenzentrum erfordern lose gekoppelte Architekturen Mechanismen für die Kommunikation der Komponenten. Zuverlässiges Messaging ist häufig ein kritisches Problem.

Angenommen, Sie arbeiten bei einer Softwarefirma, die eine Musik-Sharing-Anwendung entwickelt. Musiker können Musik, die sie erstellen, über ein Web-Front-End oder eine mobile App auf Ihre Plattform hochladen. Sie können sich die Stücke anderer Mitglieder anhören und diese kommentieren. Die Anwendung besteht aus einer Website, die bei Ihrem Internetdienstanbieter ausgeführt wird, einer mobilen App, die auf den mobilen Geräten der Benutzer betrieben wird, einer Web-API, die in Azure läuft, und einer Azure SQL-Datenbank, in der Daten gespeichert werden.

Sie haben beobachtet, dass zu Zeiten hoher Nachfrage einige Musikdateien nicht erfolgreich hochgeladen und einige Kommentare nicht veröffentlicht werden. Ihre Tests zeigen, dass diese Probleme durch verloren gegangene Nachrichten zwischen Front-End-Komponenten und Web-API verursacht werden. Sie planen, diese Probleme zu lösen, indem Sie eine oder mehrere der folgenden Azure-Technologien verwenden: Storage-Warteschlangen, Event Hubs, Event Grids und Service Bus.

Im Folgenden erfahren Sie, wie Sie für jede Kommunikationsaufgabe in einer verteilten Anwendung die richtige Messagingtechnologie in Azure wählen.

## <a name="learning-objectives"></a>Lernziele

- Beschreiben von Ereignissen und Nachrichten sowie der Herausforderungen, die Sie damit in einer verteilten Anwendung bewältigen können
- Bestimmen von Szenarien, in denen eine Azure Storage-Warteschlange die beste Messagingtechnologie für eine Anwendung ist
- Bestimmen von Szenarien, in denen Azure Event Grid die beste Messagingtechnologie für eine Anwendung ist
- Bestimmen von Szenarien, in denen Azure Event Hub die beste Messagingtechnologie für eine Anwendung ist
- Bestimmen von Szenarien, in denen Azure Service Bus die beste Messagingtechnologie für eine Anwendung ist
