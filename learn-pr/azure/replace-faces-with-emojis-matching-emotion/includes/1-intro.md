Mojifier ist ein Slack-_Schrägstrich_-Befehl, der die Gesichter von Personen in Bildern durch Emojis ersetzt, die ihren Emotionen entsprechen:

![Beispielbild](/media-drafts/example-mojify-image.png)

Der Befehl ist so konzipiert, dass er von Slack aus als benutzerdefinierter Befehl ausgeführt werden kann. Sie können den Befehl beliebig benennen. In diesem Beispiel heißt er `mojify`.

Um den Befehlstyp auszuführen, geben Sie `/mojify <image to mojify>` ein:

![Beispielbild](/media-drafts/9.slack-type-mojify.png)

Mojifier führt daraufhin folgende Aktionen aus:

1.  Berechnen der Emotionen von Personen im Bild
2.  Zuordnen von Emotionen zu Emojis
3.  Ersetzen von Gesichtern durch Emojis
4.  Posten des Bilds auf Twitter als Antwort

Mojifier wurde mit TypeScript und verschiedenen Azure-Technologien geschrieben, darunter [Azure Functions](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai) und [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai).

In diesem Tutorial erfahren Sie, wie Mojifier entwickelt wurde, und wie Sie Ihren eigenen Slack-Befehl mit Azure-Technologien erstellen.

> Wo wird TODO nun angezeigt?
> Der gesamte Code für Mojifier ist unter [GitHub](https://github.com/jawache/mojifier) verfügbar.

# <a name="requirements"></a>Anforderungen

Um Mojifier zu erstellen, benötigen Sie unterschiedliche Azure-Dienste.

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Azure Cognitive Services umfasst eine Reihe von leistungsstarken APIs, mit denen Sie Ihrer Anwendung schnell erweiterte KI-Funktionen hinzufügen können. Wenn Sie eine HTTP-Anforderung erstellen können, können Sie Cognitive Services verwenden.

[Weitere Informationen](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)

## <a name="azure-functions"></a>Azure Functions

So leistungsstark wie Logic Apps ist, müssen Sie Geschäftslogik ggf. mit der gesamten Leistungsfähigkeit einer Programmiersprache schreiben. Azure Functions ist eine Technologie, mit der Sie Codeausschnitte hosten können, die auf Ereignisse oder HTTP-Anforderungen reagieren. Azure kümmert sich um die gesamte Skalierung, und Sie bezahlen nur die tatsächlich genutzten Ressourcen.

[Weitere Informationen](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai)
