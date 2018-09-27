Eine Azure-Funktions-App wird erst ausgeführt, wenn sie dazu aufgefordert wird. Beispielsweise konnten Sie eine Azure-Funktion erstellen, die vor einem Termin eine Erinnerungs-SMS an die Kunden versendet. Wenn wir der Funktion nicht mitteilen, wann sie ausgeführt werden soll, werden unsere Kunden nie eine Meldung empfangen. 

Hier untersuchen Sie Trigger auf hoher Ebene sowie die am häufigsten verwendeten Typen von Triggern.

## <a name="what-is-a-trigger"></a>Was ist ein Trigger?

Ein Trigger ist ein Objekt, das definiert, wie eine Azure-Funktion aufgerufen wird. Wenn Sie z.B. möchten, dass eine Funktion alle 10 Minuten ausgeführt wird, können Sie einen Timertrigger verwenden.

Jeder Funktion muss exakt ein Trigger zugeordnet sein. Wenn Sie einen Logikabschnitt unter mehreren Bedingungen ausführen möchten, müssen Sie mehrere Funktionen erstellen, die den gleichen grundlegenden Funktionscode verwenden.

In diesem Modul konzentrieren wir uns auf die Triggertypen **Timer**, **HTTP** und **Blob**.

## <a name="types-of-triggers"></a>Triggertypen

Azure Functions unterstützt eine Vielzahl von Triggertypen. Diese Typen sind am gängigsten:

| Typ | Zweck |
| --- | --- |
| **Zeitgeber** | Eine Funktion wird in einem festgelegten Intervall ausgeführt. |
| **HTTP** | Eine Funktion wird bei Empfang einer HTTP-Anforderung ausgeführt. |
| **Blob** | Eine Funktion wird ausgeführt, wenn eine Datei in Azure Blob Storage hochgeladen oder aktualisiert wird. |
| **Warteschlange** | Eine Funktion wird ausgeführt, wenn eine Nachricht einer Azure Storage-Warteschlange hinzugefügt wird. |
| **Cosmos DB** | Eine Funktion wird ausgeführt, wenn sich ein Dokument in einer Sammlung ändert. |
| **Event Hub** | Eine Funktion wird ausgeführt, wenn ein Event Hub ein neues Ereignis empfängt. |

## <a name="what-is-a-binding"></a>Was ist eine Bindung?

Eine Bindung ist eine Verbindung mit Daten in Ihrer Funktion. Bindungen sind optional und können in Form von Eingabe- und Ausgabebindungen auftreten. Eine Eingabebindung entspricht den Daten, die Ihre Funktion empfängt. Eine Ausgabebindung entspricht den Daten, die Ihre Funktion sendet.

Im Gegensatz zu einem Trigger kann eine Funktion mehrere Eingabe- und Ausgabebindungen haben.

In der nächsten Übung führen Sie eine Funktion nach einem Zeitplan mithilfe eines Timertriggers aus.