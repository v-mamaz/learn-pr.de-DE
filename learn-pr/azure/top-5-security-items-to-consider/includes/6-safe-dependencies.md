Bei einem großen Prozentsatz des Codes in modernen Anwendungen handelt es sich um die Bibliotheken und Abhängigkeiten, die Sie als Entwickler auswählen. Die Verwendung von Drittanbieterkomponenten ist eine gängige Praxis, die Zeit und Geld spart. Der Nachteil: Obwohl der Code von jemand anderem geschrieben wurde, sind Sie, weil Sie ihn in Ihrem Projekt verwendet haben, jetzt für ihn verantwortlich. Wenn ein Sicherheitsexperte (oder schlimmer noch ein Hacker) ein Sicherheitsrisiko in einer dieser Drittanbieterbibliotheken entdeckt, wird der Fehler wahrscheinlich auch in Ihrer App vorhanden sein.

Die Verwendung von Komponenten mit bekannten Sicherheitsrisiken ist ein großes Problem in unserer Branche. Sie ist derart problembehaftet, dass sie seit mehreren Jahren in Folge den neunten Platz auf der [OWASP-Top-10-Liste](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) der schwerwiegendsten Sicherheitsrisiken in Webanwendungen einnimmt.

## <a name="track-known-security-vulnerabilities"></a>Nachverfolgen bekannter Sicherheitsrisiken

Für uns besteht das Problem darin, zu wissen, wann ein Problem erkannt wurde. Bibliotheken und Abhängigkeiten auf dem neuesten Stand zu halten (Nr. 4 auf unserer Liste!), ist natürlich hilfreich. Es empfiehlt sich aber auch, identifizierte Sicherheitsrisiken, die sich auf Ihre Anwendung auswirken können, nachzuverfolgen.

> [!IMPORTANT]
> Wenn ein System ein bekanntes Sicherheitsrisiko aufweist, ist die Wahrscheinlichkeit deutlich höher, dass auch Exploits verfügbar sind (d. h. Code, der für Angriffe auf solche Systeme genutzt werden kann). Wenn ein Exploit veröffentlicht wird, ist es entscheidend, dass alle betroffenen Systeme sofort aktualisiert werden.

**Mitre** ist eine gemeinnützige Organisation, die die [Common Vulnerabilities and Exposures (CVE) List](https://cve.mitre.org) (Liste der häufigen Sicherheitsrisiken und Sicherheitslücken) führt. Diese Liste ist eine öffentlich zugängliche durchsuchbare Sammlung von bekannten Cybersicherheitsrisiken in Apps, Bibliotheken und Frameworks. **Eine Bibliothek oder Komponente, die Sie in der CVE-Datenbank finden, weist bekannte Sicherheitsrisiken auf**.

Probleme werden von der Sicherheitscommunity gemeldet, wenn eine Sicherheitslücke in einem Produkt oder einer Komponente gefunden wird. Jedem veröffentlichten Problem ist eine ID zugewiesen, die das Datum der Entdeckung, eine Beschreibung des Sicherheitsrisikos und Verweise auf veröffentlichte Problemumgehungen oder Angaben des Anbieters zum Problem enthält.

### <a name="how-to-verify-if-you-have-known-vulnerabilities-in-your-3rd-party-components"></a>Überprüfen, ob Ihre Drittanbieterkomponenten bekannte Sicherheitsrisiken aufweisen

Sie könnten eine tägliche Aufgabe auf Ihrem Smartphone einrichten, um diese Liste jeden Tag zu überprüfen. Zu unserem Glück gibt es jedoch viele Tools, mit denen wir prüfen können, ob unsere Abhängigkeiten gefährdet sind. Sie können diese Tools für Ihre Codebasis ausführen oder – noch besser – Ihrer CI/CD-Pipeline hinzufügen, um im Rahmen des Entwicklungsprozesses automatisch zu überprüfen, ob Probleme vorliegen.

- [OWASP Dependency Check](https://www.owasp.org/index.php/OWASP_Dependency_Check) – ein Tool, für das ein [Jenkins-Plug-In](https://wiki.jenkins.io/display/JENKINS/OWASP+Dependency-Check+Plugin) verfügbar ist
- [OWASP SonarQube](https://www.owasp.org/index.php/OWASP_SonarQube_Project)
- [Synk](https://snyk.io) – ein Tool, das für Open Source-Repositorys auf GitHub kostenlos verfügbar ist
- [Black Duck](https://www.blackducksoftware.com) – ein Tool, das von vielen Unternehmen verwendet wird
- [RubySec](https://rubysec.com) – eine Empfehlungsdatenbank nur für Ruby
- [Retire.js](https://github.com/retirejs/retire.js/) – ein Tool, mit dem Sie überprüfen können, ob Ihre JavaScript-Bibliotheken veraltet sind (kann als Plug-In für verschiedene Tools verwendet werden, einschließlich [Burp Suite](https://www.portswigger.net))

Einige spezielle Tools für die statische Codeanalyse können ebenfalls zu diesem Zweck verwendet werden.

- [Roslyn Security Guard](https://dotnet-security-guard.github.io)
- [Puma Scan](https://pumascan.com)
- [PT Application Inspector](https://www.ptsecurity.com/ww-en/products/ai/)
- [Apache Maven Dependency Plugin](http://maven.apache.org/plugins/maven-dependency-plugin/)
- [Source Clear](https://www.sourceclear.com)
- [Sonatype](https://ossindex.sonatype.org)
- [Node Security Platform](https://nodesecurity.io)
- [WhiteSource](https://www.whitesourcesoftware.com/what-is-whitesource/)
- [Hdiv](https://hdivsecurity.com)
- [Und viele mehr...](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)

Weitere Informationen zu den Risiken im Zusammenhang mit der Verwendung gefährdeter Komponenten finden Sie auf der [OWASP-Seite](https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities) zu diesem Thema.

## <a name="summary"></a>Zusammenfassung

Wenn Sie Bibliotheken oder andere Drittanbieterkomponenten als Teil Ihrer Anwendung nutzen, übernehmen Sie auch sämtliche Risiken, die diese möglicherweise aufweisen. Am besten lässt sich dieses Risiko reduzieren, indem Sie nur Komponenten ohne bekannte Sicherheitsrisiken verwenden.
