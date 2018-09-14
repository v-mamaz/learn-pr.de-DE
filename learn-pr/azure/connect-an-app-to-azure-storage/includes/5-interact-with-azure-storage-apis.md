Azure Storage bietet eine Representational State Transfer-basierte (REST)-Web-API zum Arbeiten mit dem Container und in jedem Konto gespeicherten Daten. Es gibt unabhängig APIs zur Verfügung, mit jeder Art von Daten zu arbeiten, die Sie speichern können. Denken Sie daran, dass wir vier spezifischen Datentypen:

- **BLOBs** für unstrukturierte Daten wie z. B. Binär- und Textmodus-Dateien.
- **Warteschlangen** für dauerhaftem messaging.
- **Tabellen** für strukturierte Speicherung von Schlüssel-Wert.
- **Dateien** für herkömmliche SMB-Dateifreigaben.

## <a name="using-the-rest-api"></a>Verwenden der REST-API

Die Speicher-REST-APIs werden von zugegriffen Dienste zur Ausführung in Azure über ein virtuelles Netzwerk und über das Internet von jeder Anwendung, die eine HTTP-/HTTPS-Anforderung senden und eine HTTP/HTTPS-Antwort empfangen können.

Z. B. Wenn Sie alle Blobs in einem Container auflisten möchten, würden Sie etwa senden:

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

Dies würde einen XML-Block mit Daten für das Konto bestimmten zurückgeben:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults AccountName="https://[url-for-service-account]/">  
  <Containers>  
    <Container>  
      <Name>container1</Name>  
      <Url>https://[url-for-service-account]/container1</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 18:09:03 GMT</Last-Modified>  
        <Etag>0x8CAE7D0C4AF4487</Etag>  
      </Properties>  
      <Metadata>  
        <Color>orange</Color>  
        <ContainerNumber>01</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container2</Name>  
      <Url>https://[url-for-service-account]/container2</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8C24928</Etag>  
      </Properties>  
      <Metadata>  
        <Color>pink</Color>  
        <ContainerNumber>02</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container3</Name>  
      <Url>https://[url-for-service-account]/container3</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8EAC0BB</Etag>  
      </Properties>  
      <Metadata>  
        <Color>brown</Color>  
        <ContainerNumber>03</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
  </Containers>  
  <NextMarker>container4</NextMarker>  
</EnumerationResults>  
```

Dieser Ansatz erfordert jedoch einen Großteil der manuellen Analyse und die Erstellung von HTTP-Pakete mit jeder API arbeiten. Aus diesem Grund Azure bietet vorkonfigurierte _Clientbibliotheken_ , erleichtern die Arbeit mit dem Dienst für gängige Sprachen und Frameworks.

## <a name="using-a-client-library"></a>Mithilfe einer Clientbibliothek

-Clientbibliotheken können sehr viel Arbeit für Anwendungsentwickler speichern, da die API getestet wird, und es stellt oft nützlicher Wrapper um die Datenmodelle, die von der REST-API gesendet und empfangen.

:::row:::
    :::column:::
        Microsoft verfügt über die Azure-Clientbibliotheken, die eine Reihe von Sprachen und Frameworks wie unterstützen: – .NET - Java - Python - Node.js - Go :::column-end:::: :::column:::
        <br> ![Beispiel-Logos unterstützten Frameworks, mit denen Sie mit Azure](../media/4-common-tools.png)
    :::column-end:::
:::row-end:::

Um die gleiche Liste von Blobs im C# -Code abzurufen, können wir z. B. den folgende Codeausschnitt verwenden:

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

Oder in JavaScript:

```javascript
const containerName = "...";
const blobService = storage.createBlobService();

blobService.listBlobsSegmented(containerName, null, function (error, results) {
    if (results) {
        for (var i = 0, blob; blob = results.entries[i]; i++) {
            // Work with blob item .. could be page blob, block blob, etc.
        }
    }
});
```

> [!NOTE]
> Die Client-Bibliotheken sind einfach schlanke _Wrapper_ über die REST-API. Machen sie, ob Sie genau gehen Sie wie wenn Sie die Webdienste direkt verwendet. Diese Bibliotheken sind auch open-Source-somit sehr transparent. Sehen Sie auf GitHub an.

Fügen Sie Unterstützung von Clientbibliotheken, um die Anwendung.