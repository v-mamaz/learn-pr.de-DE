Microsoft Cognitive Services handelt es sich um eine umfassende Suite von intelligente Dienste, mit denen wir unsere apps erweitern. Die Textanalyse-API verfügt über mehrere Vorgänge, um Text in wertvolle Einblicke zu aktivieren. Den Dienst verwendet zum Ermitteln der Stimmung im Text-Feedback von Kunden. Wir haben eine Lösung, die in Azure Functions zum Sortieren dieser SMS-Nachrichten in verschiedenen Buckets oder Warteschlangen, zur weiteren Verarbeitung gehostet erstellt.

Nachdem Sie eine REST-API aufrufen können, können Sie diese intelligente Dienste problemlos in Ihre Lösungen integrieren. Alle folgen einem ähnlichen Muster:

- Melden Sie sich für einen Zugriffsschlüssel
- Entdecken Sie in der API-testkonsole
- Formulieren Sie Anforderungen mit dem Zugriffsschlüssel und die richtige Region ein.
- Senden Sie Anforderungen aus der Projektmappe, und Analysieren von Antworten für Einblicke.

Wir haben serverlose Logik, die in Azure Functions erstellt diesen Daten hinzugefügt. Sie können diese Dienste einfach aus anderen Typen von apps aufrufen. Es gibt viele Clientbibliotheken, Lernprogramme und Schnellstarts erleichtern Ihnen den Einstieg erleichtern.

## <a name="suggestions-for-further-enhancement-of-our-solution"></a>Vorschläge zur weiteren Verbesserung unserer Lösung

Hier sind einige Ideen für die Sie berücksichtigen, wenn Sie nutzen, was wir darüber möchten.

- Testen der Lösung Weitere Beispiele für Text. Entscheiden Sie, ob die Schwellenwerte, was wir stimmungswerte in Positive und negative und neutrale kategorisieren geeignet sind.
- Erwägen Sie eine andere Funktion in Ihrer Funktions-app, die Nachrichten von liest die [!INCLUDE [negative-q](./q-name-negative.md)] Warteschlange und die Textanalyse-API-Aufrufe zum Suchen der Schlüsselausdrücke im Text.
- Unsere Eingabewarteschlange enthält die unformatierten Text-Feedback. In der Praxis würden wir Feedback über eine Benutzer-ID, z. B. e-Mail-Adresse, Kontonummer, zuordnen und so weiter. Verbessern Sie die Elemente der Eingabewarteschlange zu JSON-Dokumente, und ID-Feld und den Text an. Klicken Sie dann verwenden Sie diese ID bei der Arbeit mit SMS.
- Derzeit unsere Lösung ist "hartcodiert" auf Englisch. Denken Sie die Änderungen, dass Sie implementieren würde, um Text in allen Sprachen, die von der Textanalyse-API unterstützt verarbeiten kann zu erleichtern.
- Wenn Sie mit Logik-Apps vertraut sind, rufen Sie den Link, um den integrierten Connector für Textanalysen im Abschnitt Weitere nützliche Informationen.

Nun Sie wissen wie eine der folgenden Cognitive Services-APIs aufrufen, lernen Sie einige der anderen Dienste und überlegen Sie, wie Sie diese in Ihren Lösungen verwenden können.

## <a name="further-reading"></a>Weitere nützliche Informationen

- [Übersicht über die Textanalyse](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [Beim Erkennen der Stimmung im Text Analytics](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [Dokumentation zu cognitive Services](https://docs.microsoft.com/azure/cognitive-services/)

- [Text Analytics Logic Apps-Connector](https://docs.microsoft.com/connectors/cognitiveservicestextanalytics/)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
