Angenommen, Sie arbeiten für ein Unternehmen, das Statistiken von professionellen Sportlern nachverfolgt und eine API bereitstellt, um Ergebnisse abzufragen. Dadurch können Fans aktuelle und vergangene Spiele und Spielstände nachverfolgen und prüfen. Außerdem können die Benutzer über Suchen mit natürlicher Sprache Teamstatistiken abfragen. Beispiel: „Wie viele Tore hat Max Mustermann in der Nationalmannschaft bereits geschossen?“

In Spitzenzeiten (z.B. während einer Fußballweltmeisterschaft) verlängert sich die Antwortzeit Ihres Diensts, da der Back-End-Dienst nicht über die nötigen Kapazitäten verfügt, um die erhöhte Anzahl an Abfragen zu verarbeiten. Sie sollten die Leistung für Ihre Benutzer verbessern und die Workload in Ihren Back-End- und Datenspeicherdiensten reduzieren. Anhand Ihrer Daten lässt sich erkennen, dass 50 bis 80 % der zurückgegebenen Daten für schreibgeschützte oder kürzlich angeforderte Werte zurückgegebenen werden. Wenn Sie einen Cache für häufig verwendete Daten implementieren, kann die Leistung ggf. verbessert und die Latenz reduziert werden.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Beschreiben der Funktions- und Verwendungsweise von Redis Cache entsprechend Ihrer Unternehmensanforderungen
- Erstellen eines Entwurfs und Planen der Verwendung von Redis Cache
- Bereitstellen einer Redis Cache-Instanz in Azure
- Herstellen einer Verbindung zwischen einer Anwendung und dem Cache

## <a name="prerequisites"></a>Voraussetzungen

- Erfahrungen mit der Entwicklung von Apps
- Erfahrungen mit dem Verwenden von Daten in Apps
