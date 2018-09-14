Angenommen, Sie arbeiten für ein Unternehmen, das Statistiken von professionellen Sportlern nachverfolgt und eine API für Apps bereitstellt, um Lösungen abzufragen. Dadurch können Fans aktuelle und vergangene Spiele und Spielstände nachverfolgen und prüfen. Außerdem können die Benutzer über Suchen mit natürlicher Sprache Teamstatistiken abfragen. Z.B.: „Wie viele Tore hat Max Mustermann in der Nationalmannschaft bereits geschossen?“

Während einer Fußballweltmeisterschaft verlangsamt sich die Antwortzeit Ihres Diensts, da der Back-End-Dienst nicht über die nötigen Kapazitäten verfügt, um die erhöhte Anzahl an Abfragen zu verarbeiten. Sie sollten die Leistung für Ihre Benutzer verbessern und die Workload auf Ihren Back-End- und Datenspeicherdiensten reduzieren. Anhand Ihrer Daten lässt sich erkennen, dass 50 bis 80 % der zurückgegebenen Daten für schreibgeschützte oder kürzlich angeforderte Werte zurückgegebenen werden. Wenn Sie einen Cache für häufig verwendete Daten implementieren, kann die Leistung ggf. verbessert und die Latenz reduziert werden.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul wird Folgendes thematisiert:

- Beschreiben der Funktions- und Verwendungsweise von Redis Cache
- Erstellen eines Entwurfs und Planen der Verwendung von Redis Cache
- Bereitstellen von Redis Cache in Azure
- Herstellen einer Verbindung zwischen einer Web-App und dem Cache

## <a name="prerequisites"></a>Voraussetzungen

- Erfahrungen mit der Entwicklung von Apps
- Erfahrungen mit dem Verwenden von Daten in Apps
