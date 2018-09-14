Um die Textanalyse-API in Aktion sehen zu können, lassen Sie uns einige Aufrufe, die mithilfe der integrierten API-Konsole Testtool befindet sich in der onlinereferenzdokumentation. Bevor wir dies tun, benötigen wir einen Zugriffsschlüssel für diese Aufrufe.

## <a name="create-an-access-key"></a>Erstellen eines Zugriffsschlüssels

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Jeder Aufruf Textanalyse-API ist einen Abonnementschlüssel erforderlich. Häufig als Zugriffstaste bezeichnet, es dient zum Überprüfen, dass Sie Zugriff auf den Aufruf. Wir verwenden das Azure-Portal einen Schlüssel abrufen. 

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

1. Klicken Sie auf **erstellen Sie eine Ressource**

1. Wählen Sie unter Azure Marketplace **KI und Machine Learning** um eine Liste der verfügbaren APIs anzuzeigen. Klicken Sie auf **alle** oben rechts auf der Seite auf die gesamte Liste der Cognitive Services-APIs finden Sie unter.

1. Suchen **Textanalyse** in der Liste der Cognitive Services und wählen Sie ihn.
    ![Bildschirmabbildung von AI und Machine Learning-Bereich, in der Liste ausgewählt werden mit der Textanalyse-API.](../media/select-text-analytics.PNG)

1. Geben Sie in der Seite "erstellen", das geöffnet wird die folgenden Werte in den einzelnen Feldern ein.

