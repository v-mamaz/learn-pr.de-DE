In diesem Modul ging es darum, Daten und Dienste in Ihre Funktionen zu integrieren. Wir haben uns zuerst einen Überblick über Bindungstypen verschafft, die Sie Ihrer Funktion hinzufügen können. Anschließend haben wir das Lesen von Daten aus einer Azure Cosmos DB-Datenbank mithilfe einer Eingabebindung untersucht. Die Plattform übernimmt die Verwaltung von Verbindungszeichenfolgen, und wir haben gesehen, wie einfach es ist, Daten in unserem Code mithilfe der Bindung zu lesen. Schließlich haben wir unsere Aufmerksamkeit auf das Schreiben von Daten in verschiedene Quellen mithilfe von Ausgabebindungen gerichtet. Diese Themenbereiche werden in der folgenden Tabelle zusammengefasst:

[!INCLUDE [summary table](./summary-table.md)]

Die hier erlernten Ansätze können Sie anwenden, um Ihren Funktionen Bindungen hinzuzufügen und diese zu testen. Im Folgenden finden Sie einige interessante Ideen, mit denen Sie den Umgang mit Bindungen üben und auf dem Gelernten aufbauen können.

* Erstellen Sie eine weitere Funktion zum Lesen von Blob Storage-Bindungen und anderen Eingabebindungen, die in diesem Modul nicht verwendet wurden.

* Erstellen Sie eine weitere Funktion, um mit anderen unterstützten Ausgabebindungstypen in weitere Ziele zu schreiben.

* In der vorherigen Einheit haben wir eine Warteschlange eingeführt und Nachrichten mit einer Ausgabebindung an diese übermittelt. Erwägen Sie als nächsten Schritt, eine weitere Funktion hinzuzufügen, die die Nachrichten in der Warteschlange liest und den **NACHRICHTENTEXT** mit `Console.Log()` auf der Konsole ausgibt.

Wie wir in diesem Modul gesehen haben, bietet das Azure-Portal einfach zu verwendende Features, um Funktionen zu erstellen und diese mit Daten und anderen Diensten zu verbinden.

Weitere Informationen zu den im Beispiel genannten serverlosen Integrationen mit visuellen Workflows und wenig oder gar keinem Code finden Sie in Azure Logic Apps.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>Weitere Ressourcen

Dies ist zwar keine vollständige Liste, aber im Folgenden finden Sie einige Ressourcen zu den in diesem Modul behandelten Themen, die für Sie interessant sein könnten.

* [Dokumentation zu Azure Functions](https://docs.microsoft.com/azure/azure-functions/)
* [Die Azure Functions-Herausforderung](https://aka.ms/afc)
* [Serverloses Computing mit Azure: Cookbook](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)
* [Gewusst wie: Verwenden von Queue Storage mit Node.js](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)
* [Einführung in Azure Cosmos DB: SQL-API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)
* [Technische Übersicht über Azure Cosmos DB](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)
* [Dokumentation für Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)
