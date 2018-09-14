Sie haben eine Site erstellt und möchten sie in Azure bereitstellen. Jetzt müssen Sie überlegen, welche Azure-Dienste Ihre Anforderungen am besten erfüllen. App Service bietet einen hochgradig skalierbaren Webhostingdienst mit Self-Patching für Ihre Anwendungen.

Hier erfahren Sie, wie Sie Visual Studio verwenden, um Ihre ASP.NET Core-Webanwendung in einem Azure App Service-Plan zu veröffentlichen.

## <a name="what-is-web-apps"></a>Was sind Web-Apps?

Azure App Service ist ein Dienst für das Hosten von Webanwendungen, REST-APIs und mobilen Back-Ends. App Service unterstützt Code in einer Vielzahl von Sprachen, darunter beispielsweise .NET, .NET Core, Java, Ruby, Node.js, PHP und Python. App Service eignet sich ideal für die meisten Websites, insbesondere dann, wenn Sie nicht viel Kontrolle über die Hostinginfrastruktur benötigen.

## <a name="what-is-the-app-service-plan"></a>Was ist der App Service-Plan?

Der App Service-Plan definiert die Computeressourcen, die Ihre App in Anspruch nehmen wird, wo sich diese Ressourcen befinden, wie viele zusätzliche Ressourcen der Plan in Anspruch nehmen kann und welcher Typ von Dienstplan verwendet wird. Diese Computeressourcen entsprechen der Serverfarm beim herkömmlichen Webhosting. Sie können eine oder mehrere Apps zur Ausführung im selben App Service-Plan konfigurieren.

Wenn Sie Ihre Apps bereitstellen, können Sie einen App Service-Plan erstellen oder weiterhin Apps zu einem bestehenden Plan hinzufügen.  Dieselben Computeressourcen können jedoch nur von Apps im selben App Service-Plan genutzt werden. Um festzustellen, ob die neue App über die erforderlichen Ressourcen verfügt, müssen Sie die Kapazität des vorhandenen App Service-Plans und die erwartete Last für die neue App kennen. Das Überladen eines App Service-Plans kann für neue und vorhandene Apps unter Umständen zu Ausfallzeiten führen.

Sie können einen App Service-Plan im Azure-Portal mithilfe von PowerShell oder der Azure CLI vorab definieren oder einen Plan einrichten, während Sie Ihre Anwendung in Visual Studio veröffentlichen.

Jeder App Service-Plan definiert Folgendes:

- Region (USA Westen, USA Osten usw.)
- Anzahl der VM-Instanzen
- Größe der VM-Instanzen (klein, mittel, groß)
- Tarif (Free, Shared, Basic, Standard, Premium, Premium V2, Isolated)

## <a name="specify-the-region"></a>Angeben der Region

Wenn Sie einen App Service-Plan erstellen, müssen Sie eine Region oder einen Ort definieren, wo dieser Plan gehostet wird. In der Regel wählen Sie eine Region aus, die sich geografisch in der Nähe Ihrer zu erwartenden Kunden befindet.

## <a name="what-are-the-pricing-and-reliability-levels"></a>Was ist das Preisniveau, welches sind die Zuverlässigkeitsstufen?

Ein wichtiger Faktor bei der Bereitstellung von Apps in Azure App Service ist die Auswahl des richtigen Service-Plans. Ihr App Service-Plan kann jederzeit zentral hoch- und herunterskaliert werden. Sie können zuerst einen niedrigeren Tarif wählen und diesen dann später zentral hochskalieren, wenn Sie weitere App Service-Features benötigen.

Es gibt verschiedene Kategorien von Tarifen:

**Freigegebener Computemodus**: Bei **Free** und **Shared** (die beiden Basistarife) wird eine App auf derselben Azure-VM wie andere App Service-Apps ausgeführt, einschließlich der Apps anderer Kunden. Für diese Tarife werden CPU-Kontingente für jede App zugeteilt, die auf den freigegebenen Ressourcen ausgeführt wird, und für die Ressourcen ist das horizontale Hochskalieren nicht möglich.

Kostenlose Pläne und Shared-Pläne eignen sich am besten für kleinere persönliche Projekte mit stark eingeschränkten Anforderungen hinsichtlich des Datenverkehrs und mit einer festgelegten Begrenzung von 165 MB ausgehender Daten pro 24 Stunden.

**Dedizierter Computemodus**: In den Tarifen **Basic, Standard, Premium und Premium V2** werden Apps auf dedizierten Azure-VMs ausgeführt. Nur für Apps desselben App Service-Plans werden dieselben Computeressourcen gemeinsam genutzt. Je höher der Tarif ist, desto mehr VM-Instanzen stehen Ihnen für das horizontale Hochskalieren zur Verfügung.

