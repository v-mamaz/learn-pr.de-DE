Angenommen, Sie planen die Architektur einer Anwendung für den Austausch von Musik. Sie möchten sicherstellen, dass Musikdateien zuverlässig von der mobilen App in die Web-API hochgeladen werden.

Da diese Kommunikation eine Nachricht ist, müssen Sie auswählen, ob Sie Azure Storage-Warteschlangen oder den Service Bus verwenden. Mit beidem können Sie Nachrichtenwarteschlangen speichern, während sie auf die Verarbeitung warten.

## <a name="delivery-guarantees"></a>Übermittlungsgarantie

Warteschlangensysteme garantieren in der Regel die Übermittlung jeder Nachricht in der Warteschlange an eine Zielkomponente. Allerdings können dabei unterschiedliche Ansätze verfolgt werden:

- **At-Least-Once-Übermittlung** Bei diesem Ansatz wird jede Nachricht an mindestens eine der Komponenten übermittelt, die Nachrichten aus der Warteschlange abrufen. Unter Umständen ist es jedoch möglich, dass dieselbe Nachricht mehrfach übermittelt wird. Wenn beispielsweise zwei Instanzen einer Webanwendung Nachrichten aus einer Warteschlange abrufen, geht jede Nachricht in der Regel nur an eine dieser Instanzen. Wenn eine Instanz jedoch lange zum Verarbeiten der Nachrichten braucht, und ein Timeout abläuft, wird die Nachricht ggf. an die andere Instanz gesendet. Behalten Sie diese Möglichkeit im Hinterkopf, wenn Sie Ihren Web-App-Code entwickeln.
- **At-Most-Once-Übermittlung** Bei diesem Ansatz wird nicht garantiert, dass jede Nachricht übermittelt wird. Es besteht die sehr geringe Wahrscheinlichkeit, dass eine Nachricht nicht ankommt. Allerdings kann es nicht vorkommen, dass Nachrichten doppelt übermittelt werden wie bei der maximal einmaligen Übermittlung.
- **First In, First Out (FIFO)** In den meisten Messaging-Systemen verlassen Nachrichten die Warteschlange in der Regel in der Reihenfolge, in der sie hinzugefügt wurden. Allerdings sollten Sie überprüfen, ob diese Reihenfolge eingehalten wird. Wenn Ihre verteilte Anwendung verlangt, dass die Nachrichten in der richtigen Reihenfolge verarbeitet werden, müssen Sie ein Warteschlangensystem mit FIFO-Garantie auswählen.

## <a name="transactions"></a>Transaktionen

Einige eng verwandte Nachrichtengruppen können Probleme verursachen, wenn die Übermittlung einer Nachricht in der Gruppe fehlschlägt.

Nehmen Sie als Beispiel eine E-Commerce-Anwendung. Wenn der Benutzer auf die Schaltfläche „Kaufen“ klickt, wird eine Nachricht mit den Bestelldaten zusammen mit einer Nachricht mit den Kreditkartendaten gesendet. Wenn die Nachricht mit den Kreditkartendaten nicht zugestellt wird, wird die Bestellung ggf. ohne Bezahlung versendet.

Solche Probleme können Sie vermeiden, indem Sie die beiden Nachrichten in einer Transaktion zusammenfassen. Wenn Transaktionen erfolgreich sind oder fehlschlagen, dann als ganze Einheit. Wenn die Übermittlung der Kreditkartendaten fehlschlägt, gilt dasselbe für die Nachricht mit der Bestellung.

## <a name="when-to-use-storage-queues"></a>Verwenden von Storage-Warteschlangen

Warteschlangen werden für Nachrichten verwendet – nicht für Ereignisse.

Azure Storage-Konten umfassen Warteschlangen, die verteilte Anwendungen als einfache temporäre Speicherorte für Nachrichten verwenden können. Eine Quellkomponente kann der Warteschlange eine Nachricht hinzufügen. Zielkomponenten rufen die Nachricht am Anfang der Warteschlange zur Verarbeitung ab. Solchen Warteschlangen erhöhen die Zuverlässigkeit des Nachrichtenaustauschs, da in Zeiten hoher Nachfrage Nachrichten einfach warten können, bis eine Zielkomponente bereit ist, sie zu verarbeiten.

Warteschlangen werden auch im Rahmen von Azure Service Bus-Messaging bereitgestellt. Wenn Sie eine Warteschlange in Azure für eine bestimmte Kommunikation verwenden möchten, haben Sie die Wahl zwischen einer Storage- und einer Service Bus-Warteschlange.

Berücksichtigen Sie bei der Entscheidungsfindung die folgenden Fragen:

- Benötigen Sie eine At-Most-Once-Übermittlungsgarantie?
- Benötigen Sie eine FIFO-Garantie?
- Müssen Sie Nachrichten zu Transaktionen gruppieren?
- Müssen Sie Nachrichten speichern, die größer als 64 KB sind?

Wenn Sie mindestens eine Frage mit „Ja“ beantwortet haben, entscheiden Sie sich für eine Service Bus-Warteschlange.

Beachten Sie darüber hinaus diese Aspekte:

- Benötigen Sie serverseitige Protokolle aller Nachrichten, die die Warteschlange passieren?
- Gehen Sie davon aus, dass die Größe der Warteschlange 80 GB überschreitet?

Wenn Sie mindestens eine Frage mit „Ja“ beantwortet haben, entscheiden Sie sich für eine Storage-Warteschlange.

## <a name="summary"></a>Zusammenfassung

Eine Warteschlange ist ein einfacher temporärer Speicherort für Nachrichten, die zwischen Komponenten einer verteilten Anwendung gesendet werden. Mit Warteschlangen können Sie Nachrichten organisieren und unvorhersehbare Nachfragespitzen bewältigen.

Verwenden Sie Azure Storage-Warteschlangen, wenn Sie ein einfaches und leicht zu codierendes Warteschlangensystem wünschen. Nutzen Sie für anspruchsvollere Anforderungen Azure Service Bus-Warteschlangen.