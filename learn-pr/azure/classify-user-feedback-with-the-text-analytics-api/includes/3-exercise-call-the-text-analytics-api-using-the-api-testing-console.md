Um die Textanalyse-API in Aktion zu sehen, führen wir einige Aufrufe mit der integrierten API-Testkonsole aus der Onlinereferenzdokumentation durch. Hierzu müssen wir aber zunächst einen Zugriffsschlüssel erstellen, um diese Aufrufe durchführen zu können.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-access-key"></a>Erstellen eines Zugriffsschlüssels

Für jeden Aufruf der Textanalyse-API ist ein Abonnementschlüssel erforderlich. Dieser wird häufig als Zugriffsschlüssel bezeichnet und dient der Überprüfung, ob Sie über Zugriff für den Aufruf verfügen. Hier verwenden Sie das Azure-Portal zum Abrufen eines Schlüssels.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

1. Klicken Sie auf **Ressource erstellen**.

1. Geben Sie im Suchfeld **Marketplace durchsuchen** *Textanalyse* ein, und drücken Sie die EINGABETASTE.

1. Wählen Sie in den Suchergebnissen **Textanalyse** aus, und klicken Sie dann unten rechts auf die Schaltfläche **Erstellen**.

1. Geben Sie auf der jetzt geöffneten Seite **Erstellen** die folgenden Werte in jedes Feld ein.

    |Eigenschaft  | Wert  | Beschreibung  |
    |---------|---------|---------|
    |Name     |    MyTextAnalyticsAPIAccount     |  Der Name des Cognitive Services-Kontos. Es wird empfohlen, einen beschreibenden Namen zu verwenden. Gültige Zeichen sind `a-z`, `0-9` und `-`.    |
    |Abonnement     |  Concierge-Abonnement    |   Das Abonnement, unter dem dieses neue Cognitive Services-API-Konto mit der **Textanalyse-API** erstellt wird.      |
    |Standort     |  *Region aus der Dropdownliste auswählen*       |  Da Sie die kostenlose Sandbox verwenden, wählen Sie einen Standort aus der Dropdownliste aus, der **ebenso** in der unten angezeigten Liste der Sandboxregionen enthalten ist.  |
    |Tarif     | **F0 Free**     |   Die Kosten für Ihr Cognitive Services-Konto hängen von der tatsächlichen Nutzung und den ausgewählten Optionen ab. Es wird empfohlen, zu unseren Zwecken den Tarif „Free“ auszuwählen.      |
    |Ressourcengruppe     |  Klicken Sie auf **Vorhandene verwenden**, und wählen Sie <rgn>[Name der Sandboxressourcengruppe]</rgn> aus.       |  Name für die neue Ressourcengruppe, in der Sie Ihr Cognitive Services-Konto für die Textanalyse-API erstellen.       |

    ### <a name="sandbox-region-list"></a>Liste der Sandboxregionen
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    > [!TIP]
    > Merken Sie sich den Standort, den Sie beim Erstellen des Cognitive Services-Kontos für die Textanalyse ausgewählt haben. Sie werden ihn in Kürze für API-Aufrufe verwenden. 

1. Wählen Sie unten auf der Seite **Erstellen** aus, um das Konto zu erstellen. Warten Sie auf eine Benachrichtigung, dass die Bereitstellung durchgeführt wird. Sie erhalten anschließend eine Benachrichtigung, dass das Konto erfolgreich in Ihrer Ressourcengruppe bereitgestellt wurde.

    ![Benachrichtigung über erfolgreiche Bereitstellung mit einer Schaltfläche „Zur Ressource wechseln“ und einer Schaltfläche „An Dashboard anheften“](../media/deploy-resource-group-success.PNG)

## <a name="get-the-access-key"></a>Abrufen des Zugriffsschlüssels

Da wir nun über ein Cognitive Services-Konto verfügen, werden wir den Zugriffsschlüssel abrufen, damit wird mit dem Aufruf der API beginnen können.

