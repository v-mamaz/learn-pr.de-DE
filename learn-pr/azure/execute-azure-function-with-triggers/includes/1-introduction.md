Stellen Sie sich folgendes Szenario vor: In einem ausgelasteten Friseursalon tritt immer wieder ein Problem auf: Die Kunden verpassen häufig ihre Termine. Die Termine sind reservierte Zeitfenster. Wenn ein Kunde seinen Termin verpasst, verliert der Salon Geld. Um dieses Problem zu beheben, wendet der Salon sich an Sie als Softwareentwickler. Sie entscheiden, das Problem mithilfe von SMS-Nachrichten zur Erinnerung zu lösen. Diese können gesendet werden, sobald der Termin geplant oder geändert wird, und jeden Morgen senden Sie eine SMS an jeden Kunden mit einem Termin an diesem Tag.

Sie müssen einen Dienst erstellen, der problemlos geplant, aktualisiert und skaliert werden kann. Sie entscheiden sich, dieses Problem mit einer Funktions-App zu lösen. Sie wissen bereits, wie Sie die Logik zum Senden einer SMS implementieren. Jetzt müssen Sie lernen, wie Sie die Nachricht zu einem bestimmten Zeitpunkt oder beim Eintreten eines bestimmten Ereignisses senden können. Glücklicherweise unterstützt Azure Functions eine Funktion namens _triggers_. Mit Triggern wird bestimmt, wie eine Azure-Funktion ausgeführt wird.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:
- Bestimmen des Triggers, der sich am besten für Ihre geschäftlichen Anforderungen eignet
- Erstellen eines Zeitgebertriggers, um eine Funktion nach einem konsistenten Zeitplan aufzurufen
- Erstellen eines HTTP-Triggers, um eine Funktion bei Empfang einer HTTP-Anforderung aufzurufen
- Erstellen eines Blobtriggers, um eine Funktion aufzurufen, wenn ein Blob in Azure Storage erstellt oder aktualisiert wird