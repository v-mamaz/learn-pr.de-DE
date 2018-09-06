Stellen Sie sich folgendes Szenario vor: In einem ausgelasteten Friseursalon tritt immer wieder ein Problem auf: Die Kunden verpassen häufig ihre Termine. Die Termine sind reservierte Zeitfenster. Wenn ein Kunde seinen Termin verpasst, verliert der Salon Geld. Um dieses Problem zu beheben, wendet der Salon sich an Sie als Softwareentwickler. Sie entscheiden, das Problem mittels SMS-Nachrichten zur Erinnerung zu lösen. Jeden Morgen senden Sie eine Textnachricht an jeden Kunden, der an diesem Tag einen Termin hat.

Als Azure-Entwickler entscheiden Sie sich, zur Lösung dieses Problems eine Azure-Funktion zu verwenden. Sie wissen bereits, wie Sie die Logik zum Senden einer Textnachricht implementieren. Nun müssen Sie lernen, die Nachricht zu einem bestimmten Zeitpunkt zu senden. Glücklicherweise unterstützt Azure Functions eine Funktion namens _triggers_. Mit Triggern wird bestimmt, wie eine Azure-Funktion ausgeführt wird.

## <a name="learning-objectives"></a>Lernziele
In diesem Modul lernen Sie Folgendes:

- Bestimmen des Triggers, der sich am besten für Ihre geschäftlichen Anforderungen eignet
- Erstellen Sie einen Trigger mit Timer, um eine Funktion nach einem konsistenten Zeitplan aufzurufen.
- Erstellen Sie einen HTTP-Trigger, um eine Funktion bei Empfang einer HTTP-Anforderung aufzurufen.
- Erstellen Sie einen Blobtrigger, um eine Funktion aufzurufen, wenn ein Blob in Azure Storage erstellt oder aktualisiert wird.
