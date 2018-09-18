Microsoft Cognitive Services ist eine umfassende Suite mit intelligenten Diensten, die wir zum Erweitern unserer Apps nutzen können. Wir haben einen kleinen Teil des Textanalyse-API-Diensts untersucht, um allgemeinere Informationen zum Text zu ermitteln. Wir haben den Dienst verwendet, um Textfeedback von Kunden auf Stimmungen zu analysieren. Wir haben eine Lösung erstellt, die in Azure Functions gehostet wird, um diese Textnachrichten zur weiteren Verarbeitung in verschiedene Buckets bzw. Warteschlangen einzusortieren.

Wenn Sie wissen, wie Sie eine REST-API aufrufen, können Sie diese intelligenten Dienste leicht in Ihre Lösungen integrieren. Hierbei wird jeweils ein ähnliches Muster eingehalten:

- Registrieren für einen Zugriffsschlüssel
- Erkunden in der API-Testkonsole
- Formulieren von Anforderungen mit dem Zugriffsschlüssel und der richtigen Region
- Senden von POST-Anforderungen aus Ihrer Lösung und Analysieren der Antworten auf Erkenntnisse

Wir haben diese „Intelligence“ der serverlosen Logik von Azure Functions hinzugefügt. Es ist für Sie einfach, diese Dienste über andere Arten von Apps aufzurufen. Es sind viele Clientbibliotheken, Tutorials und Schnellstartanleitungen vorhanden, um Ihnen den Einstieg zu erleichtern.

## <a name="suggestions-for-further-enhancement-of-our-solution"></a>Vorschläge zur weiteren Verbesserung unserer Lösung

Hier sind einige Ideen aufgeführt, die Sie als Anregungen für Schritte zur Weiterführung der vermittelten Grundlagen verwenden können. 

- Testen Sie die Lösung mit mehr Textbeispielen. Entscheiden Sie, ob die Schwellenwerte, die wir zum Kategorisieren von Stimmungspunktzahlen in „Positiv“, „Negativ“ und „Neutral“ festgelegt haben, geeignet sind. 
- Erwägen Sie das Hinzufügen einer weiteren Funktion zu Ihrer Funktions-App, mit der Nachrichten aus der Warteschlange [!INCLUDE [negative-q](./q-name-negative.md)] gelesen und die Textanalyse-API aufgerufen wird, um im Text nach Schlüsselbegriffen zu suchen.
- Unsere Eingabewarteschlange enthält unformatiertes Textfeedback. In der Praxis ordnen wir Feedback mit einer Art von Benutzer-ID zu, z.B. E-Mail-Adresse, Kontonummer usw. Erweitern Sie also die Elemente der Eingabewarteschlange, um JSON-Dokumente mit ID-Feld und Text zu erhalten. Verwenden Sie diese ID anschließend beim Verwenden der Textnachricht.
 - Derzeit ist unsere Lösung auf die Sprache Englisch „hartcodiert“. Überlegen Sie, welche Änderungen Sie vornehmen würden, um sie anzupassen oder die Verarbeitung von Text in allen Sprachen zu ermöglichen, die von der Textanalyse-API unterstützt werden.  

Nachdem Sie nun wissen, wie Sie eine dieser Cognitive Services-APIs aufrufen, können Sie sich einige andere Dienste ansehen und überlegen, wie Sie diese in Ihren Lösungen nutzen könnten. 

## <a name="further-reading"></a>Weitere nützliche Informationen

- [Übersicht über die Textanalyse](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [Ermitteln von Standpunkten mithilfe der Textanalyse](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [Dokumentation zu Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/)

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Der Begriff *Ressourcen* bezieht sich im Zusammenhang mit Azure auf Funktions-Apps, Funktionen, Speicherkonten und Ähnliches. Sie werden in *Ressourcengruppen* zusammengefasst, und sämtliche Inhalte einer Gruppe können durch das Löschen der Gruppe gelöscht werden.

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

 * [Gewusst wie: Verwenden von Queue Storage mit Node.js](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [Einführung in Azure Cosmos DB: SQL-API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [Technische Übersicht über Azure Cosmos DB](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [Dokumentation für Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)
