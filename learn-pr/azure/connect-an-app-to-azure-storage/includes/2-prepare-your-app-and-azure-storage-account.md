Ihre Anwendung zum Teilen von Fotos erfordert die Speicherung verschiedener Arten von Daten. Sie müssen Binärdaten wie z.B. ein Foto und Textdaten wie einen Benutzernamen oder eine E-Mail-Adresse speichern. Wie jeder gute Entwickler müssen Sie sicherstellen, dass Sie die richtigen Überlegungen zum Entwurf vorgenommen haben, wenn Sie die Speicherart auswählen.

Hier lernen Sie einige Überlegungen zum Entwurf kennen, die Sie vor dem Auswählen einer Speicherstrategie berücksichtigen sollten. Sie wünschen etwas, das benutzerfreundlich, auf die Sprache Ihrer Wahl anwendbar, zuverlässig und schnell ist.

## <a name="design-considerations"></a>Überlegungen zum Entwurf

Azure Storage macht die Funktionalität mit einem HTTP-Endpunkt über das Internet verfügbar. Was geschieht, wenn Probleme mit der Internet-Konnektivität auftreten? Muss ich darüber hinaus Code schreiben, um eine Anforderung zu erstellen, mit dem Endpunkt zu kommunizieren und eine Antwort zu analysieren?

## <a name="connectivity-and-networking-issues"></a>Konnektivitäts- und Netzwerkprobleme

In einer idealen Welt ist ein Netzwerk 100% der Zeit verfügbar und immer zuverlässig. Dies ist jedoch keine realistische Erwartung. Da Speicher ein Teil fast aller Anwendungen ist, und Azure Storage-APIs über das Netzwerk verfügbar gemacht werden, müssen Sie die Auswirkungen eines Netzwerkausfalls berücksichtigen. Wenn Sie entscheiden, ob Azure Storage für Ihre Anforderungen geeignet ist, stellen Sie folgende Überlegungen an:

* Setzt Ihre Anwendung eine kontinuierliche Webkonnektivität voraus?

Wenn Sie eine Webanwendung erstellen, setzen Sie häufig voraus, dass immer Webkonnektivität verfügbar ist, mindestens in erster Linie für den Zugriff auf die Anwendung. Diese Tatsache vorauszusetzen, macht es sicherlich einfacher, Anwendungen zu schreiben, da weniger Code und Komplexität zum Behandeln von Offlineszenarios erforderlich sind. Nicht-Webanwendungen, z.B. die auf einem Desktop oder mobilen Gerät installierten, sind möglicherweise nicht in der Lage, von solchen Voraussetzungen auszugehen, und dies müssen Sie berücksichtigen, wenn Sie Ihre Anwendung entwerfen. Diese Apps mit vorausgesetzter konstanter Webkonnektivität sollten mindestens mit Verbindungsfehlern wie z.B. Netzwerkausfällen umgehen können, die von Zeit zu Zeit auftreten.

* Unterstützen Ihr Anwendungsentwurf und Ihre Implementierung einen beeinträchtigten Funktionssatz, wenn die Webkonnektivität ausfällt?

Wenn die Anwendung regulär getrennt oder zumindest in einem getrennten Zustand betrieben werden kann, wird sie dann korrekt herabgestuft, ohne einfach abzustürzen oder einen Fehler zu melden und nicht mehr verwendbar zu sein? Dies ist ein wichtiger Aspekt, da in der Verarbeitung von Trennungsszenarios viel Aufwand und Komplexität steckt. Sie können vielleicht bestimmte Teile der benötigten Daten lokal auf dem Gerät speichern, um Offlinebetrieb zuzulassen. Müssen bestimmte Elemente der Anwendung deaktiviert werden, bis die Konnektivität wiederhergestellt wird? Diese Überlegungen sind anwendungsspezifisch, und es ist wichtig, sie wg. des mit der Vorsorge für dieses Szenario verbundenen Aufwands frühzeitig in Entwurf und Implementierung einzuschließen.

## <a name="communicating-with-azure-storage"></a>Kommunikation mit Azure Storage

Wenn Sie Ihre Anwendung schreiben, möchten Sie sich in der Regel nicht übermäßig darum kümmern, Code zu schreiben, der sich auf Low-Level-Elemente wie z.B. das Formatieren von Daten zum Senden an Dienste für die Verarbeitung bezieht. Häufig werden Bibliotheken für Clients zur Kommunikation mit Diensten wie Azure Storage erstellt, um diese Aufgabe erheblich zu vereinfachen. Nicht alle Sprachen verfügen jedoch über Clientbibliotheken, die dies unterstützen.

* Gibt es eine verfügbare Clientbibliothek für den Technologiestapel Ihrer Wahl?

Wenn dies nicht der Fall ist, sind Sie damit zufrieden, Ihre eigenen Methoden für den Zugriff auf Dienstendpunkte zu erstellen, was in der Regel mehr Aufwand beinhaltet?

Wenn Bibliotheken verfügbar sind, stellen Sie sicher, dass eine für Ihren Technologiestapel zur Verfügung steht. Bei Verwendung gängigerer Technologiestapel wie .NET oder Java stehen in der Regel Clientbibliotheken zur Verfügung. Bei Verwendung nicht so gängiger Technologiestapel wie Haskel oder Scala ist dies möglicherweise nicht der Fall. Wenn Sie keine bereitgestellte Clientbibliothek verwenden, kann der zusätzliche Aufwand häufig beträchtlich sein und muss bei Entwurf und Implementierung Ihrer Anwendung berücksichtigt werden.

Für die Zwecke des Moduls und zur Vereinfachung gehen wir davon aus, dass wir eine .NET Core-Konsolenanwendung erstellen, die immer über Internetkonnektivität verfügen wird und nicht für die ordnungsgemäße Herabstufung der Funktionalität bei deren Nichtvorhandensein konzipiert ist.

## <a name="summary"></a>Zusammenfassung

Azure Storage ist ein flexibler und leistungsstarker Speicherungsmechanismus, der seine Funktionalität über eine Reihe von HTTP-API-Endpunkten verfügbar macht. Berücksichtigen Sie unbedingt die Auswirkungen von Netzwerkkonnektivitäts-Problemen sowie die Verfügbarkeit von Clientbibliotheken auf den Aufwand für Entwurf und Implementierung Ihrer Anwendung, um sicherzustellen, dass Azure Storage die richtige Wahl für Ihre Anwendung ist.

