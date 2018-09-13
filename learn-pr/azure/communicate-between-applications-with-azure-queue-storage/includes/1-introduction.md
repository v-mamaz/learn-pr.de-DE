Angenommen, Sie arbeiten für eine wichtige Nachrichtenagentur, die über aktuelle Nachrichten berichtet. Das Unternehmen beschäftigt weltweit Journalisten, die über ein Webportal und eine mobile App ständig Updates senden. Die Logikschicht eines Webdiensts veröffentlicht diese neuen Nachrichten dann über mehrere Kanäle im Internet.

Es wurde jedoch festgestellt, dass dem System Nachrichten entgehen, wenn etwas geschieht, das die ganze Welt betrifft. Das ist ein _großes_ Problem, da die Mitbewerber dem Unternehmen so zuvorkommen. Sie als der beste Entwickler des Unternehmens wurden ausgewählt, um das Problem zu identifizieren und zu beheben.

Die Logikschicht enthält viele Funktionen, um normale Kapazitäten zu bewältigen. Ein Blick auf die Serverprotokolle zeigt jedoch, dass das System überlastet war, als mehrere Journalisten versucht haben, größere aktuelle Nachrichten gleichzeitig hochzuladen. Einige davon haben sich beschwert, dass das Portal nicht reagiert hat, während andere angegeben haben, dass ihre Berichte verloren gegangen sind. Sie haben eine direkte Korrelation zwischen den gemeldeten Problemen und der Spitze bei der Nachfrage auf den Servern der Logikschicht erkannt.

Nun müssen Sie eine Möglichkeit finden, um diese unerwarteten Spitzen zu bewältigen. Sie sollten keine weiteren Instanzen der Website und des Logikschicht-Webdiensts hinzufügen, da diese teuer und unter normalen Umständen überflüssig sind. Sie könnten Instanzen dynamisch einrichten, dies nimmt jedoch viel Zeit in Anspruch, und Sie müssten darauf warten, dass neue Server online geschaltet werden.

Sie können dieses Problem lösen, indem Sie Azure Queue Storage verwenden. Bei einer Storage-Warteschlange handelt es sich um einen leistungsstarken Puffer für Nachrichten, der als Broker zwischen den Front-End-Komponenten (den „Herstellern“) und der Logikschicht (den „Konsumenten“) fungieren kann. 

Die Front-End-Komponenten erstellen eine Meldung für jede neue Nachricht in der Warteschlange. Die Logikschicht ruft diese Meldungen dann nacheinander aus der Warteschlange ab, um diese zu verarbeiten. Wenn eine hohe Auslastung vorliegt, kann die Warteschlange länger werden, es gehen jedoch keine Berichte verloren, und die Anwendung bleibt reaktionsfähig. Wenn die Auslastung sich wieder normalisiert, holt der Webdienst auf, indem er sich durch das Backlog der Warteschlange arbeitet.

Erfahren Sie, wie Sie Azure Queue Storage verwenden können, um hohe Auslastung zu bewältigen und die Resilienz in Ihren verteilten Anwendungen zu verbessern.

## <a name="learning-objectives"></a>Lernziele

- Erstellen Sie ein Azure Storage-Konto, das Warteschlangen unterstützt.
- Erstellen Sie eine Warteschlange mithilfe von C# und der Azure Storage-Clientbibliothek für .NET.
- Verwenden Sie C# und die Azure Storage-Clientbibliothek für .NET, um Meldungen zu einer Warteschlange hinzuzufügen, abzurufen und aus dieser zu entfernen.