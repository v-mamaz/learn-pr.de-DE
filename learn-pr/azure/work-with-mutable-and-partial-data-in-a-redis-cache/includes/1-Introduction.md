Angenommen Sie, Sie erstellen ein Instant messaging-Verwaltungsrichtlinie für mobile Anwendungen. Ihre Anwendung ermöglicht das Senden von Nachrichten an alle Mitglieder einer bestimmten benutzerdefinierten Gruppe. Es gibt einige Daten, die über jeden Benutzer, wie Sie ihren Benutzernamen, e-Mail-Adresse und Kennwort gespeichert werden soll. Möchten Sie SQL Server verwenden, um eine relationale Datenbank Informationen zu erstellen. Allerdings müssen die Nachrichten selbst gesendet und schnell zugegriffen werden, und eine relationale Datenbank, zu langsam ist.

Sie beschließen, einen Azure Redis Cache aufgrund der Anzahl von Vorteilen zu erstellen, die es bereitstellt. Beispielsweise werden Sie Transaktionen verwenden, um sicherzustellen, dass eine Nachricht mit einem Bild und Text zusammen gesendet werden. Ablauf von Daten verwenden den Namen der Gruppenchat nach einer Stunde zurückgesetzt. Abschließend verwenden Sie entfernungsrichtlinien, um sicherzustellen, dass die ältesten Nachrichten, wenn Sie nicht genügend Speicher auf werden zuerst gelöscht werden.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Mehrere Vorgänge in einer Transaktion gruppieren
- Festlegen Sie eine Ablaufzeit, auf Ihre Daten
- Out-of-Memory-Bedingungen verwalten
- Verwenden Sie das Cache-Aside-Muster
