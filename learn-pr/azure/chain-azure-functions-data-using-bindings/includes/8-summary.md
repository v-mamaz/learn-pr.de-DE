In diesem Modul ging es darum, Daten und Dienste in Ihre Funktionen zu integrieren. Wir begannen mit einer kurzen Tour durch die Bindungstypen, die auftreten, wenn Sie sie einer Funktion hinzufügen. Wir haben dann das Lesen von Daten aus einer Azure Cosmos DB mithilfe einer Eingabebindung untersucht. Die Plattform übernimmt die Verwaltung von Verbindungszeichenfolgen, und wir haben gesehen, wie einfach es ist, Daten in unserem Code mithilfe der Bindung zu lesen. Schließlich haben wir unsere Aufmerksamkeit auf das Schreiben von Daten in verschiedene Quellen mithilfe von Ausgabebindungen gerichtet. Diese Themenbereiche werden in der folgenden Tabelle zusammengefasst.

[!INCLUDE [summary table](./summary-table.md)]

Die hier erlernten Ansätze können Sie anwenden, um Ihren Funktionen Bindungen hinzuzufügen und diese zu testen. Hier sind ein paar interessante Ideen, um mehr Übung mit Bindungen zu bekommen und auf dem aufzubauen, was Sie hier gelernt haben.

* Erstellen Sie eine weitere Funktion zum Lesen von Blob Storage- und anderen Eingabebindungen, die wir in diesem Modul nicht verwendet haben.

* Erstellen Sie eine weitere Funktion, um mit anderen unterstützten Ausgabebindungstypen in weitere Ziele zu schreiben.

* In der letzten Einheit haben wir eine Warteschlange eingeführt und Nachrichten mit einer Ausgabebindung in ihr gespeichert. Erwägen Sie als nächsten Schritt, eine weitere Funktion hinzuzufügen, die die Nachrichten in der Warteschlange liest und den **NACHRICHTENTEXT** in der Konsole mit `Console.Log()` ausgibt.

Wie wir in diesem Modul gesehen haben, bietet das Azure-Portal einfach zu verwendende Features, um Funktionen zu erstellen und diese mit Daten und anderen Diensten zu verbinden.

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

*Ressourcen* bezieht sich im Zusammenhang mit Azure auf Funktions-Apps, Funktionen, Speicherkonten usw. Sie werden in *Ressourcengruppen* zusammengefasst, und sämtliche Inhalte einer Gruppe können durch Löschen der Gruppe gelöscht werden.

Sie haben Ressourcen erstellt, um dieses Modul abzuschließen. Für diese Ressourcen fallen je nach [Kontostatus](https://azure.microsoft.com/account/) und [Dienstpreisen](https://azure.microsoft.com/pricing/) unter Umständen Kosten an. Nicht mehr benötigte Ressourcen können wie folgt gelöscht werden:

1. Navigieren Sie im Azure-Portal zur Seite **Ressourcengruppe**.

   Von der Seite „Funktions-App“ aus gelangen Sie zu dieser Seite, indem Sie auf die Registerkarte **Übersicht** und anschließend unter **Ressourcengruppe** auf den Link klicken.

   Vom Dashboard aus gelangen Sie zu dieser Seite, indem Sie auf **Ressourcengruppen** klicken und anschließend die Ressourcengruppe auswählen, die Sie für dieses Modul verwendet haben. 

> [!NOTE]
> Der Standardname der Ressourcengruppe, den wir für dieses Modul vorgeschlagen haben, war [!INCLUDE [resource-group-name](./rg-name.md)], aber es ist möglich, dass Sie einen anderen Namen verwendet haben.

2. Prüfen Sie auf der Seite **Ressourcengruppe** die Liste mit den enthaltenen Ressourcen, und vergewissern Sie sich, dass es sich dabei um die Ressourcen handelt, die Sie löschen möchten.

3. Klicken Sie auf **Ressourcengruppe löschen**, und folgen Sie den Anweisungen.

   Der Löschvorgang kann einige Minuten dauern. Nach Abschluss des Vorgangs wird kurz eine Benachrichtigung angezeigt. Sie können auch am oberen Seitenrand auf das Glockensymbol klicken, um die Benachrichtigung anzuzeigen.

## <a name="further-reading"></a>Weitere nützliche Informationen

Dies ist zwar nicht als vollständige Liste gedacht, aber im Folgenden finden Sie einige Ressourcen zu den in diesem Modul behandelten Themen, die für Sie interessant sein könnten.

 * [Dokumentation zu Azure Functions](https://docs.microsoft.com/azure/azure-functions/)

* [Die Azure Functions-Herausforderung](https://aka.ms/afc)

* [Serverloses Computing mit Azure: Cookbook](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)

 * [Verwenden von Queue Storage aus Node.js](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [Einführung in Azure Cosmos DB: SQL-API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [Technische Übersicht über Azure Cosmos DB](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [Dokumentation für Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)