1. Klicken Sie in der Benachrichtigung *Bereitstellung erfolgreich* auf **Zu Ressource wechseln**. Hierdurch wird der Schnellstart zum Konto geöffnet.

1. Wählen Sie im Menü links oder im Abschnitt *Schlüssel abrufen* des Schnellstarts die Option **Schlüssel** aus. Hierdurch wird die Seite **Schlüssel verwalten** geöffnet.

1. Kopieren Sie einen der Schlüssel über die Schaltfläche zum Kopieren.

    ![Benutzeroberfläche zum Verwalten von Schlüsseln mit Anzeige des Cognitive Services-Kontos und den Einträgen für Schlüssel 1 und Schlüssel 2.](../media/manage-keys.PNG)

    > [!IMPORTANT]
    > Bewahren Sie Ihre Zugriffsschlüssel immer sicher auf, und geben Sie diese niemals weiter.

1. Speichern Sie diesen Schlüssel für die verbleibenden Abschnitte in diesem Modul. Wir benötigen diesen Schlüssel für die API-Aufrufe von der Testkonsole sowie in den verbleibenden Abschnitten des Moduls.

## <a name="call-the-api-from-the-testing-console"></a>Aufrufen der API von der Testkonsole

Nachdem wir nun über unseren Schlüssel verfügen, können wir zur Testkonsole wechseln und die API aufrufen.

1. Navigieren Sie in Ihrem bevorzugten Browser zu folgender URL. Ersetzen Sie `[location]` durch den Standort, den Sie weiter oben in dieser Lektion beim Erstellen des Cognitive Services-Kontos für die Textanalyse ausgewählt haben. Wenn Sie das Konto zum Beispiel in *USA, Osten* erstellt haben, ersetzen Sie in der URL `[location]` durch `eastus`.

    ```bash
    https://[location].dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0
    ```

    Auf der Landing Page wird links ein Menü und rechts Inhalt angezeigt. Im Menü werden die POST-Methoden aufgelistet, die Sie für die Textanalyse-API aufrufen können. Diese Endpunkte sind **Sprachenerkennung**, **Entitäten**, **Schlüsselbegriffe** und **Stimmung**. Um einen dieser Vorgänge aufzurufen, müssen Sie zunächst einige Schritte ausführen.

    - Wählen Sie die Methode aus, die Sie aufrufen möchten.
    - Fügen Sie jedem Aufruf den Zugriffsschlüssel hinzu, den Sie zu einem früheren Zeitpunkt in dieser Lektion gespeichert haben.

1. Wählen Sie im Menü links die Option **Stimmung** aus. Durch diese Auswahl wird auf der rechten Seite die zugehörige Dokumentation geöffnet. Wie die Dokumentation zeigt, führen wir einen REST-Aufruf im folgenden Format aus:  

    `https://[location].api.cognitive.microsoft.com/text/analytics/v2.0/sentiment`

     `[location]` wird durch den Standort ersetzt, den Sie beim Erstellen des Textanalyse-Kontos ausgewählt haben.  
Wir übergeben unseren Abonnementschlüssel (oder Zugriffsschlüssel) im Header **ocp-Apim-Subscription-Key**.

## <a name="make-some-api-calls"></a>Ausführen einiger API-Aufrufe

1. Klicken Sie auf die Schaltfläche **API-Testkonsole öffnen**, um die interaktive Live-API-Testkonsole zu öffnen.

1. Fügen Sie den zuvor gespeicherten Zugriffsschlüssel in das Feld **Ocp-Apim-Subscription-Key** ein. Beachten Sie, dass der Schlüssel automatisch als Headerwert in das HTTP-Anforderungsfenster geschrieben wird.

