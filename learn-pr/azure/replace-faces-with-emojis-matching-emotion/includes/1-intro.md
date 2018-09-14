TheMojifier ist eine Slack _Schrägstrich_ Peoples Gesichter auf Bildern mit übereinstimmenden ihre Emotionen, Emojis ersetzt Befehl wie folgt:

![Beispielbild](/media-drafts/example-mojify-image.png)

Es wurde entwickelt, um über Slack als einen benutzerdefinierten Befehl zu arbeiten. Sie können den Befehl was Ihnen gefallen hat, nicht aber für dieses Modul, wir nennen sie `mojify`.

Geben Sie zum Ausführen des Befehls `/mojify <image to mojify>`:

![Beispielbild](/media-drafts/9.slack-type-mojify.png)

Klicken Sie dann wird die Mojifier zur Verfügung:

  1.  Berechnen Sie die Emotionen überhaupt keine Personen in der Abbildung
  2.  Emotionen, Emojis übereinstimmen
  3.  Gesichter im Bild ersetzt mit emojis
  4.  Posten Sie das aktualisierte Image in Slack, als Antwort

Mithilfe von TypeScript und mehrere Azure-Technologien, einschließlich der Mojifier geschrieben [Azure Functions](https://azure.microsoft.com/services/functions/) und [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/). Sie verwenden diese, um Ihre eigene Version von stellen _TheMojifier_. 

> [!NOTE] 
> Alle Code für Mojifier ist verfügbar für [GitHub](https://github.com/microsoftdocs/mslearn-the-mojifier).

## <a name="tools-youll-use"></a>Tools, die Sie verwenden

### <a name="azure-cognitive-services"></a>Azure Cognitive Services

Azure Cognitive Services sind eine Reihe von allgemeinen APIs, die Sie verwenden können, schnell erweiterte künstliche Intelligenz (KI) Funktionen in eine app hinzuzufügen. Wenn Sie wissen wie eine HTTP-Anforderung, sollte dann Sie Cognitive Services verwenden können.

### <a name="azure-functions"></a>Azure Functions

Mit Azure Functions können, die Sie Codeausschnitte hosten, die auf Ereignisse oder HTTP-Anforderungen reagieren können. Azure kümmert sich um Skalierung Probleme, und Sie bezahlen nur für die tatsächliche Nutzung. Wie wird mit Elementen auf der Microsoft-Learn, Kosten für Sie in der Learning-Umgebung behandelt.
