Beim Entwerfen einer App, die Daten speichern muss, müssen Sie unbedingt überlegen, wie die App Daten in Speicherkonten, Containern und Blobs organisieren soll.

## <a name="storage-accounts"></a>Speicherkonten

Ein einzelnes Speicherkonto ist flexibel genug, um Ihre Blobs nach Ihren Wünschen zu organisieren, aber Sie sollten zusätzliche Speicherkonten nach Bedarf hinzufügen, um Kosten- und Steuerungszugriff auf Daten logisch zu trennen.

## <a name="containers-and-blobs"></a>Container und Blobs

Die Art der Anwendung und die Daten, die sie speichert, sollten Ihre Strategie für das Benennen und Organisieren von Containern und Blobs bestimmen.

Apps, die Blobs als Teil eines Speicherschemas verwenden, das eine Datenbank beinhaltet, müssen sich häufig nicht stark auf Organisation, Benennung oder Metadaten verlassen, um etwas zu ihren Daten anzuzeigen. Solche Apps verwenden im Allgemeinen Bezeichner wie z.B. GUIDs als Blobnamen und verweisen in Datenbank-Datensätzen auf diese Bezeichner. Die App verwendet die Datenbank, um zu bestimmen, wo Blobs gespeichert werden, und welche Art von Daten sie enthalten.

Andere Apps verwenden Azure Blob Storage eher wie ein persönliches Dateisystem, in dem Bedeutung und Struktur mit Container- und Blobnamen angegeben werden. Blobnamen sehen in Apps dieser Arten oft wie herkömmliche Dateinamen aus und enthalten Dateinamenerweiterungen wie `.jpg`, um anzugeben, welche Art von Daten sie enthalten. Sie verwenden virtuelle Verzeichnisse (siehe unten), um Blobs zu organisieren, und häufig Metadatentags zum Speichern von Informationen zu Blobs und Containern.

Bei der Entscheidung, wie Blobs und Container organisiert und gespeichert werden sollen, sind ein paar wichtige Punkte zu berücksichtigen.

### <a name="naming-limitations"></a>Einschränkungen bei der Benennung

Für Container -und Blobnamen müssen bestimmten Regeln eingehalten werden, die beispielsweise Längen- und Zeichenbeschränkungen umfassen. Spezifischere Informationen zu Benennungsregeln finden Sie im Abschnitt „Weitere Informationen“ am Ende dieses Moduls.

### <a name="public-access-and-containers-as-security-boundaries"></a>Öffentlicher Zugriff und Container als Sicherheitsgrenzen

Standardmäßig setzen alle Blobs Authentifizierung für den Zugriff voraus. Allerdings können einzelne Container so konfiguriert werden, dass sie das öffentliche Herunterladen ihrer Blobs ohne Authentifizierung ermöglichen. Dieses Feature unterstützt viele Anwendungsfälle, wie z.B. das Hosten statischer Websiteressourcen und das Freigeben von Dateien. Der Grund hierfür ist, dass das Herunterladen von Blobinhalten in gleicher Weise funktioniert wie das Lesen von Daten jeder anderen Art über das Internet: Sie rufen in einem Browser oder einem anderen Programm, das eine GET-Anforderung stellen kann, die Blob-URL auf.

Das Aktivieren des öffentlichen Zugriffs ist wichtig für die Skalierbarkeit, da direkt aus Blob Storage heruntergeladene Daten keinen Datenverkehr in Ihrer serverseitigen App generieren. Auch wenn Sie nicht sofort den öffentlichen Zugriff nutzen, oder wenn Sie eine Datenbank zur Steuerung des Datenzugriffs über Ihre Anwendung verwenden werden, planen Sie die Verwendung von separaten Containern für Daten, die Sie öffentlich verfügbar machen möchten.

> [!CAUTION]
> Blobs in einem für öffentlichen Zugriff konfigurierten Container können ohne jegliche Authentifizierung oder Überwachung von jedem Benutzer heruntergeladen werden, der ihre Speicher-URLs kennt. Legen Sie Blobdaten niemals in einem öffentlichen Container ab, den Sie nicht öffentlich freigeben möchten.

Zusätzlich zum öffentlichen Zugriff bietet Azure ein Signaturfeature für freigegebenen Zugriff, das eine differenzierte Berechtigungensteuerung im Container ermöglicht. Eine präzise Zugriffssteuerung ermöglicht Szenarien, die die Skalierbarkeit weiter verbessern – die Berücksichtigung von Containern als Sicherheitsgrenzen ist also im Allgemeinen eine hilfreiche Richtlinie.

### <a name="blob-name-prefixes-virtual-directories"></a>Präfixe von Blobnamen (virtuelle Verzeichnisse)

Technisch gesehen sind Container „flach“ und unterstützen Schachtelung oder Hierarchie in keiner Weise. Aber wenn Sie Ihren Blobs hierarchische Namen geben, die wie Dateipfade aussehen (z.B. `finance/budgets/2017/q1.xls`), kann der Auflistungsvorgang der API Ergebnisse für bestimmte Präfixe filtern. So können Sie in der Liste navigieren, als wäre sie ein hierarchisches System von Dateien und Ordnern.

Dieses Feature wird häufig als *virtuelle Verzeichnisse* bezeichnet, da einige Tools und Clientbibliotheken es zum Visualisieren von Blobspeicher und zum Navigieren darin verwenden, als wäre es ein Dateisystem. Jede Ordnernavigation löst einen separaten Aufruf zum Auflisten von Blobs in diesem Ordner aus.

Die Verwendung von Blobnamen, die Dateinamen ähneln, ist eine gängige Methode, um komplexe Blobdaten zu organisieren und diese zu durchsuchen.

### <a name="blob-types"></a>Blobtypen

Es gibt drei verschiedene Arten von Blobs, in denen Sie Daten speichern können:

- **Blockblobs** bestehen aus Blöcken verschiedener Größen, die gleichzeitig und unabhängig voneinander hochgeladen werden können. Wenn Sie für einen Blockblob einen Schreibvorgang ausführen, werden Daten in Blöcke hochgeladen. Anschließend wird ein Commit ausgeführt, um die Blöcke in den Blob zu übertragen.
- **Anfügeblobs** sind spezielle Blockblobs, die zwar nur das Anfügen neuer Daten unterstützen (nicht Aktualisieren oder Löschen vorhandener Daten), diesen Vorgang jedoch sehr effizient ausführen. Anfügeblobs eignen sich hervorragend für Szenarios wie das Speichern von Protokollen oder Schreiben von Streamingdaten.
- **Seitenblobs** sind für Szenarios mit Lese- und Schreibvorgängen mit wahlfreiem Zugriff vorgesehen. Seitenblobs dienen zum Speichern der Dateien der virtuellen Festplatte (Virtual Hard Disk, VHD), die von Azure Virtual Machines verwendet werden, aber sie eignen sich hervorragend für jedes Szenario, das wahlfreien Zugriff umfasst.

Blockblobs sind die beste Wahl für die meisten Szenarios, die nicht speziell Anfüge- oder Seitenblobs erfordern. Die blockbasierte Struktur unterstützt schnelle Uploads und Downloads sowie den effizienten Zugriff auf individuelle Blobkomponenten. Der Verwaltungs- und Commitprozess für Blöcke wird von den meisten Clientbibliotheken automatisch gesteuert. Einige Bibliotheken verarbeiten zusätzlich gleichzeitige Uploads und Downloads zur Leistungsoptimierung.