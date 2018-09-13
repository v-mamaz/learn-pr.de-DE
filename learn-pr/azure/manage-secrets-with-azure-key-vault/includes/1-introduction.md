Wenn Sie wissen möchten, was bei der Verwaltung der Konfiguration von Geheimnissen einer Anwendung schief gehen kann, ist die Geschichte von Steve, dem Chefentwickler, genau das Richtige für Sie.

Steve hatte seinen Job bei einem Tierfutterlieferanten ein paar Wochen zuvor angetreten. Er untersuchte gerade die Details der Web-App des Unternehmens – einer .NET Core-Webanwendung, die eine Azure SQL-Datenbank zur Speicherung von Bestellinformationen und APIs von Drittanbietern für die Kreditkartenabrechnung und die Zuordnung von Kundenadressen verwendete – als er versehentlich die Verbindungszeichenfolge für die Auftragsdatenbank in ein öffentliches Forum einfügte.

Tage später bemerkte die Buchhaltung, dass das Unternehmen eine Menge Tiernahrung lieferte, für die niemand bezahlt hatte. Jemand hatte die Verbindungszeichenfolge verwendet, um auf die Datenbank zuzugreifen, das Schema (per Reverse Engineering) zurückentwickelt und Bestellungen aufgegeben, ohne über die Website zu gehen.

Nachdem er seinen Fehler erkannt hatte, änderte Steve umgehend das Datenbankkennwort, um den Angreifer von der Website auszuschließen, wodurch die Website gestört wurde. Er meldete sich direkt beim Anwendungsserver an und änderte die App-Konfiguration, anstatt sie neu bereitzustellen, aber der Server wies immer noch fehlerhafte Anforderungen auf.

Steve hatte vergessen, dass mehrere Instanzen der App auf verschiedenen Servern ausgeführt wurden, und nur die Konfiguration für einen davon geändert. Eine vollständige Neubereitstellung war erforderlich, was weitere 30 Minuten Ausfallzeit zur Folge hatte.

Das Preisgeben von Datenbank-Verbindungszeichenfolgen, API-Schlüsseln oder Dienstkennwörtern kann katastrophale Folgen haben. Gestohlene oder gelöschte Daten, finanzielle Schäden, Ausfallzeiten von Anwendungen und irreparable Schäden an Betriebsvermögen und Ruf sind mögliche Folgen. Leider müssen Werte von Geheimnissen oft an mehreren Stellen gleichzeitig bereitgestellt und zu ungünstigen Zeiten geändert werden. Und Sie müssen sie ja irgendwo *speichern*! Sehen wir uns an, wie wir das alles mit Azure Key Vault sicherer gestalten können.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Verstehen, welche Arten von Informationen in Azure Key Vault gespeichert werden können
- Erstellen eines Azure Key Vault-Stores
- Authentifizieren bei Azure Key Vault
- Zugreifen auf Geheimnisse in Azure Key Vault