|Eigenschaft  | Wert  | Beschreibung  |
|---------|---------|---------|
|Name     |    MyTextAnalyticsAPIAccount     |  Der Name des Cognitive Services-Kontos. Es wird empfohlen, einen aussagekräftigen Namen. Gültige Zeichen sind `a-z`, `0-9` und `-`.    |
|Abonnement     |  Ihr Abonnement       |   Das Abonnement, unter denen diese neue Cognitive Services-API-Konto mit **Textanalyse-API** erstellt wird.      |
|Standort     |  USA (Westen)       |  Wählen Sie eine [Region](https://azure.microsoft.com/regions/) in Ihrer Nähe.       |
|Tarif     | **Kostenlose F0**     |   Die Kosten für Ihr Cognitive Services-Konto, hängt von der tatsächlichen Nutzung und der gewählten Optionen ab. Es wird empfohlen, den freien-Tarif für unsere Zwecke hier auswählen.      |
|Ressourcengruppe     |  Wählen Sie **vorhandene** , und wählen Sie <rgn>[Sandkasten Resource Group-Name]</rgn>       |  Der Name für die neue Ressourcengruppe, in dem Ihr Cognitive Services-Textanalyse-API-Konto zu erstellen.       |

Dies ist ein Screenshot, was die **erstellen** sieht, dass die Seite "Wenn Sie ihn abgeschlossen haben.

![Screenshot der Benutzeroberfläche zum Erstellen eines Text Analytics-Kontos mit allen Feldern mit Werten, die in der obigen Tabelle vorgeschlagenen ausgefüllt.](../media/create-text-analytics-account.PNG)

1. Wählen Sie **erstellen** am unteren Rand der Seite der kontoerstellung gestartet.  Sehen Sie sich für eine Benachrichtigung, die die Bereitstellung ausgeführt wird. Sie erhalten dann eine Benachrichtigung, dass das Konto für die Ressourcengruppe erfolgreich bereitgestellt wurde.

![Benachrichtigung über eine ressourcenschaltfläche Gehe zu und eine Pin auf die Schaltfläche "Dashboard" für die Bereitstellung war erfolgreich.](../media/deploy-resource-group-success.PNG)

Nun, da wir unsere Cognitive Services-Konto haben, finden Sie den Zugriffsschlüssel lassen Sie uns, damit wir anfangen können, die API aufrufen.

1. Klicken Sie auf die **zu Ressource wechseln** Schaltfläche der *Bereitstellung erfolgreich* Benachrichtigung. Diese Aktion öffnet das Schnellstart-Konto.

1. Wählen Sie die **Schlüssel** Menüelement im Menü auf der linken Seite oder in der *nehmen Sie Ihre Schlüssel* Abschnitt des Schnellstarts.  Diese Aktion öffnet den **Verwalten von Schlüsseln** Seite.

1. Kopieren Sie einen der Schlüssel mithilfe der Schaltfläche "Kopieren".

![Verwalten Sie Schlüssel-Benutzeroberfläche, die mit dem Namen des Cognitive Services-Konto und die Schlüssel 1 und 2 mit Schlüssel-Einträge.](../media/manage-keys.PNG)

> [!IMPORTANT]
> Immer Ihre Zugriffsschlüssel schützen, und sie nicht freigeben.

1. Store dieser Schlüssel für den Rest dieses Moduls. Wir verwenden diese in Kürze, um API-Aufrufe in der testkonsole und im weiteren Verlauf od des Moduls.

Nun, da wir unseren Schlüssel verfügen, können wir navigieren Sie zu der testkonsole und nutzen die API für ein Drehfeld.

## <a name="call-the-api-from-the-testing-console"></a>Aufrufen der API aus der testkonsole

1. Navigieren Sie zu der [Textanalyse-API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7?azure-portal=true) Referenzdokumentation in Ihrem bevorzugten Browser.

    Die Landing Page zeigt ein Menü auf der linken und der Inhalt auf der rechten Seite. Klicken Sie im Menü aufgeführt, die POST-Methoden, die für die Textanalyse-API aufgerufen werden können. Diese Endpunkte werden **Sprache erkennen**, **Entitäten**, **Schlüsselausdrücken**, und **Stimmung**.  Um einen dieser Vorgänge aufzurufen, müssen wir einige Dinge tun.

    - Wählen Sie die Methode, die wir aufrufen möchten.
    - Wählen Sie einen Test-Konsole, die mit der Region übereinstimmt oder Speicherort, den wir zuvor in dieser Lektion ausgewählt.
    - Fügen Sie den Zugriffsschlüssel, den wir zuvor in dieser Lektion für die einzelnen Aufrufe gespeichert.

1. Vorderseite im linken Menü die Option **Stimmung**. Diese Auswahl wird die Stimmung Dokumentation auf der rechten Seite geöffnet. Wie in die Dokumentation wird gezeigt, werden wir einen REST-Aufruf im folgenden Format vornehmen:

    `https://[location].api.cognitive.microsoft.com/text/analytics/v2.0/sentiment`

Übergeben wir in unserer Abonnementschlüssel und Zugriffsschlüssel die **Ocp-Apim-Subscription-Key** Header.

## <a name="make-some-api-calls"></a>Führen Sie einige API-Aufrufe

1. Wählen Sie eine Region aus der Liste auf dieser Seite, die den Speicherort, den wir ausgewählt entspricht, wenn Sie unsere Cognitive Services-Konto weiter oben in dieser Lektion erstellen.  Angenommen, wir haben uns entschieden *USA, Westen* bei der Erstellung des Kontos, wählen Sie ihn hier wie folgt.
    ![Screenshot der Textanalyse-API-Referenz-Website mit Stimmung Menüelement ausgewählt, gefolgt von West US.](../media/select-testing-console-region.png)

1. Die nächste Seite, die geöffnet wird, ist eine interaktive, API-Konsole.  Fügen Sie den Zugriffsschlüssel, die Sie gespeichert haben weiter oben in das Feld auf der Seite mit der Bezeichnung **Ocp-Apim-Subscription-Key**. Beachten Sie, dass der Schlüssel automatisch in das Fenster des HTTP-Anforderung als Headerwert geschrieben wird.

1. Führen Sie einen Bildlauf zum unteren Rand der Seite, und klicken Sie auf **senden**. Wir unterteilen, was geschieht, indem Sie diesen Bildschirm im Detail ansehen.

Im Header Abschnitt der Benutzeroberfläche legen wir den Zugriff oder die Abonnement-Schlüssel im Header der Anforderung.

![Screenshot des Header-Abschnitt.](../media/2-marker.PNG)

Als Nächstes müssen wir den Text der Anforderung im Abschnitt der enthält eine **Dokumente** Array. Jedes Dokument in das Array als drei Eigenschaften. Die Eigenschaften sind *"Sprache"*, *"Id"*, *"Text"*. Die *"Id"* ist eine Zahl in diesem Beispiel, jedoch kann sein, was Sie möchten, solange er in das Dokumentarray eindeutig ist. In diesem Beispiel haben wir in Dokumenten, die in drei verschiedenen Sprachen geschrieben und übergibt. Mehr als 15 Sprachen werden in die Stimmung-Funktion von der Textanalyse-API unterstützt. Weitere Informationen finden Sie in [unterstützte Sprachen der Textanalyse-API](https://docs.microsoft.com//azure/cognitive-services/text-analytics/text-analytics-supported-languages). Die maximale Größe eines einzelnen Dokuments beträgt 5.000 Zeichen und eine Anforderung kann bis zu 1.000 Dokumente.

![Screenshot der Request Body-Abschnitt](../media/3-marker.PNG)

Die vollständige Anforderung, einschließlich der Header und die Anforderungs-URL werden im nächsten Abschnitt angezeigt. In diesem Beispiel können Sie sehen, dass die Anforderungen weitergeleitet werden, um eine URL, die mit beginnen `westus`. Die URL unterscheidet sich abhängig von der gewählten Region.

![Anzahl der im Abschnitt 4. ](../media/4-marker.PNG)
 ![Nummer 5 des Abschnitts.](../media/5-marker.PNG)

Dann müssen wir Informationen über die Antwort. In diesem Beispiel sehen Sie, dass die Anforderung ein Erfolg und der Code war `200` zurückgegeben wurde. Wir sehen auch, dass der Roundtrip 38 ms gedauert hat.

![Anzahl der im Abschnitt 5.](../media/6-marker.PNG)

Abschließend sehen wir die Antwort auf der Anforderung. Die Antwort enthält die Einblicke, die die Textanalyse-API über unsere Dokumente haben. Ein Array von Dokumenten wird uns, ohne den ursprünglichen Text zurückgegeben. Wir erhalten ein *"Id"* und *"Score"* für jedes Dokument. Die API gibt einen numerischen Wert zwischen 0 und 1 zurück. Werte nahe 1 zeigen eine positive Absicht an, Werte nahe 0 zeigen eine negative Absicht an. Eine Bewertung von 0,5 gibt an, das Fehlen der Stimmung, eine neutrale-Anweisung. In diesem Beispiel haben wir zwei sehr positive Dokumenten und eine negative.

![Anzahl der im Abschnitt 5.](../media/7-marker.PNG)

Herzlichen Glückwunsch! Sie haben Ihren ersten Aufruf an die Textanalyse-API vorgenommen, ohne eine einzige Zeile Code schreiben zu müssen. Gerne bleiben in der Konsole, und probieren Sie weitere Aufrufe. Hier sind einige Vorschläge:

- Ändern Sie die Dokumente in Abschnittsnummer 2, und sehen Sie, was die API gibt zurück.
- Probieren Sie die anderen Methoden **Sprache erkennen**, **Entitäten** und **Schlüsselausdrücken**, mit dem gleichen Abonnementschlüssel.
- Versuchen Sie, einen Aufruf aus einer anderen Region mit Ihrem Abonnement sehen, was geschieht.

Der Test-API-Konsole ist eine hervorragende Möglichkeit, das die Funktionen dieser API zu erkunden. Nun, da Sie für sich selbst erläutert habe, betrachten wir nun diesen Daten in einem realen Szenario zu platzieren.