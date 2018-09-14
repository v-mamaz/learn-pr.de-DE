Betrachten wir zunächst einen Blick auf Azure Storage-Dienste, Daten-Stile und -Konten. 

Microsoft Azure Storage ist ein verwalteter Dienst, der stellt dauerhafte, sichere und skalierbaren Speicher, in der Cloud. Schauen wir uns diese Begriffe nach unten.

| | |
|-|-|
| **Durable** | Mit Redundanz wird sichergestellt, dass Ihre Daten sicher sind, falls es zu vorübergehenden Hardwareausfällen kommt. Sie können auch Daten über Rechenzentren oder geografische Regionen für zusätzlichen Schutz vor lokalen Notfällen oder Naturkatastrophen replizieren. Daten, die auf diese Weise repliziert werden, sind bei einem unerwarteten Ausfall weiterhin hoch verfügbar. |
| **Schützen** | Alle Daten, die in Azure Storage geschrieben werden, werden vom Dienst verschlüsselt. Bei Azure Storage können Sie genau steuern, wer Zugriff auf Ihre Daten hat. |
| **Skalierbar** | Azure Storage ist auf hohe Skalierbarkeit ausgelegt, um die Datenspeicherungs- und Leistungsanforderungen heutiger Anwendungen zu erfüllen. |
| **Verwaltet** | Microsoft Azure übernimmt für Sie die Wartung und Behandlung aller kritischen Probleme. |

Ein einzelnes Azure-Abonnement kann bis zu 200 Speicherkonten, hosten, die jeweils 500 TB an Daten aufnehmen kann. Wenn Sie einen Business Case verfügen, können Sie wenden Sie sich an das Azure Storage-Team und Genehmigung für bis zu 250 Speicherkonten in einem Abonnement, die Ihre maximale Speicherkapazität bis zu 125 Petabytes überträgt erhalten.

## <a name="azure-data-services"></a>Azure-Datendienste

Azure Storage umfasst vier Typen von Daten.

- **BLOBs**: ein stark skalierbarer Objektspeicher für Text- und binäre Daten.
- **Dateien**: verwaltete Datei Dateifreigaben für die Cloud oder in lokalen Bereitstellungen.
- **Warteschlangen**: ein messagingspeicher für zuverlässiges messaging zwischen Anwendungskomponenten.
- **Tabellen**: ein NoSQL-Speicher für die schemalose Speicherung von strukturierten Daten. Dieser Dienst wurde ersetzt durch Cosmos DB und wird hier nicht erörtert.

Alle diese Datentypen im Azure-Speicher werden von zugegriffen an einer beliebigen Stelle in der Welt über HTTP oder HTTPS. Microsoft stellt SDKs für Azure-Speicher in einer Vielzahl von Sprachen sowie eine REST-API bereit. Sie können Daten direkt im Azure-Portal auch visuell untersuchen.

### <a name="blob-storage"></a>Blob-Speicher

Azure Blob Storage ist eine Objekt-speicherlösung, die für die Speicherung großer Mengen von unstrukturierten Daten, z.B. Text-oder Binärdaten optimiert. Blobspeicher ist für folgende Zwecke ideal geeignet:

- Speichern von Bildern oder Dokumenten direkt für einen Browser, einschließlich vollständig statischen Websites.
- Speichern von Dateien für verteilten Zugriff
- Streamen von Video und Audio
- Speichern von Daten für Sicherung und Wiederherstellung, notfallwiederherstellung und Archivierung.
- Speichern von Daten für Analysen durch einen lokalen oder von Azure gehosteten Dienst

Azure Storage unterstützt drei Arten von Blobs:

| BLOB-Typ | Beschreibung |
|-----------|-------------|
| **Blockblobs** | Block-Blobs werden verwendet, um Text zu speichern, oder bis zu 5 TB (50.000 Blöcke von 100 MB) der Binärdateien Größe. Der wichtigste Anwendungsfall für Blockblobs ist die Speicherung von Dateien, die von Anfang bis Ende gelesen werden, z.B. Mediendateien oder Imagedateien für Websites. Sie werden blockblobs bezeichnet, da Dateien, die größer als 100 MB als kleine Blöcke müssen, die anschließend konsolidiert hochgeladen werden (in das endgültige Blob oder ein Commit ausgeführt werden). |
| **Seitenblobs** | Seiten-Blobs werden verwendet, um enthalten random-Access-Dateien bis zu 8 TB groß. Seiten-Blobs dienen hauptsächlich als Hintergrundspeicher für die VHDs verwendet, um dauerhafte Datenträger für Azure Virtual Machines (Azure-VMs) bereitzustellen. Sie werden als Seitenblobs bezeichnet, da sie zufälligen Lese-/Schreibzugriff auf 512-Byte-Seiten ermöglichen. |
| **Anfügeblobs** | Fügen Sie Blobs bestehen aus Blöcken wie Block-Blobs, jedoch optimiert sind, für die Anfügevorgänge. Diese werden häufig zum Protokollieren von Informationen aus einer oder mehreren Quellen in der gleichen Blob verwendet. Beispielsweise können Sie aller die Ablaufverfolgung in dasselbe anfügeblob für eine Anwendung auf mehrere virtuelle Computer schreiben. Ein einzelnes Anfügeblob kann eine maximale Größe von 195 GB haben. |

