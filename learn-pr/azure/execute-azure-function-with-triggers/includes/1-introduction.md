Stellen Sie sich folgendes Szenario vor: In einem ausgelasteten Friseursalon tritt immer wieder ein Problem auf: Die Kunden verpassen häufig ihre Termine. Die Termine sind reservierte Zeitfenster. Wenn ein Kunde seinen Termin verpasst, verliert der Salon Geld. Um dieses Problem zu beheben, wendet der Salon sich an Sie als Softwareentwickler. Sie entscheiden, das Problem mittels SMS-Nachrichten zur Erinnerung zu lösen. Dies konnte gesendet werden, sobald der Termin geplant ist oder geändert, und jeden Morgen, müssen Sie eine Textnachricht an jeder Kunde mit diesem Tag Terminen senden.

Sie müssen einen Dienst zu erstellen, der problemlos geplant, aktualisiert und skaliert werden können. Möchten Sie dieses Problem mithilfe einer Funktionen-app zu beheben. Sie wissen bereits, wie Sie die Logik zum Senden einer Textnachricht implementieren. Nun Sie erfahren, wie Sie die Nachricht zu einem bestimmten Zeitpunkt zu senden müssen, oder wenn ein bestimmtes Ereignis auftritt. Glücklicherweise unterstützt Azure Functions eine Funktion namens _triggers_. Mit Triggern wird bestimmt, wie eine Azure-Funktion ausgeführt wird.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:
- Bestimmen des Triggers, der sich am besten für Ihre geschäftlichen Anforderungen eignet
- Erstellen eines Zeitgebertriggers, um eine Funktion nach einem konsistenten Zeitplan aufzurufen
- Erstellen eines HTTP-Triggers, um eine Funktion bei Empfang einer HTTP-Anforderung aufzurufen
- Erstellen eines Blobtriggers, um eine Funktion aufzurufen, wenn ein Blob in Azure Storage erstellt oder aktualisiert wird