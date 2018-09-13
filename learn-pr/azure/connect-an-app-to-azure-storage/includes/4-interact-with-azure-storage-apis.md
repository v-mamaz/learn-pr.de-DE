Als Softwareentwickler möchten Sie so wenig Zeit wie möglich mit dem Schreiben von Code verbringen. Zum Interagieren mit Azure Storage können Sie den REST-Endpunkt verwenden. Allerdings erfordert dies sehr viel Arbeit. Daher wurden Bibliotheken entwickelt, um die Verbindungsherstellung und die Verwendung von Azure Storage zu beschleunigen. Diese Bibliotheken werden als *Clientbibliotheken* verwendet und stellen in der Regel die einfachste Möglichkeit zur Interaktion mit Azure Storage dar. 

Nachfolgend erfahren Sie, wie Sie eine Clientbibliothek als Verweis zu Ihrer .NET-Anwendung hinzufügen können.

## <a name="application-programming-interface-api"></a>Anwendungsprogrammierschnittstelle

Azure Storage stellt mithilfe verschiedener Anwendungsprogrammierschnittstellen (APIs) und REST-Protokollen (Representational State Transfer) im Internet Dienste zur Verfügung. Diese APIs werden ausführlich in der [REST-API-Referenz für Azure Storage-Dienste](https://docs.microsoft.com/rest/api/storageservices/) dokumentiert. Sie können zwar direkt mit diesen APIs interagieren, aber der Zugriff auf Azure Storage verläuft in der Regel über eine Clientbibliothek. Mithilfe von Clientbibliotheken haben Anwendungsentwickler viel weniger Arbeit, da die API ausführlich getestet wird.

## <a name="language-support"></a>Sprachunterstützung

Es gibt einige Clientbibliotheken, über die Sie auf Azure Storage zugreifen können und die mehrere Sprachen unterstützen. Diese [Dokumentationsseite zu SDK Tools](https://docs.microsoft.com/azure/#pivot=sdkstools) enthält Links zu den Clientbibliotheken oder SDKs für sämtliche derzeit unterstützte Sprachen. Z.B.: .NET, Java, Python, Node.js und Go.

## <a name="summary"></a>Zusammenfassung

Azure Storage stellt einen REST-Endpunkt zur Verfügung, um mit allen zugehörigen Diensten zu interagieren. Sie können zwar auf diese Endpunkte zurückgreifen, aber in der Regel werden Clientbibliotheken verwendet. Azure Storage unterstützt eine Reihe von Sprachen, u.a. .NET, Java, Python und Node.js.
