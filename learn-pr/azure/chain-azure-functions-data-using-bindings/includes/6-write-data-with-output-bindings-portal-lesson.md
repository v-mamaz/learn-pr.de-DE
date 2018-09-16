Ähnlich wie bei Eingabebindungen sind mehrere Typen von Ausgabebindungen vorhanden.

Es gibt mehrere Typen von Ausgabebindungen, jedoch nicht alle Typen unterstützen sowohl Ein- als auch Ausgabe. Sie können sie immer dann verwenden, wenn Sie Daten senden oder speichern möchten. Hier untersuchen wir die Typen, die Ausgabebindungen unterstützen, und die Frage, wann sie verwendet werden.

## <a name="output-binding-types"></a>Ausgabebindungstypen

- **Blobspeicher**: Sie können die Blobausgabebindung verwenden, um Blobs zu schreiben.

- **Azure Cosmos DB**: Die Azure Cosmos DB-Ausgabebindung ermöglicht das Schreiben eines neuen Dokuments in eine Azure Cosmos DB-Datenbank mithilfe der SQL-API.

- **Event Hubs**: Mit der Event Hubs-Ausgabebindung werden Ereignisse in einen Ereignisdatenstrom geschrieben. Um Ereignisse in einen Event Hub schreiben zu können, müssen Sie über Sendeberechtigungen verfügen.

- **HTTP**: Verwenden Sie die HTTP-Ausgabebindung, um eine Antwort an den Absender der HTTP-Anforderung zu senden. Diese Bindung erfordert einen HTTP-Trigger und ermöglicht Ihnen, die Antwort, die der Anforderung des Triggers zugeordnet ist, benutzerdefiniert anzupassen.

- **Microsoft Graph**: Microsoft Graph-Ausgabebindungen ermöglichen es Ihnen, in OneDrive in Dateien zu schreiben, Excel-Daten zu ändern und E-Mail-Nachrichten über Outlook zu senden.

- **Mobile Apps**: Die Mobile Apps-Ausgabebindung schreibt einen neuen Datensatz in eine Mobile Apps-Tabelle.

- **Notification Hubs**: Mit Notification Hubs-Ausgabebindungen können Sie Pushbenachrichtigungen senden.

- **Queue Storage**: Verwenden Sie die Azure Queue Storage-Ausgabebindung, um Nachrichten in eine Warteschlange zu schreiben.

- **SendGrid**: Senden Sie E-Mail-Nachrichten über SendGrid-Bindungen.

- **Service Bus**: Verwenden Sie die Azure Service Bus-Ausgabebindung zum Senden von Warteschlangen- oder Themanachrichten.

- **Table Storage**: Verwenden Sie eine Azure Table Storage-Ausgabebindung, um in eine Tabelle in einem Azure Storage-Konto zu schreiben.

- **Twilio**: Senden Sie Textnachrichten mit Twilio.

- **Webhooks**: Verwenden Sie die HTTP-Ausgabebindung, um eine Antwort an den Absender der HTTP-Anforderung zu senden. Diese Bindung erfordert einen HTTP-Trigger und ermöglicht Ihnen, die Antwort, die der Anforderung des Triggers zugeordnet ist, benutzerdefiniert anzupassen.


## <a name="how-to-create-an-output-binding"></a>Wie wird eine Ausgabebindung erstellt?
Um eine Bindung als eine Ausgabe zu definieren, müssen Sie die `direction` als `out` definieren.
Die Parameter für jeden Typ von Bindung können unterschiedlich sein. Diese sind in der [Dokumentation von Microsoft](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings) gut dokumentiert.

## <a name="combining-input-and-output-bindings"></a>Kombinieren von Eingabe- und Ausgabebindungen 
Es ist möglich, mehrere Bindungen auf eine einzelne Funktion anzuwenden. Auf diese Weise können Sie sowohl Eingabe- als auch Ausgabebindungen definieren.

Und bei der Eingabe und der Ausgabe kann es sich sogar um den gleichen Bindungstyp handeln...