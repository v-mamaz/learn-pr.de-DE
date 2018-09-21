Für Ausgabebindungen sind ebenso wie für Eingabebindungen mehrere Bindungstypen vorhanden. Nicht alle Typen unterstützen allerdings sowohl Ein- als auch Ausgaben. Sie verwenden Ausgabebindungen immer dann, wenn Sie Daten senden oder speichern möchten. Hier untersuchen wir die Typen, die Ausgabebindungen unterstützen, und die Frage, wann sie verwendet werden.

## <a name="output-binding-types"></a>Ausgabebindungstypen

- **Blob Storage:** Sie können die Blobausgabebindung verwenden, um Blobs zu schreiben.

- **Cosmos DB:** Die Azure Cosmos DB-Ausgabebindung ermöglicht das Schreiben eines neuen Dokuments in eine Azure Cosmos DB-Datenbank mithilfe der SQL-API.

- **Event Hubs:** Mit der Event Hubs-Ausgabebindung werden Ereignisse in einen Ereignisdatenstrom geschrieben. Sie müssen über Sendeberechtigungen verfügen, um Ereignisse in einen Event Hub schreiben zu können.

- **HTTP:** Verwenden Sie die HTTP-Ausgabebindung, um eine Antwort an den Absender der HTTP-Anforderung zu senden. Diese Bindung erfordert einen HTTP-Trigger und ermöglicht es Ihnen, die Antwort anzupassen, die der Anforderung des Triggers zugeordnet ist. Dadurch kann auch eine Verbindung mit Webhooks hergestellt werden.

- **Microsoft Graph:** Microsoft Graph-Ausgabebindungen ermöglichen es Ihnen, in OneDrive in Dateien zu schreiben, Excel-Daten zu ändern und E-Mail-Nachrichten über Outlook zu senden.

- **Mobile Apps:** Die Mobile Apps-Ausgabebindung schreibt einen neuen Datensatz in eine Mobile Apps-Tabelle.

- **Notification Hubs:** Mit Notification Hubs-Ausgabebindungen können Sie Pushbenachrichtigungen senden.

- **Queue Storage:** Verwenden Sie die Azure Queue Storage-Ausgabebindung, um Nachrichten in eine Warteschlange zu schreiben.

- **SendGrid:** Senden Sie E-Mails über SendGrid-Bindungen.

- **Service Bus:** Verwenden Sie die Azure Service Bus-Ausgabebindung zum Senden von Warteschlangen- oder Themanachrichten.

- **Table Storage:** Verwenden Sie eine Azure Table Storage-Ausgabebindung, um in eine Tabelle in einem Azure Storage-Konto zu schreiben.

- **Twilio:** Senden Sie SMS mit Twilio.

Sie müssen `direction` als `out` definieren, um eine Bindung als Ausgabe zu erstellen. Die Parameter für die unterschiedlichen Bindungstypen können variieren.

## <a name="combining-input-and-output-bindings"></a>Kombinieren von Eingabe- und Ausgabebindungen 

Es ist möglich, mehrere Bindungen auf eine einzelne Funktion anzuwenden. Dadurch können Sie sowohl Eingabe- als auch Ausgabebindungen definieren, und die Eingabe und Ausgabe kann sogar den gleichen Bindungstyp aufweisen.