Der Serviceplan Standard ist am besten für Live-Produktionsworkloads geeignet, wenn Sie kommerzielle Anwendungen für Kunden veröffentlichen.
Die Premium-Servicepläne unterstützen Web-Apps mit hoher Kapazität, bei denen die zusätzlichen Kosten eines dedizierten (isolieren) Plans vermieden werden sollen.

**Isolated**: Bei diesem Tarif werden dedizierte Azure-VMs in dedizierten Azure Virtual Networks ausgeführt, die eine Netzwerkisolation und eine Computeisolation für Ihre Apps ermöglichen. Sie verfügen hiermit über die maximalen Funktionen für die horizontale Skalierung. Sie wählen in der Regel nur dann einen isolierten Serviceplan aus, wenn Sie ein Höchstmaß an Sicherheit und Leistung benötigen.

Isolieren Sie Ihre App in einem neuen App Service-Plan, wenn Folgendes gilt:

- Die App ist ressourcenintensiv.
- Sie möchten die App unabhängig von den anderen Apps im vorhandenen Plan skalieren.
- Die App benötigt Ressourcen in einer anderen geografischen Region.

## <a name="specify-the-resource-group"></a>Angeben der Ressourcengruppe

Wie bei den meisten Azure-Ressourcen müssen Sie die Ressourcengruppe angeben, die Sie verwenden möchten. Sie können eine vorhandene Ressourcengruppe verwenden oder direkt aus Visual Studio eine Ressourcengruppe erstellen. Eine Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen wie z.B. Web-Apps, Datenbanken und Speicherkonten bereitgestellt und verwaltet werden. Dies ist ein nützlicher Mechanismus, um zugeordnete Ressourcen zusammenzuhalten.

## <a name="deploy-your-web-app-from-visual-studio"></a>Bereitstellen Ihrer Web-App aus Visual Studio

Das Veröffentlichen Ihrer App in Azure aus Visual Studio umfasst nur wenige Schritte.

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-the-project"></a>Auswählen des Projekts

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt.

1. Wählen Sie **Veröffentlichen > Veröffentlichen in Azure** aus.

### <a name="configure-the-app-service-plan-in-windows"></a>Konfigurieren des App Service-Plans unter Windows

1. Konfigurieren des App Service-Plans

    - Hosting: Sie konfigurieren Ihren App Service-Plan auf dieser Registerkarte. Hier werden der Standort, die Größe und die Features des Webservers angegeben, der Ihre App hostet. Sie können einen vorhandenen Hostingplan auswählen oder einen Plan erstellen. Windows generiert automatisch global eindeutige Namen, die Sie während des Setups ändern können.
    - Dienste: Sie können hier eine SQL-Datenbank für Ihre Site konfigurieren.

        > [!NOTE]
        > Sie können eine SQL-Datenbank in Azure zwar auch aus Visual Studio verbinden und verwalten, diese Vorgehensweise wird jedoch nicht im Rahmen des vorliegenden Moduls behandelt.

1. Klicken Sie zum Bereitstellen der App auf **Erstellen**. Nun startet Visual Studio die Webseite, auf der Ihre Site gehostet wird.

### <a name="configure-the-app-service-plan-for-mac"></a>Konfigurieren des App Service-Plans für Mac

1. Sie können einen vorhandenen App Service-Plan auswählen, sofern Sie einen solchen Plan in Azure eingerichtet haben, oder Sie können einen Plan erstellen.

1. Konfigurieren Sie Ihren App Service-Plan auf dieser Registerkarte. Hier werden der Standort, die Größe und die Features des Webservers angegeben, der Ihre App hostet. Sie können einen vorhandenen Hostingplan auswählen oder einen Plan erstellen. Denken Sie daran, dass in Azure der Name Ihrer Website und aller Ressourcen global eindeutig sein muss.

1. Klicken Sie zum Bereitstellen der App auf **Erstellen**. Nun startet Visual Studio die Webseite, auf der Ihre Site gehostet wird.

## <a name="summary"></a>Zusammenfassung

ASP.NET Core-Webanwendungen und Azure App Service bieten eine flexible, skalierbare Lösung für das Hosten Ihrer ASP.NET-Web-App. Wie bei allen Azure-Diensten müssen Sie eine Ressourcengruppe angeben und den Tarif auswählen, der Ihre Anforderungen am besten erfüllt.
