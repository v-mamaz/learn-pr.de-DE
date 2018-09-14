Ähnlich wie Bindungen zu geben, es gibt mehrere Typen von ausgabebindungen.

Es gibt mehrere Typen von ausgabebindungen, jedoch nicht alle Typen unterstützt sowohl ein- und Ausgabe. Sie verwenden diese, wann immer Sie möchten, senden oder Speichern von Daten. Hier ist betrachten die Typen wir, die ausgabebindungen und deren Verwendung unterstützen.

## <a name="output-binding-types"></a>Ausgabe Bindungstypen

- **BLOB-Speicher** können Sie die Blob-ausgabebindung auf um Blobs zu schreiben.

- **COSMOS DB** der Azure Cosmos DB ausgeben Bindung können Sie ein neues Dokument mit einer Azure Cosmos DB-Datenbank mithilfe der SQL-API zu schreiben.

- **Event Hubs** verwenden Sie die Event Hubs-ausgabebindung werden Ereignisse in einen ereignisdatenstrom geschrieben. Um Ereignisse in einen Event Hub schreiben zu können, müssen Sie über eine Sendeberechtigung verfügen.

- **HTTP** verwenden, die die HTTP-ausgabebindung, um an den Absender der HTTP-Anforderung zu reagieren. Diese Bindung erfordert einen HTTP-Trigger und ermöglicht Ihnen, die Antwort, die der Anforderung des Triggers zugeordnet ist, benutzerdefiniert anzupassen.

- **Microsoft Graph** Microsoft Graph-ausgabebindungen ermöglichen Ihnen, Dateien in OneDrive zu schreiben, ändern die Excel-Daten und senden Sie eine e-Mail über Outlook.

- **Mobile Apps** das Mobile Apps-Ausgabe Bindung schreibt einen neuen Datensatz in einer Mobile Apps-Tabelle.

- **Notification Hubs** Senden von Pushbenachrichtigungen mit Notification Hubs-ausgabebindungen.

- **Warteschlangenspeicher** verwenden die Azure Queue Storage-ausgabebindung zum Schreiben von Nachrichten an eine Warteschlange.

- **Senden Sie Raster** Senden per e-Mail über SendGrid-Bindungen.

- **Service Bus** verwendet Azure Service Bus-ausgabebindung zum Senden von Warteschlangen-oder themanachrichten.

- **Tabellenspeicher** mithilfe eine Azure Table Storage-ausgabebindung in einer Tabelle in Azure Storage-Konto geschrieben.

- **Twilio** Twilio SMS-Nachrichten zu senden.

- **Webhooks** verwenden, die die HTTP-ausgabebindung, um an den Absender der HTTP-Anforderung zu reagieren. Diese Bindung erfordert einen HTTP-Trigger und ermöglicht Ihnen, die Antwort, die der Anforderung des Triggers zugeordnet ist, benutzerdefiniert anzupassen.

## <a name="how-to-create-an-output-binding"></a>Vorgehensweise: Erstellen Sie eine ausgabebindung?
Um eine Bindung definieren eine Eingabe, müssen Sie definieren die `direction` als `out`.
Die Parameter für jeden Typ der Bindung können abweichen, diese sind gut dokumentiert [Microsoft Dokumentation](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)

## <a name="combining-input-and-output-bindings"></a>Kombinieren von Eingabe- und ausgabebindungen 
Es ist möglich, mehrere Bindungen für eine einzelne Funktion gelten. Dadurch können Sie sowohl Eingabe- und ausgabebindungen zu definieren.

Und die Eingabe und Ausgabe kann dem gleichen Bindungstyp...