1. Scrollen Sie auf der Seite nach unten, und klicken Sie auf **Senden**.

    Sehen wir uns die Anzeige abschnittsweise genauer an.

    Im Headerabschnitt der Benutzeroberfläche wird der Zugriffs- oder Abonnementschlüssel im Header unserer Anforderung festgelegt.

    ![Screenshot des Headerabschnitts](../media/2-marker.PNG)

    Als Nächstes folgt der Abschnitt mit dem Anforderungstext, der ein Array aus **Dokumenten** enthält. Jedes Dokument im Array verfügt über drei Eigenschaften. Diese Eigenschaften sind *language*, *id* und *text*. Die Eigenschaft *id* ist in diesem Beispiel eine Zahl, könnte aber ein beliebiger Wert sein, solange dieser im Dokumentarray eindeutig ist. In diesem Beispiel übergeben wir Dokumente, die in drei unterschiedlichen Sprachen geschrieben sind. Das Stimmungsfeature der Textanalyse-API unterstützt mehr als 15 Sprachen. Weitere Informationen finden Sie unter [Unterstützte Sprachen in der Textanalyse-API](https://docs.microsoft.com//azure/cognitive-services/text-analytics/text-analytics-supported-languages). Ein einzelnes Dokument kann maximal 5.000 Zeichen enthalten, und eine einzelne Anforderung kann bis zu 1.000 Dokumente umfassen.

    ![Screenshot des Abschnitts mit dem Anforderungstext](../media/3-marker.PNG)

    Die vollständige Anforderung – einschließlich der Header und der Anforderungs-URL – wird im nächsten Abschnitt angezeigt. In diesem Beispiel können Sie sehen, dass die Anforderungen an eine URL geroutet werden, die mit `westus` beginnt. Die URL unterscheidet sich abhängig vom Standort, den Sie beim Erstellen Ihres Textanalyse-Kontos ausgewählt haben.

    ![Abschnitt 4](../media/4-marker.PNG)
    ![Abschnitt 5](../media/5-marker.PNG)

    Dann liegen Informationen zur Antwort vor. Im Beispiel war die Anforderung erfolgreich und hat den Code `200` zurückgegeben. Außerdem wird angezeigt, dass der Roundtrip 38 ms gedauert hat.

    ![Abschnitt 5](../media/6-marker.PNG)

    Schließlich wird die Antwort für unsere Anforderung angezeigt. Die Antwort enthält die Erkenntnisse zu unseren Dokumenten, die mit der Textanalyse-API gewonnen wurden. Es wird ein Array aus Dokumenten an uns zurückgegeben, ohne den ursprünglichen Text. Für jedes Dokument wird *id* (ID) und *score* (Bewertung) zurückgegeben. Die API gibt einen numerischen Wert zwischen 0 und 1 zurück. Werte nahe 1 zeigen eine positive Stimmung an, Werte nahe 0 zeigen eine negative Stimmung an. Eine Bewertung von 0,5 weist auf keine Stimmung hin, der Text ist neutral. In diesem Beispiel gibt es zwei deutlich positive Dokumente und ein negatives Dokument.

    ![Abschnitt 5](../media/7-marker.PNG)

Herzlichen Glückwunsch! Sie haben Ihren ersten Aufruf der Textanalyse-API ausgeführt, ohne auch nur eine Codezeile zu schreiben. Sie können gerne noch ein bisschen probieren und weitere Aufrufe ausführen. Hier einige Vorschläge:

- Ändern Sie die Dokumente in Abschnitt 2, und beachten Sie, was die API zurückgibt.
- Probieren Sie mit demselben Abonnementschlüssel die anderen Methoden aus: **Spracherkennung**, **Entitäten** und **Schlüsselbegriffe**.
- Versuchen Sie, einen Aufruf aus einer anderen Region mit Ihrem Abonnement auszuführen, und beobachten Sie, was passiert.

Die API-Testkonsole ist eine hervorragende Möglichkeit, die Funktionalität dieser API zu erkunden. Wenn Sie genügend probiert haben, lassen Sie uns diese Erkenntnisse in einem Szenario aus der Praxis umsetzen.