Azure Storage bietet eine REST-basierte (Representational State Transfer) Web-API für die Arbeit mit den Containern und gespeicherten Daten in den einzelnen Konten. Es stehen jeweils unabhängige APIs für die verschiedenen Datentypen zur Verfügung, mit denen Sie arbeiten können. Zur Erinnerung: Wir haben vier spezifische Datentypen:

- **Blobs** für unstrukturierte Daten (beispielsweise Binär- und Textdateien).
- **Warteschlangen** für beständiges Messaging.
- **Tabellen** für die strukturierte Speicherung von Schlüssel-Wert-Paaren.
- **Dateien** für herkömmliche SMB-Dateifreigaben.

## <a name="using-the-rest-api"></a>Verwenden der REST-API

In Diensten, die in Azure ausgeführt werden, kann auf die Storage-REST-APIs über ein virtuelles Netzwerk zugegriffen werden. In Anwendungen, die HTTP-/HTTPS-Anforderungen senden und eine HTTP-/HTTPS-Antworten empfangen kann, ist der Zugriff über das Internet möglich.

Wenn Sie also beispielsweise alle Blobs in einem Container auflisten möchten, können Sie etwa Folgendes senden:

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

Dadurch wir ein XML-Block mit kontospezifischen Daten zurückgeben:

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

Dieser Ansatz ist jedoch mit einem hohen manuellen Analyseaufwand sowie mit der Erstellung von geeigneten HTTP-Paketen für die jeweilige API verbunden. Aus diesem Grund bietet Azure vorkonfigurierte _Clientbibliotheken_, die die Arbeit mit dem Dienst für gängige Sprachen und Frameworks erleichtern.

## <a name="using-a-client-library"></a>Verwenden einer Clientbibliothek

Clientbibliotheken können Anwendungsentwicklern sehr viel Arbeit sparen, da die API getestet wird und häufig praktischere Wrapper für die Datenmodelle bereitstellt, die von der REST-API gesendet und empfangen werden.

:::row:::
    :::column:::
        Microsoft stellt Azure-Clientbibliotheken bereit, die eine Reihe von Sprachen und Frameworks unterstützen. Hierzu zählen unter anderem Folgende: - .NET - Java - Python - Node.js - Go :::column-end:::: :::column:::
        <br> ![Beispiellogos unterstützter Frameworks, die mit Azure verwendet werden können](../media/4-common-tools.png)
    :::column-end:::
:::row-end:::

Mit dem folgenden Codeausschnitt können Sie beispielsweise die gleiche Blobliste in C# abrufen:

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

JavaScript-Variante:

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
> Bei den Clientbibliotheken handelt es sich lediglich um einfache _Wrapper_ für die REST-API. Die Bibliotheken tun genau das, was Sie auch tun, wenn Sie die Webdienste direkt verwenden. Dank ihres Open-Source-Charakters sind die Bibliotheken zudem äußerst transparent. Sie finden sie auf GitHub.

Als Nächstes bereiten wir unsere Anwendung für die Unterstützung von Clientbibliotheken vor.