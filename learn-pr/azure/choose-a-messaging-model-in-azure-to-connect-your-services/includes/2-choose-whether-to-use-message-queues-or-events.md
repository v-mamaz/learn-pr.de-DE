Angenommen, Sie planen die Architektur einer verteilten Anwendung zum Austauschen von Musik. Sie möchten sicherstellen, dass die Anwendung möglichst zuverlässig und skalierbar ist, und Sie beabsichtigen die Verwendung von Azure-Technologien, um eine stabile Kommunikationsinfrastruktur zu erstellen.

Bevor Sie die richtige Azure-Technologie auswählen können, müssen Sie die gesamte Kommunikation verstehen, die die Komponenten der Anwendung austauschen. Für jeden Kommunikationsschritt können Sie eine andere Azure-Technologie auswählen.

Zunächst müssen Sie wissen, ob für die Kommunikation **Nachrichten** oder **Ereignisse** gesendet werden. Das ist eine wichtige Entscheidung, die Ihnen dabei hilft, einen entsprechenden Azure-Dienst zu finden.

## <a name="what-is-a-message"></a>Was ist eine Nachricht?
In der Terminologie von verteilten Anwendungen weisen **Nachrichten** folgende Merkmale auf:

- Eine Nachricht enthält Rohdaten, die von einer Komponente erzeugt wurden und von einer anderen Komponente verwendet werden.
- Eine Nachricht enthält die Daten selbst, nicht nur einen Verweis auf diese Daten.
- Die sendende Komponente erwartet, dass der Inhalt der Nachricht auf eine bestimmte Weise von der Zielkomponente verarbeitet wird. Die Integrität des gesamten Systems kann davon abhängen, dass Absender und Empfänger einen bestimmten Auftrag ausführen.

Stellen Sie sich beispielsweise vor, dass ein Benutzer einen neuen Song mit der mobilen App zum Austauschen von Musik hochlädt. Die mobile App muss diesen Song an die Web-API senden, die in Azure ausgeführt wird. Die Mediendatei des Songs selbst muss gesendet werden, nicht nur eine Benachrichtigung, die angibt, dass ein neuer Song hinzugefügt wurde. Die mobile App erwartet, dass die Web-API den neuen Song in der Datenbank speichert und für andere Benutzer verfügbar macht. Dies ist ein Beispiel für eine Nachricht.

## <a name="what-is-an-event"></a>Was ist ein Ereignis?

**Ereignisse** sind einfacher als Nachrichten und werden am häufigsten für die Broadcastkommunikation verwendet. Die Komponenten, die das Ereignis senden, werden als **Herausgeber** bezeichnet, und die Empfänger werden als **Abonnenten** bezeichnet.

Bei Ereignissen entscheiden die empfangenden Komponenten im Allgemeinen, an welcher Kommunikation sie interessiert sind, und „abonnieren“ sie. Das Abonnement wird in der Regel von einem Vermittler wie Azure Event Grid oder Azure Event Hubs verwaltet. Wenn Herausgeber ein Ereignis senden, leitet der Vermittler dieses Ereignis an interessierte Abonnenten weiter. Das wird auch als „Herausgeben-Abonnieren-Architektur“ bezeichnet. Dies ist nicht die einzige Möglichkeit zum Behandeln von Ereignissen, aber die am häufigsten genutzte.

Ereignisse weisen folgende Merkmale auf:

- Ein Ereignis ist eine einfache Benachrichtigung, die angibt, dass etwas passiert ist.
- Das Ereignis kann an mehrere Empfänger oder an gar keine Empfänger gesendet werden.
- Ereignisse sollen sich meist „weit verbreiten“ oder haben eine große Anzahl von Abonnenten für jeden Herausgeber.
- Der Herausgeber des Ereignisses hat keine Erwartungen hinsichtlich der Aktion, die eine empfangende Komponente ausführt.
- Einige Ereignisse sind diskrete Einheiten und stehen nicht mit anderen Ereignissen im Zusammenhang. 
- Einige Ereignisse sind Teil einer verknüpften und geordneten Reihe.  

Stellen Sie sich beispielsweise vor, der Upload der Musikdatei wurde abgeschlossen und der neue Song der Datenbank hinzugefügt. Um Benutzer über die neue Datei zu informieren, muss die Web-API die Benutzer des Web-Front-Ends und der mobilen App über die neue Datei informieren. Die Benutzer können entscheiden, ob sie sich den neuen Song anhören möchten. Die erste Benachrichtigung enthält also nicht die Musikdatei, sondern benachrichtigt die Benutzer nur darüber, dass der Song vorhanden ist. Der Absender hat keine bestimmte Erwartung, dass der Ereignisempfänger als Reaktion auf den Empfang dieses Ereignisses etwas Bestimmtes tut.

Dies ist ein Beispiel für ein diskretes Ereignis.

## <a name="how-to-choose-messages-or-events"></a>Auswählen von Nachrichten oder Ereignissen

Eine einzelne Anwendung wird wahrscheinlich Ereignisse für einige Funktionen und Nachrichten für andere verwenden. Vor der Entscheidung müssen Sie die Anwendungsarchitektur und alle Anwendungsfälle analysieren, um alle unterschiedlichen Funktionen zu identifizieren, für die ihre Komponenten miteinander kommunizieren müssen.

Ereignisse werden eher für Broadcasts verwendet und sind oft kurzlebig. Dies bedeutet, dass die Kommunikation möglicherweise von keinem Empfänger verarbeitet wird, wenn keiner sie gerade abonniert hat. Nachrichten werden eher verwendet, wenn die verteilte Anwendung eine Garantie benötigt, dass die Kommunikation verarbeitet wird.

Stellen Sie sich für jede Kommunikation folgende Frage: **Erwartet die sendende Komponente, dass die Kommunikation von der Zielkomponente auf eine bestimmte Weise verarbeitet wird?**

Wenn die Antwort _Ja_ lautet, verwenden Sie eine Nachricht. Wenn die Antwort _Nein_ lautet, können Sie möglicherweise Ereignisse verwenden.

Wenn Sie verstehen, wie Ihre Komponenten miteinander kommunizieren, können Sie besser entscheiden, wie sie miteinander kommunizieren sollen. Beginnen wir mit Nachrichten.