### <a name="files"></a>Dateien

Azure Files ermöglicht Ihnen die Einrichtung hochverfügbarer Netzwerkdateifreigaben, die mithilfe des standardmäßigen Server Message Block (SMB)-Protokolls zugegriffen werden kann. Dies bedeutet, dass mehrere virtuelle Computer die gleichen Dateien mit Lese- und Schreibzugriff verwenden können. Die Dateien können auch mithilfe der REST-Schnittstelle oder mithilfe der Speicherclientbibliotheken gelesen werden. Sie können auch eine eindeutige URL für jede Datei, um einen festgelegten Zeitraum differenzierten Zugriff auf die Datei mit einem privaten ermöglichen zuordnen. Dateifreigaben können in zahlreichen Szenarien verwendet werden:

- Speichern freigegebenen Konfigurationsdateien für virtuelle Computer, Tools oder Dienstprogramme, damit alle Benutzer die gleiche Version verwendet wird.
- Protokolldateien, z. B. Diagnose, Metriken und Absturzabbilder erfasst.
- Gemeinsam verwendeten Daten auf lokale Anwendungen und Azure-VMs, um die Migration von apps in der Cloud über einen Zeitraum zu ermöglichen.

### <a name="queues"></a>Warteschlangen

Der Azure Queue-Dienst wird zum Speichern und Abrufen von Nachrichten verwendet. Warteschlangennachrichten können eine Größe von bis zu 64 KB haben, und eine Warteschlange kann Millionen von Nachrichten enthalten. Warteschlangen dienen im Allgemeinen zum Speichern von Listen mit Nachrichten, die asynchron verarbeitet werden sollen.

Sie können Warteschlangen verwenden, um verschiedene Teile Ihrer Anwendung lose miteinander zu verbinden. Beispielsweise können wir auf die vom Benutzer hochgeladenen Fotos bildverarbeitung. Möglicherweise geben Sie eine Art von gesichtserkennung werden soll, oder Tags-Funktion, so dass es sich bei der Suche nach Personen über alle Images können sie in unserem Dienst gespeichert haben. Wir können Warteschlangen verwenden, um die Nachrichten an unsere Bildverarbeitungsdienst zum Laden, damit sie wissen, dass neue Bilder hochgeladen wurden, und sind bereit für die Verarbeitung übergeben. Diese Art von Architektur können Sie zum Entwickeln und jeder Teil des Diensts unabhängig voneinander aktualisieren.

## <a name="azure-storage-accounts"></a>Azure-Speicherkonten

Um eines dieser Dienste über eine Anwendung zuzugreifen, müssen Sie erstellen eine _Speicherkonto_. Das Storage-Konto bietet es sich um einen eindeutigen Namespace, in Azure speichern und Abrufen Ihrer Datenobjekte. Ein Speicherkonto enthält alle Blobs, Dateien, Warteschlangen, Tabellen und VM-Datenträger, die Sie unter diesem Konto zu erstellen.

### <a name="creating-a-storage-account"></a>Erstellen eines Speicherkontos

Sie können Azure Storage-Konto mithilfe der Azure-Portal, Azure PowerShell oder Azure-Befehlszeilenschnittstelle erstellen. Azure Storage bietet drei verschiedene Kontooptionen jeweils unterschiedliche Preise und Funktionen, die unterstützt werden.

> [!div class="mx-tableFixed"]
> | Kontotyp | Beschreibung |
> |--------------|-------------|
> | **General Purpose v2 (GPv2)** | Konten vom Typ „General Purpose v2 (GPv2)“ unterstützen alle aktuellen Features für Blobs, Dateien, Warteschlangen und Tabellen. Die Preise für GPv2-Konten wurde entwickelt, um die niedrigsten GB-Preise zu übermitteln. |
> | **Allgemein v1 (GPv1)** | Allgemein v1 (GPv1)-Konten bieten Zugriff auf Azure Storage-Dienste, aber möglicherweise nicht die aktuellen Features oder die niedrigsten GB-Preise. Beispielsweise werden die Speicherebenen „Cool“ und „Archiv“ in GPv1 nicht unterstützt. Die Preise für GPv1-Transaktionen sind niedriger, sodass Workloads mit hohen Datenänderungs- oder Leseraten ggf. von der Nutzung dieses Kontotyps profitieren. |
> | **Blob-Speicherkonten** | Einen legacy-Kontotyp, Blob Storage-Konten unterstützen die gleichen Block-BLOB-Features wie GPv2, aber sie sind auf unterstützen nur Block- und anfügeblobs zu ermitteln. Die Preise sind weitestgehend mit den Preisen für allgemeine Konten vom Typ „General Purpose v2“ identisch. |

Wenn Sie möchten mehr über das Erstellen von Speicherkonten, stellen Sie sicher, durchlaufen die **erstellen Sie ein Azure Storage-Konto** -Modul in das Lernportal.