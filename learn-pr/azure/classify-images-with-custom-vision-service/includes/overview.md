Bei [Microsoft Cognitive Services](https://azure.microsoft.com/en-us/services/cognitive-services/ "Microsoft Cognitive Services") handelt es sich um eine Sammlung von Diensten und APIs, die durch Machine Learning unterstützt werden und Entwicklern das Integrieren von intelligenten Features wie Gesichtserkennung in Fotos und Videos, Stimmungsanalyse in Texten und Language Understanding in ihre Anwendungen ermöglicht. [Custom Vision Service](https://azure.microsoft.com/en-us/services/cognitive-services/custom-vision-service/) wurde erst kürzlich von Microsoft zur Cognitive Services-Sammlung hinzugefügt. Dieser Dienst soll Modelle zur Bildklassifizierung erstellen, die anhand von bereitgestellten gekennzeichneten Bildern „lernen“. Sie würden gerne wissen, ob auf einem bestimmten Bild eine Blume zu finden ist? Trainieren Sie Custom Vision Service mit einer Sammlung von Blumen, auf denen Bilder dargestellt sind. Dann kann der Dienst Ihnen mitteilen, ob auf dem nächsten Bild eine Blume zu sehen ist und sogar, um welche Art von Blume es sich handelt.

### <a name="what-is-covered-in-this-lab"></a>Welche Themen werden in dieser Übungseinheit behandelt?
In dieser Übungseinheit werden folgende Vorgänge beschrieben:
* Erstellen eines Custom Vision Service-Projekts 
* Trainieren eines Custom Vision Service-Modells mit gekennzeichneten Bildern  
* Testen eines Custom Vision Service-Modells 
* Erstellen von Apps, die Custom Vision Service-Modelle nutzen, um REST-APIs aufzurufen

Für diese Übung benötigen Sie ein Microsoft-Konto. Falls Sie noch keines besitzen, können Sie sich [kostenlos registrieren](https://account.microsoft.com/account). Außerdem benötigen Sie Visual Studio Code und Node.js.