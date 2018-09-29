<span data-ttu-id="ea35a-101">Azure Storage bietet eine REST-API für die Arbeit mit den Containern und Daten, die in den einzelnen Konten gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="ea35a-101">Azure Storage provides a REST API to work with the containers and data stored in each account.</span></span> <span data-ttu-id="ea35a-102">Es stehen jeweils unabhängige APIs zur Verfügung, um mit den verschiedenen Typen von Daten, die Sie speichern können, zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="ea35a-102">There are independent APIs available to work with each type of data you can store.</span></span> <span data-ttu-id="ea35a-103">Zur Erinnerung: Wir haben vier spezifische Datentypen:</span><span class="sxs-lookup"><span data-stu-id="ea35a-103">Recall that we have four specific data types:</span></span>

- <span data-ttu-id="ea35a-104">**Blobs** für unstrukturierte Daten (beispielsweise Binär- und Textdateien).</span><span class="sxs-lookup"><span data-stu-id="ea35a-104">**Blobs** for unstructured data such as binary and text files.</span></span>
- <span data-ttu-id="ea35a-105">**Warteschlangen** für beständiges Messaging.</span><span class="sxs-lookup"><span data-stu-id="ea35a-105">**Queues** for persistent messaging.</span></span>
- <span data-ttu-id="ea35a-106">**Tabellen** für die strukturierte Speicherung von Schlüssel-Wert-Paaren.</span><span class="sxs-lookup"><span data-stu-id="ea35a-106">**Tables** for structured storage of key/values.</span></span>
- <span data-ttu-id="ea35a-107">**Dateien** für herkömmliche SMB-Dateifreigaben.</span><span class="sxs-lookup"><span data-stu-id="ea35a-107">**Files** for traditional SMB file shares.</span></span>

## <a name="using-the-rest-api"></a><span data-ttu-id="ea35a-108">Verwenden der REST-API</span><span class="sxs-lookup"><span data-stu-id="ea35a-108">Using the REST API</span></span>

<span data-ttu-id="ea35a-109">Anwendungen, die HTTP-/HTTPS-Anforderungen senden und HTTP-/HTTPS-Antworten empfangen können, ist der Zugriff auf die Storage-REST-APIs ist über das Internet möglich.</span><span class="sxs-lookup"><span data-stu-id="ea35a-109">The Storage REST APIs are accessible from anywhere on the Internet, by any application that can send an HTTP/HTTPS request and receive an HTTP/HTTPS response.</span></span>

<span data-ttu-id="ea35a-110">Wenn Sie also beispielsweise alle Blobs in einem Container auflisten möchten, können Sie etwa Folgendes senden:</span><span class="sxs-lookup"><span data-stu-id="ea35a-110">For example, if you wanted to list all the blobs in a container, you would send something like:</span></span>

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

<span data-ttu-id="ea35a-111">Dadurch wir ein XML-Block mit kontospezifischen Daten zurückgeben:</span><span class="sxs-lookup"><span data-stu-id="ea35a-111">This would return an XML block with data specific to the account:</span></span>

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

<span data-ttu-id="ea35a-112">Dieser Ansatz ist jedoch mit einem hohen manuellen Analyseaufwand sowie mit der Erstellung von HTTP-Paketen für die jeweilige API verbunden.</span><span class="sxs-lookup"><span data-stu-id="ea35a-112">However, this approach requires a lot of manual parsing and the creation of HTTP packets to work with each API.</span></span> <span data-ttu-id="ea35a-113">Aus diesem Grund bietet Azure vorkonfigurierte _Clientbibliotheken_, die die Arbeit mit dem Dienst für gängige Sprachen und Frameworks erleichtern.</span><span class="sxs-lookup"><span data-stu-id="ea35a-113">For this reason, Azure provides pre-built _client libraries_ that make working with the service easier for common languages and frameworks.</span></span>

## <a name="using-a-client-library"></a><span data-ttu-id="ea35a-114">Verwenden einer Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="ea35a-114">Using a client library</span></span>

<span data-ttu-id="ea35a-115">Clientbibliotheken können Anwendungsentwicklern sehr viel Arbeit sparen, da die API getestet wird und häufig praktischere Wrapper für die Datenmodelle bereitstellt, die von der REST-API gesendet und empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="ea35a-115">Client libraries can save a significant amount of work for application developers because the API is tested and it often provides nicer wrappers around the data models sent and received by the REST API.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="ea35a-116">Microsoft stellt Azure-Clientbibliotheken bereit, die eine Reihe von Sprachen und Frameworks unterstützen. Hierzu zählen unter anderem Folgende: - .NET - Java - Python - Node.js - Go :::column-end::::</span><span class="sxs-lookup"><span data-stu-id="ea35a-116">Microsoft has Azure client libraries that support a number of languages and frameworks including: - .NET - Java - Python - Node.js - Go :::column-end::::</span></span> :::column:::
        <br> <span data-ttu-id="ea35a-117">![Beispiellogos unterstützter Frameworks, die mit Azure verwendet werden können](../media/4-common-tools.png)</span><span class="sxs-lookup"><span data-stu-id="ea35a-117">![Sample logos of supported frameworks you can use with Azure](../media/4-common-tools.png)</span></span> 
    :::column-end:::
:::row-end:::

<span data-ttu-id="ea35a-118">Mit dem folgenden Codeausschnitt können Sie beispielsweise die gleiche Blobliste in C# abrufen:</span><span class="sxs-lookup"><span data-stu-id="ea35a-118">For example, to retrieve the same list of blobs in C#, we could use the following code snippet:</span></span>

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

<span data-ttu-id="ea35a-119">JavaScript-Variante:</span><span class="sxs-lookup"><span data-stu-id="ea35a-119">Or in JavaScript:</span></span>

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
> <span data-ttu-id="ea35a-120">Bei den Clientbibliotheken handelt es sich lediglich um einfache _Wrapper_ für die REST-API.</span><span class="sxs-lookup"><span data-stu-id="ea35a-120">The client libraries are just thin _wrappers_ over the REST API.</span></span> <span data-ttu-id="ea35a-121">Die Bibliotheken tun genau das, was Sie auch tun, wenn Sie die Webdienste direkt verwenden.</span><span class="sxs-lookup"><span data-stu-id="ea35a-121">They are doing exactly what you would do if you used the web services directly.</span></span> <span data-ttu-id="ea35a-122">Dank ihres Open-Source-Charakters sind die Bibliotheken zudem äußerst transparent.</span><span class="sxs-lookup"><span data-stu-id="ea35a-122">These libraries are also open source, making them very transparent.</span></span> <span data-ttu-id="ea35a-123">Sie finden sie auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="ea35a-123">Look for them on GitHub.</span></span>

<span data-ttu-id="ea35a-124">Als Nächstes bereiten wir unsere Anwendung für die Unterstützung von Clientbibliotheken vor.</span><span class="sxs-lookup"><span data-stu-id="ea35a-124">Let's add client library support to our application.</span></span>