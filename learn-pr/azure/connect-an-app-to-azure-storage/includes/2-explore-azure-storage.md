Zunächst werfen wir einen kurzen Blick auf die Azure-Speicherdienste, -Datenformate und -Konten. 

Microsoft Azure Storage ist ein verwalteter Dienst, der die permanente, sichere und skalierbare Speicherung in der Cloud ermöglicht. Diese Begriffe werden nun einzeln beschrieben.

| | |
|-|-|
| **Permanent** | Mithilfe von Redundanz wird sichergestellt, dass Ihre Daten sicher sind, falls es zu vorübergehenden Hardwareausfällen kommt. Sie können Daten auch über Rechenzentren oder geografische Regionen hinweg replizieren, um eine weitere Schutzebene vor lokalen Notfällen oder Naturkatastrophen zu schaffen. Daten, die auf diese Weise repliziert werden, sind bei einem unerwarteten Ausfall weiterhin hoch verfügbar. |
| **Sicher** | Alle Daten, die in Azure Storage geschrieben werden, werden vom Dienst verschlüsselt. Bei Azure Storage können Sie genau steuern, wer Zugriff auf Ihre Daten hat. |
| **Skalierbar** | Azure Storage ist auf hohe Skalierbarkeit ausgelegt, um die Datenspeicherungs- und Leistungsanforderungen heutiger Anwendungen zu erfüllen. |
| **Verwaltet** | Microsoft Azure übernimmt für Sie die Wartung und Behandlung aller kritischen Probleme. |

Unter einem einzelnen Azure-Abonnement können bis zu 200 Speicherkonten gehostet werden, die jeweils bis zu 500 TB an Daten enthalten können. Wenn Sie über einen Business Case verfügen, können Sie sich an das Azure Storage-Team wenden und die Genehmigung für bis zu 250 Speicherkonten unter einem Abonnement einholen. Der maximale Speicher erhöht sich hierdurch auf bis zu 125 Petabyte!

## <a name="azure-data-services"></a>Azure-Datendienste

Azure Storage umfasst vier Typen von Daten.

- **Blobs**: Ein extrem skalierbarer Objektspeicher für Text- und Binärdaten.
- **Files**: Verwaltete Dateifreigaben für Bereitstellungen lokal oder in der Cloud.
- **Warteschlangen**: Ein Messagingspeicher für zuverlässiges Messaging zwischen Anwendungskomponenten.
- **Tables**: Ein NoSQL-Speicher für die schemalose Speicherung von strukturierten Daten. Dieser Dienst wurde durch Cosmos DB ersetzt und wird hier nicht beschrieben.

Auf alle diese Datentypen kann in Azure Storage von jedem Ort der Welt aus per HTTP oder HTTPS zugegriffen werden. Microsoft stellt SDKs für Azure Storage in verschiedenen Sprachen sowie eine REST-API bereit. Sie können Ihre Daten auch direkt im Azure-Portal visuell erkunden.

### <a name="blob-storage"></a>Blobspeicher
Azure-Blobspeicher ist eine Objektspeicherlösung, die für die Speicherung großer Mengen von unstrukturierten Daten, z.B. Text oder Binärdaten, optimiert ist. Blobspeicher ist für folgende Zwecke ideal geeignet:

- Bereitstellen von Bildern oder Dokumenten direkt in einem Browser, einschließlich vollständiger statischer Websites
- Speichern von Dateien für verteilten Zugriff
- Video- und Audio-Streaming
- Speichern von Daten für Sicherung und Wiederherstellung, Notfallwiederherstellung und Archivierung
- Speichern von Daten für Analysen durch einen lokalen oder von Azure gehosteten Dienst

Azure Storage unterstützt drei Arten von Blobs:

| Blobtyp | Beschreibung |
|-----------|-------------|
| **Blockblobs** | Blockblobs werden für Text- oder Binärdateien mit einer Größe von bis zu 5 TB (50.000 Blöcke mit 100 MB) verwendet. Der wichtigste Anwendungsfall für Blockblobs ist die Speicherung von Dateien, die von Anfang bis Ende gelesen werden, z.B. Mediendateien oder Imagedateien für Websites. Sie werden als Blockblobs bezeichnet, weil Dateien, die größer als 100 MB sind, als kleine Blöcke hochgeladen werden müssen, die dann zu einem endgültigen Blob zusammengefasst (committet) werden. |
| **Seitenblobs** | Seitenblobs werden für Random-Access-Dateien mit einer Größe von bis zu 8 TB verwendet. Seitenblobs werden hauptsächlich als Hintergrundspeicher für die VHDs verwendet, die zum Bereitstellen von dauerhaften Datenträgern für Azure Virtual Machines (Azure VMs) genutzt werden. Sie werden als Seitenblobs bezeichnet, da sie zufälligen Lese-/Schreibzugriff auf 512-Byte-Seiten ermöglichen. |
| **Anfügeblobs** | Anfügeblobs bestehen wie Blockblobs auch aus Blöcken, aber sie sind für Anfügevorgänge optimiert. Diese werden häufig eingesetzt, um Informationen aus mindestens einer Quelle in demselben Blob zu protokollieren. Beispielsweise können Sie die gesamte Protokollierung der Ablaufverfolgung für eine Anwendung, die auf mehreren VMs ausgeführt wird, in dasselbe Anfügeblob schreiben. Ein einzelnes Anfügeblob kann eine maximale Größe von 195 GB haben. |

