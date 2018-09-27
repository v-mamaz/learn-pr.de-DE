Azure Cognitive Services ist eine umfassende Suite mit intelligenten Diensten, die Sie zum Erweitern Ihrer Apps nutzen können. Die Textanalyse-API verfügt über mehrere Vorgänge, um Text in wertvolle Erkenntnisse umzuwandeln. Wir haben den Dienst verwendet, um die Stimmung im Textfeedback von Kunden zu ermitteln. Wir haben eine Lösung erstellt, die in Azure Functions gehostet wird, um diese Textnachrichten zur weiteren Verarbeitung in verschiedene Buckets bzw. Warteschlangen einzusortieren.

Wenn Sie wissen, wie Sie eine REST-API aufrufen, können Sie diese intelligenten Dienste leicht in Ihre Lösungen integrieren. Hierbei wird jeweils ein ähnliches Muster eingehalten:

- Registrieren für einen Zugriffsschlüssel
- Untersuchen in der API-Testkonsole
- Formulieren von Anforderungen mit dem Zugriffsschlüssel und der richtigen Region
- Senden von POST-Anforderungen aus Ihrer Lösung und Analysieren der Antworten auf Erkenntnisse

Wir haben diese „Intelligenz“ der serverlosen Logik von Azure Functions hinzugefügt. Es ist für Sie einfach, diese Dienste über andere Arten von Apps aufzurufen. Es sind viele Clientbibliotheken, Tutorials und Schnellstartanleitungen vorhanden, um Ihnen den Einstieg zu erleichtern.

## <a name="suggestions-for-further-enhancement-of-our-solution"></a>Vorschläge zur weiteren Verbesserung unserer Lösung

Hier sind einige Ideen aufgeführt, die Sie als Anregungen für Schritte zur Weiterführung der vermittelten Grundlagen verwenden können.

- Testen Sie die Lösung mit weiteren Textbeispielen. Entscheiden Sie, ob die Schwellenwerte, die wir zum Kategorisieren von Stimmungspunktzahlen in „Positiv“, „Negativ“ und „Neutral“ festgelegt haben, geeignet sind.
- Erwägen Sie das Hinzufügen einer weiteren Funktion zu Ihrer Funktions-App, mit der Nachrichten aus der Warteschlange [!INCLUDE [negative-q](./q-name-negative.md)] gelesen und die Textanalyse-API aufgerufen wird, um im Text nach Schlüsselbegriffen zu suchen.
- Unsere Eingabewarteschlange enthält unformatiertes Textfeedback. In der Praxis ordnen wir Feedback mit einer Art von Benutzer-ID zu, z.B. E-Mail-Adresse, Kontonummer usw. Erweitern Sie die Elemente der Eingabewarteschlange, um JSON-Dokumente mit ID-Feld und Text zu erhalten. Verwenden Sie diese ID anschließend beim Verwenden der Textnachricht.
- Derzeit ist unsere Lösung auf die Sprache Englisch „hartcodiert“. Überlegen Sie, welche Änderungen Sie implementieren würden, um die Verarbeitung von Text in allen Sprachen zu ermöglichen, die von der Textanalyse-API unterstützt werden.
- Wenn Sie mit Logic Apps vertraut sind, können Sie den Link zum integrierten Connector für Textanalysen im Abschnitt „Weitere nützliche Informationen“ nutzen.

Nachdem Sie nun wissen, wie Sie eine dieser Cognitive Services-APIs aufrufen, können Sie einige andere Dienste ausprobieren und überlegen, wie Sie diese in Ihren Lösungen nutzen könnten.

## <a name="further-reading"></a>Weitere nützliche Informationen

- [Übersicht über die Textanalyse](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [Textanalysedemo](https://azure.microsoft.com/services/cognitive-services/text-analytics/)
- [Ermitteln von Stimmungen mithilfe der Textanalyse](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [Dokumentation zu Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/)

- [Textanalyse-Logic Apps-Connector](https://docs.microsoft.com/connectors/cognitiveservicestextanalytics/)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
