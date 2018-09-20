Blobs sind „Dateien für die Cloud“. Apps funktionieren mit Blobs im Wesentlichen auf die gleiche Weise, wie sie mit Dateien auf einem Datenträger funktionieren würden (Daten lesen und schreiben). Im Gegensatz zu einer lokalen Datei kann mit einer Internetverbindung von überall auf Blobs zugegriffen werden.

Azure Blob Storage ist *unstrukturiert*, d.h. es gibt für die so gespeicherten Daten keine Einschränkungen. Ein Blob enthält beispielsweise ein PDF-Dokument, ein JPG-Bild, eine JSON-Datei, Videoinhalte usw. Blobs sind nicht auf gebräuchliche Dateiformate beschränkt. Ein Blob kann mehrere Gigabyte binärer Daten von einem wissenschaftlichen Gerät, eine verschlüsselte Nachricht für eine andere Anwendung oder Daten in benutzerdefiniertem Format für eine App, die Sie entwickeln, enthalten.

Blobs sind in der Regel nicht für strukturierte Daten geeignet, die regelmäßig abgefragt werden müssen. Sie weisen eine höhere Latenz auf als Arbeitsspeicher und lokale Datenträger, und verfügen nicht über Indizierungsfunktionen, die Datenbanken effizienter beim Ausführen von Abfragen machen. Jedoch werden Blobs häufig in *Kombination* mit Datenbanken zum Speichern von nicht abfragbaren Daten verwendet. Beispielsweise könnte eine App mit einer Datenbank mit Benutzerprofilen Profilbilder in Blobs speichern. Jeder Benutzerdatensatz in der Datenbank würde den Namen oder die URL des Blobs enthalten, der das Bild des Benutzers enthält.

Bei allen Arten von Anwendungen und Architekturen werden Blobs für die Datenspeicherung verwendet:

- Apps, die große Datenmengen über ein Nachrichtensystem übermitteln müssen, das nur kleine Nachrichten unterstützt. Diese Apps können Daten in Blobs speichern und die Blob-URLs in Nachrichten senden.
- Blobspeicher können wie ein Dateisystem zum Speichern und Freigeben von Dokumenten und anderen persönlichen Daten verwendet werden.
- Statische Webressourcen wie Bilder können in Blobs gespeichert und zum öffentlichen Download verfügbar gemacht werden, als wären sie Dateien auf einem Webserver.
- Viele Azure-Komponenten verwenden Blobs im Hintergrund. Azure Cloud Shell beispielsweise speichert die Dateien und Konfiguration in Blobs, und Azure Virtual Machines verwendet Blobs zum Speichern auf der Festplatte.

Einige Apps erstellen, aktualisieren und löschen Blobs ständig als Teil ihrer Arbeit. Andere verwenden eine geringe Anzahl von Blobs und ändern diese nur selten.

## <a name="storage-accounts-containers-and-metadata"></a>Speicherkonten, Container und Metadaten

In Blob Storage befindet sich jedes Blob in einem *Blobcontainer*. Sie können eine unbegrenzte Anzahl von Blobs in einem Container und eine unbegrenzte Anzahl von Containern in einem Speicherkonto speichern. Container sind „flach“ und können nur Blobs, aber keine anderen Container speichern.

Blobs und Container unterstützen Metadaten in Form von Name/Wert-Zeichenfolgenpaaren. Ihre Apps können Metadaten für alles verwenden, was Sie möchten: eine lesbare Beschreibung der Inhalte eines Blobs, die von der Anwendung angezeigt werden, eine Zeichenfolge, die Ihre App verwendet, um festzulegen, wie die Daten des Blobs verarbeitet werden sollen usw.

> [!TIP]
> Blob Storage bietet keinen Mechanismus für die Suche oder Sortierung von Blobs nach Metadaten an. Weitere Informationen zur Verwendung von Azure Search finden Sie im Abschnitt „Weitere Informationen“ am Ende dieses Moduls.

## <a name="the-blob-storage-api-and-client-libraries"></a>Blob Storage-API und Clientbibliotheken

Die Blob Storage-API basiert auf REST und wird von Clientbibliotheken in vielen Sprachen unterstützt. Sie ermöglicht es Ihnen Apps zu schreiben, die Blobs und Container erstellen und löschen, Blobdaten hochzuladen und herunterzuladen und die Blobs in einem Container aufzulisten.