### <a name="files"></a>Files
Azure Files ermöglicht die Einrichtung hochverfügbarer Netzwerkdateifreigaben, auf die über das standardmäßige SMB-Protokoll (Server Message Block) zugegriffen werden kann. Dadurch können mehrere virtuelle Computer gemeinsam die gleichen Dateien mit Lese- und Schreibzugriff nutzen. Die Dateien können auch mithilfe der REST-Schnittstelle oder mithilfe der Speicherclientbibliotheken gelesen werden. Sie können eine eindeutige URL auch einer beliebigen Datei zuordnen, um für einen festgelegten Zeitraum den präzisen Zugriff auf eine private Datei zu ermöglichen. Dateifreigaben können in zahlreichen Szenarien verwendet werden:

- Speichern von freigegebenen Konfigurationsdateien für VMs, Tools oder Hilfsprogramme, damit alle Benutzer die gleiche Version verwenden
- Protokollieren von Dateien, z.B. Diagnose, Metriken und Absturzabbilder
- Freigeben von Daten zwischen lokalen Anwendungen und virtuellen Azure-Computern, um die Migration von Apps in die Cloud für einen bestimmten Zeitraum zuzulassen

### <a name="queues"></a>Warteschlangen
Der Azure-Warteschlangendienst wird zum Speichern und Abrufen von Nachrichten verwendet. Warteschlangennachrichten können eine Größe von bis zu 64 KB haben, und eine Warteschlange kann Millionen von Nachrichten enthalten. Warteschlangen dienen im Allgemeinen zum Speichern von Listen mit Nachrichten, die asynchron verarbeitet werden sollen.

Sie können Warteschlangen verwenden, um unterschiedliche Teile Ihrer Anwendung lose zu verknüpfen. Beispielsweise können Sie die Bildverarbeitung für die Fotos durchführen, die von Ihren Benutzern hochgeladen werden. Es kann sein, dass Sie die Gesichtserkennung oder eine Markierungsfunktion bereitstellen möchten, damit die Benutzer alle Bilder durchsuchen können, die sie unter dem Dienst gespeichert haben. Sie können Warteschlangen zum Senden von Nachrichten an den Bildverarbeitungsdienst nutzen, um anzugeben, dass neue Bilder hochgeladen wurden und bereit für die Verarbeitung sind. Diese Art der Architektur ermöglicht es Ihnen, die einzelnen Teile des Diensts unabhängig voneinander zu entwickeln und zu aktualisieren.

## <a name="azure-storage-accounts"></a>Azure-Speicherkonten

Sie müssen ein _Speicherkonto_ erstellen, um über eine Anwendung auf diese Dienste zuzugreifen. Das Speicherkonto stellt in Azure einen eindeutigen Namespace zum Speichern Ihrer Datenobjekte sowie für den Zugriff darauf bereit. Ein Speicherkonto enthält alle Blobs, Dateien, Warteschlangen, Tabellen und VM-Datenträger, die Sie unter diesem Konto erstellen.

### <a name="creating-a-storage-account"></a>Erstellen eines Speicherkontos

Ein Azure-Speicherkonto kann über das Azure-Portal, mithilfe von Azure PowerShell oder über die Azure-Befehlszeilenschnittstelle erstellt werden. Azure Storage enthält drei verschiedene Kontooptionen, für die jeweils unterschiedliche Preise und unterstützte Features gelten.

> [!div class="mx-tableFixed"]
> | Kontotyp | Beschreibung |
> |--------------|-------------|
> | **Allgemein v2 (GPv2)** | Speicherkonten vom Typ „Allgemein v2 (GPv2)“ unterstützen alle aktuellen Features für Blobs, Dateien, Warteschlangen und Tabellen. Die Preise für GPv2-Konten wurden so ausgelegt, dass sich die niedrigsten Kosten pro Gigabyte ergeben. |
> | **Allgemein v1 (GPv1)** | Speicherkonten vom Typ „Allgemein v1 (GPv1)“ ermöglichen den Zugriff auf alle Azure Storage-Dienste, bieten aber ggf. nicht die aktuellen Features oder die niedrigsten GB-Preise. Beispielsweise werden die Speicherebenen „Cool“ und „Archiv“ in GPv1 nicht unterstützt. Die Preise für GPv1-Transaktionen sind niedriger, sodass Workloads mit hohen Datenänderungs- oder Leseraten ggf. von der Nutzung dieses Kontotyps profitieren. |
> | **Blobspeicherkonten** | Blobspeicherkonten stellen einen älteren Kontotyp dar und unterstützen alle Blockblobfeatures, die auch für GPv2 unterstützt werden, aber sie sind ausschließlich auf die Unterstützung von Block- und Anfügeblobs beschränkt. Die Preise sind weitestgehend mit den Preisen für allgemeine Konten vom Typ „Allgemein v2“ identisch. |
    
Wenn Sie daran interessiert sind, mehr über die Erstellung von Speicherkonten zu erfahren, hilft Ihnen das Modul **Erstellen eines Azure-Speicherkontos** im Lernportal weiter.