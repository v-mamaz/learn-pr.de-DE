Sollten Sie verstehen, was mit Verwaltung geheimer Schlüssel Konfiguration von einer Anwendung auftreten können, suchen Sie nicht weiter als die Geschichte von Steve der leitende Entwickler.

Steve war in seinem Auftrag in einem Unternehmen der pet Food-Übermittlung für einige Wochen. Er wurde die Details des Unternehmens-Web-App untersuchen &mdash; bestellen eine .NET Core-Webanwendung, die Azure SQL-Datenbank zum Speichern von verwendet, Informationen und Drittanbieter-APIs für die Kreditkarte, Abrechnung und Zuordnen von Kundenadressen &mdash; wenn er die Verbindungszeichenfolge für die Auftragsdatenbank wird versehentlich in einem öffentlichen Forum eingefügt.

Tage später bemerkt berücksichtigt, dass das Unternehmen viele pet Food bereit war, die niemand bezahlt haben. Jemand hatte verwendet die Verbindungszeichenfolge für den Datenbankzugriff, das Schema Reverse Engineering und Aufträge ohne Umweg über die Website platziert.

Nach der Realisierung seine Fehler, geändert Steve hurriedly das Datenbankkennwort zum Sperren des Angreifer, unterbrechen die Website. Er direkt bei der Anwendungsserver angemeldet sind und die app-Konfiguration, anstatt die erneute Bereitstellung geändert werden, aber der Server wurde nicht erfolgreichen Anforderungen weiterhin angezeigt.

Steve vergessen hat, dass mehrere Instanzen der app auf verschiedenen Servern ausgeführt, und er musste nur die Konfiguration für einen geändert. Eine vollständige erneute Bereitstellung war erforderlich, eine andere 30 Minuten Ausfallzeit verursachen.

---

Verlust einer datenbankverbindung kann "string", "API-Schlüssel oder das Kennwort schwerwiegenden. Gestohlen oder gelöschten Daten, finanziellen Schaden, Ausfallzeiten der Anwendung und irreparablen Schäden an geschäftlichen Ressourcen und die Zuverlässigkeit der sind alle möglichen Ergebnisse. Leider müssen geheime Werte häufig gleichzeitig an mehreren Orten bereitgestellt und ungünstigen Zeitpunkten geändert werden. Und Sie sie speichern *an einer beliebigen Stelle!* Sehen wir uns an, wie wir all dies sicherer machen können.

## <a name="key-vault"></a>Key Vault

Key Vault ist ein *geheimnisspeicher*: eine zentrale Cloud-Dienst zum Speichern von anwendungsgeheimnissen. Key Vault hilft zu verhindern, dass die oben genannten Szenarien von geheime Schlüssel für Anwendungen in einem zentralen Ort speichern und Bereitstellen von sicherem Zugriff, Berechtigungen-Steuerelement, und die benutzerzugriffsprotokollierung.

Ein einzelnen Tresor ist eine Azure-Ressource mit eigenen Konfigurations- und Sicherheitsinformationen Richtlinie, die Sie mit der Azure standard-Management-Tools wie Azure-Portal oder die Befehlszeilenschnittstelle erstellen können. Verwaltung von Geheimnissen Zugriff und Vault erfolgt über eine REST-API. Jedem Tresor verfügt über eine eindeutige URL, unter dessen-API gehostet wird.

> [!IMPORTANT]
> **Key Vault dient zum Speichern von geheimen Konfigurationsinformationen für Server-Anwendungen.** Es dient nicht zum Speichern von Daten, die zu Ihrer app-Benutzer gehören, und es sollte nicht in der clientseitige Teil einer app verwendet werden. Dies wirkt sich die Leistungsmerkmale, die API und die Kosten Modell.
>
> Benutzerdaten sollte an anderer Stelle gespeicherten, z. B. Azure SQL-Datenbank mit Transparent Data Encryption, oder ein Speicherkonto mit Storage Service Encryption. Geheimnisse, die von Ihrer Anwendung verwendet werden, um diesen Datenspeicher zugreifen, können in Key Vault gespeichert werden.

## <a name="what-is-a-secret-in-key-vault"></a>Was ist ein Geheimnis in Key Vault?

In Key Vault ist ein Geheimnis ein Name / Wert-Paar von Zeichenfolgen. Geheimnisnamen muss 1 – 127 Zeichen lang sein, darf nur alphanumerische Zeichen und Bindestriche enthalten und in einem Tresor muss eindeutig sein. Ein geheimer Wert kann UTF-8-Zeichenfolge, bis zu 25KB groß sein.

> [!TIP]
> Geheimnisnamen nicht besonders geheimen selbst berücksichtigt werden müssen. Sie können diese in Ihrer app Konfiguration speichern, wenn Ihre Implementierung für sie aufruft. Dasselbe gilt für tresornamen und zu den URLs zur Verfügung.

> [!NOTE]
> Key Vault unterstützt zwei weitere Arten von geheimen Schlüsseln über Zeichenfolgen &mdash; *Schlüssel* und *Zertifikate* &mdash; und bietet nützliche Funktionen, die spezifisch für ihre Anwendungsfälle. Diese Funktionen und konzentriert sich auf die geheimen wie Kennwörter und Verbindungszeichenfolgen werden von der dieses Modul nicht behandelt.
