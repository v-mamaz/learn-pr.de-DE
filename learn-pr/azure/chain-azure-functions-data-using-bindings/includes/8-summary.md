Dieses Modul wurde alles über die Integration von Daten und Dienste in Ihre Funktionen. Wir begannen mit einen kurzen Überblick über die Bindungstypen, die angezeigt werden, wenn Sie sie an eine Funktion hinzufügen. Wir haben uns angeschaut dann Lesen von Daten aus einer Azure Cosmos DB-eingabebindung verwenden. Die Plattform übernimmt die Verwaltung von Verbindungszeichenfolgen und erläutert, wie einfach es ist zum Lesen von Daten in unserem Code unter Verwendung der Bindung. Zum Schluss konzentrierten wir uns unsere Aufmerksamkeit auf das Schreiben von Daten von verschiedenen Quellen mit Hilfe der ausgabebindungen. Dieser Weg ist in der folgenden Tabelle zusammengefasst.

[!INCLUDE [summary table](./summary-table.md)]

Sie können die Ansätze anwenden, die Sie hier gelernt haben, hinzufügen und Testen von Bindungen in Ihren Funktionen. Hier sind einige interessante Ideen aus, um weitere vertraut zu machen, mit Bindungen und erstellen auf die Sie hier gelernt haben.

* Erstellen Sie eine andere Funktion zum Lesen von BLOB-Speicher und andere eingabebindungen, die wir in diesem Modul nicht verwendet haben.

* Erstellen Sie eine andere Funktion zum Schreiben in mehrere Ziele, die mit anderen unterstützten Ausgabetypen für die Bindung an.

* In der letzten Einheit wir eingeführt, eine Warteschlange und Nachrichten an diese mit einer ausgangsbindung bereitgestellt. Als Nächstes, erwägen Sie eine andere Funktion, die die Nachrichten in der Warteschlange liest und druckt die **MELDUNGSTEXT** an die Konsole mit `Console.Log()`.

Wie wir in diesem Modul gesehen haben, bietet das Azure-Portal einfach zu bedienende Features, um Funktionen zu erstellen und das Verbinden mit Daten und andere Dienste zu starten.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="further-reading"></a>Weitere nützliche Informationen

Obwohl dies nicht die eine vollständige Liste gedacht ist, sind die folgenden einige Ressourcen, die im Zusammenhang mit den Themen in diesem Modul aus, die Sie interessant finden können.

 * [Dokumentation zu Azure Functions](https://docs.microsoft.com/azure/azure-functions/)

* [Die Herausforderung mit Azure Functions](https://aka.ms/afc)

* [Azure Serverless Computing Cookbook](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)

 * [Gewusst wie: Verwenden von Queue Storage mit Node.js](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [Einführung in Azure Cosmos DB: SQL-API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [Eine technische Übersicht über Azure Cosmos DB](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [Dokumentation für Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)
