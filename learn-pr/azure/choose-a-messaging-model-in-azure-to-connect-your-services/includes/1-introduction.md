Viele Anwendungen bestehen aus Programmen, die auf mehreren Computern oder Geräten ausgeführt werden. In solchen verteilten Anwendungen müssen Nachrichten zwischen den Komponenten über Netzwerke und große Entfernungen gesendet werden. Selbst auf demselben Server oder im selben Rechenzentrum erfordern lose gekoppelte Architekturen Mechanismen für die Kommunikation der Komponenten. Zuverlässiges Messaging ist häufig ein kritisches Problem.

Angenommen, Sie arbeiten bei einer Softwarefirma, die eine Anwendung für den Austausch von Musik entwickelt. Dabei können Musiker ihre Songs über ein Web-Front-End oder eine mobile App auf Ihre Plattform hochladen. Außerdem können sie sich die Lieder anderer Mitglieder anhören und diese kommentieren. Die Anwendung besteht aus einer Website, die bei Ihrem ISP ausgeführt wird, einer mobilen App, die auf den mobilen Geräten der Benutzer ausgeführt wird, einer Web-API, die in Azure läuft, und einer Azure SQL-Datenbankinstanz, in der Daten gespeichert werden.

Sie haben beobachtet, dass im Fall hoher Auslastung einige Musikdateien nicht erfolgreich hochgeladen und einige Kommentare nicht veröffentlicht werden. Ihre Tests zeigen, dass diese Probleme durch verloren gegangene Nachrichten zwischen Front-End-Komponenten und Web-API verursacht werden. Nun möchten Sie diese Probleme mit mindestens einer der folgenden Technologien lösen: Azure Storage-Warteschlangen, Azure Event Hubs, Azure Event Grid und Azure Service Bus.

Im Folgenden erfahren Sie, wie Sie für jede Kommunikationsaufgabe in einer verteilten Anwendung die richtige Messagingtechnologie in Azure auswählen.

## <a name="learning-objectives"></a>Lernziele
In diesem Modul

- beschreiben Sie Ereignisse und Nachrichten sowie die Herausforderungen, die Sie damit in einer verteilten Anwendung bewältigen können,
- ermitteln Szenarios, in denen eine Azure Storage-Warteschlange die beste Messagingtechnologie für eine Anwendung ist,
- ermitteln Szenarios, in denen Event Grid die beste Messagingtechnologie für eine Anwendung ist,
- ermitteln Szenarios, in denen Event Grid die beste Messagingtechnologie für eine Anwendung ist
- und ermitteln Szenarios, in denen Azure Service Bus die beste Messagingtechnologie für eine Anwendung ist.
