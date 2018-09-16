Angenommen, Sie erstellen eine mobile Instant Messaging-Anwendung. Ihre Anwendung ermöglicht es Benutzern, Nachrichten an alle Mitglieder einer bestimmten benutzerdefinierten Gruppe zu senden. Es gibt einige Daten, die zu jedem Benutzer gespeichert werden müssen, etwa der Benutzername, die E-Mail-Adresse und das Kennwort. Sie entscheiden sich also dafür, SQL Server zu verwenden, um eine relationale Datenbank für diese Informationen zu erstellen. Allerdings müssen die Nachrichten selbst schnell gesendet werden und schnellen Zugriff ermöglichen, und eine relationale Datenbank ist dafür zu langsam.

Aufgrund der vielfältigen Vorteile, die er bereitstellt, beschließen Sie, einen Redis Cache zu erstellen. Beispielsweise können Sie Transaktionen verwenden, um sicherzustellen, dass eine Nachricht, die ein Bild und Text enthält, zusammen gesendet wird. Sie verwenden Datenablauf, um den Namen des Gruppenchats nach einer Stunde zurückzusetzen. Schließlich verwenden Sie Entfernungsrichtlinien, um sicherzustellen, dass die ältesten Nachrichten zuerst gelöscht werden, wenn der Speicher knapp wird.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:
- Gruppieren mehrerer Vorgänge in einer Transaktion
- Festlegen einer Ablaufzeit für Ihre Daten
- Verwalten von Bedingungen des Typs „Nicht genügend Arbeitsspeicher“
- Verwenden des cachefremden Musters


