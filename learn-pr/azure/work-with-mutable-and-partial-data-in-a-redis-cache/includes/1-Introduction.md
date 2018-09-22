Angenommen, Sie erstellen eine mobile Instant Messaging-Anwendung. Ihre Anwendung ermöglicht es Benutzern, Nachrichten an alle Mitglieder einer bestimmten benutzerdefinierten Gruppe zu senden. Es gibt einige Daten, die für jeden Benutzer gespeichert werden müssen, etwa der Benutzername, die E-Mail-Adresse und das Kennwort. Sie entscheiden sich also dafür, SQL Server zu verwenden, um eine relationale Datenbank für diese Informationen zu erstellen. Allerdings müssen die Nachrichten selbst schnell gesendet werden und schnellen Zugriff ermöglichen, und eine relationale Datenbank ist dafür zu langsam.

Aufgrund der vielen Vorteile, die er bereitstellt, beschließen Sie, einen Azure Redis Cache zu erstellen. Wie Sie bereits im Modul **Optimize your web applications by caching read-only data with Redis** (Optimieren Ihrer Webanwendungen durch das Zwischenspeichern von schreibgeschützten Daten mit Redis) erfahren haben, ist ein Redis Cache ein In-Memory-Datenspeicher, der als Datenbank, Cache oder Nachrichtenbroker verwendet werden kann.

Mit dem Azure Redis Cache können Sie Transaktionen verwenden, um sicherzustellen, dass ein Bild und ein Text, die in einer Nachricht enthalten sind, zusammen gesendet werden. Mithilfe der Ablaufzeit für Daten setzen Sie den Namen des Gruppenchats nach einer Stunde zurück. Zusätzlich verwenden Sie Entfernungsrichtlinien, um sicherzustellen, dass die ältesten Nachrichten zuerst gelöscht werden, wenn der Speicher knapp wird.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Gruppieren mehrerer Vorgänge in einer Transaktion
- Festlegen einer Ablaufzeit für Ihre Daten
- Verwalten von Bedingungen mit nicht genügend Arbeitsspeicher
- Verwenden des cachefremden Musters
- Verwenden des Pakets „ServiceStack.Redis“ in einer .NET Core-Konsolenanwendung