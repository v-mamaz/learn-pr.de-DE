Nehmen wir an, Sie seien Fotograf und besäßen eine Website, auf denen Sie Ihre Bilder des Tages anzeigen. Weil Sie sehr beschäftigt sind, haben Sie keinen konsistenten Uploadzeitplan, aber Sie möchten Ihren Fans mitteilen, wann Sie ein Bild hochladen. Sie entscheiden, eine Azure-Funktion zu erstellen, um automatisch einen Tweet zu senden, wenn Sie ein Bild in Ihren Azure Storage-Blobcontainer hochladen.

Hier erfahren Sie, wie Sie einen Blobtrigger erstellen, und ihn anweisen, einen bestimmten Speicherort in Ihrem Azure Storage-Blobcontainer zu überwachen.

## <a name="what-is-azure-storage"></a>Was ist Azure Storage?

Azure Storage ist die Cloudspeicherlösung von Microsoft, die alle Arten von Daten einschließlich Blobs, Warteschlangen und NoSQL unterstützt. Das Ziel von Azure Storage ist, Datenspeicher mit folgenden Eigenschaften bereitzustellen:

- Hoch verfügbar
- Sicher
- Skalierbar
- Verwaltet

Wir werden uns nicht zu intensiv mit Azure Storage beschäftigen. Stattdessen verwenden wir Azure Storage zum Erstellen von Blobs, die die Ausführung unserer Funktion auslösen.

## <a name="what-is-azure-blob-storage"></a>Was ist Azure-Blobspeicher?

Azure-Blobspeicher ist eine Objektspeicherlösung, die zum Speichern großer Mengen unstrukturierter Daten entworfen wurde. 

Azure Blob Storage eignet sich z.B. hervorragend für folgende Aufgaben:

- Speichern von Dateien
- Bereitstellen von Dateien
- Video- und Audiostreaming
- Protokollieren von Daten

Es gibt drei Arten von Blobs: **Blockblobs**, **Anfügeblobs** und **Seitenblobs**. Blockblobs sind der gängigste Typ. Dort können Sie Text- oder Binärdaten effizient speichern. Anfügeblobs sind wie Blockblobs, aber sie eignen sich eher für Anfügevorgänge wie das Erstellen einer Protokolldatei, die ständig aktualisiert wird. Seitenblobs bestehen aus Seiten und sind für häufige wahlfreie Lese-/Schreibzugriffe vorgesehen.

## <a name="what-is-a-blob-trigger"></a>Was ist ein Blobtrigger?

Ein Blobtrigger führt eine Funktion aus, wenn eine Datei in Azure-Blobspeicher hochgeladen oder aktualisiert wird. Um einen Blobtrigger zu erstellen, müssen Sie ein Azure Storage-Konto erstellen und einen Speicherort angeben, den der Trigger überwacht.

## <a name="how-to-create-a-blob-trigger"></a>Gewusst wie: Erstellen eines Blobtriggers

Genau wie die anderen Trigger, die wir bisher kennengelernt haben, erstellen wir einen Blobtrigger im Azure-Portal. Wählen Sie in Ihrer Azure-Funktion **Blobtrigger** aus der Liste der vordefinierten Triggertypen aus. Geben Sie dann die Logik ein, die beim Erstellen oder Aktualisieren eines Blobs ausgeführt wird.

Eine Einstellung, die Sie beachten sollten, ist der **Pfad**. Der **Pfad** weist den Blobtrigger an, wo er überwachen soll, ob ein Blob hochgeladen oder aktualisiert wird. Standardmäßig ist der Wert **Pfad** festgelegt auf: 

> samples-workitems/{Name}

Wir unterteilen dieses Konzept in zwei Teile: *samples-workitems* und *{Name}*. Der erste Teil, *samples-workitems*, stellt den Blobcontainer dar, den der Trigger überwacht. Der zweite Teil, *{Name}, bedeutet, dass jeder Dateityp den Trigger veranlasst, die Funktion aufzurufen. Die Funktion wird aufgerufen, da kein Filter vorhanden ist. Beispielsweise lässt sich mithilfe der folgenden Syntax einstellen, dass der Trigger die Funktion nur aufruft, wenn eine PNG-Datei hinzugefügt wird:

> samples-workitems/{Name}.png

Die letzte wichtige Information in diesem Konzept ist der Text *Name*. Der *Name* stellt einen Parameter in Ihrer Azure-Funktion dar, der den Namen der hinzugefügten Datei empfängt. Wenn ich z.B. eine Datei namens *resume.txt* hochlade, empfängt meine Azure-Funktion diesen Wert als Zeichenfolge über einen Parameter namens *Name*.

## <a name="summary"></a>Zusammenfassung

Ein Blobtrigger ruft eine Azure-Funktion auf, wenn er Aktivität an einem bestimmten Speicherort in Ihrem Azure-Blobspeicherkonto feststellt. Sie legen den zu überwachenden Speicherort durch Ändern des Werts **Pfad** im Azure-Portal fest.
