Ein großer Prozentsatz der Code in modernen Anwendungen vorhanden sind, die Bibliotheken und Abhängigkeiten, die von Ihnen ausgewählten: der Entwickler. Dies ist eine gängige Praxis, die Zeit und Geld spart. Der Nachteil ist jedoch, dass Sie jetzt für diesen Code, verantwortlich sind, auch wenn andere Benutzer ihn geschrieben hat, da Sie sie in Ihrem Projekt verwendet. Wenn eine Schwachstelle in einer dieser 3rd Party-Bibliotheken, Forscher (oder noch schlimmer ist, ein Hacker) ermittelt werden, und klicken Sie dann der gleiche Fehler wahrscheinlich auch vorhanden sein, in Ihrer app.

Verwenden von Komponenten mit bekannten Sicherheitsrisiken ist ein großes Problem in der Branche. Es ist deshalb problematisch, wurde die [OWASP Top 10-Liste](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) der schlechtesten Sicherheitsanfälligkeiten in Webanwendungen, über mehrere Jahre #9.

## <a name="track-known-security-vulnerabilities"></a>Verfolgen Sie bekannte Sicherheitsrisiken

Das Problem schon ist wissen, wenn ein Problem erkannt wird. Beibehalten von unserem Bibliotheken und-Abhängigkeiten aktualisierte (#4 in unserer Liste!) können sich natürlich, aber es ist eine gute Idee, zu verfolgen erkannte Sicherheitsrisiken, die Ihre Anwendung auswirken können.

> [!IMPORTANT]
> Wenn ein System eine bekannte Schwachstelle aufweist, ist es sehr wahrscheinlich auch Exploits verfügbar ist, Code zu verfügen, die Personen für solche Systeme Angriffe verwendet werden kann. Wenn ein Exploit veröffentlicht wird, ist es entscheidend, dass alle betroffenen Systemen sofort aktualisiert werden.

**Mitre** ist eine gemeinnützige Organisation, die verwaltet die [Common Vulnerabilities and Exposures Liste](https://cve.mitre.org). Diese Liste ist ein öffentlich durchsuchbaren Satz von bekannten Cybersecurity-Sicherheitsrisiken in apps, Bibliotheken und Frameworks. **Wenn Sie eine Bibliothek oder Komponente in der Datenbank CVE finden, hat es bekannte Schwachstellen**.

Probleme werden von der Community Security gesendet, wenn ein Sicherheitsrisiko in einem Produkt oder einer Komponente gefunden wird. Jedes veröffentlichte Problem eine ID zugewiesen ist, enthält das Datum, die ermittelt, wird eine Beschreibung des Sicherheitsrisikos, und Verweise auf veröffentlichte problemumgehungen oder Anbieter-Anweisungen zu diesem Problem.

### <a name="how-to-verify-if-you-have-known-vulnerabilities-in-your-3rd-party-components"></a>Gewusst wie: Überprüfen, ob Sie Schwachstellen in Ihren 3rd Party-Komponenten bekannte

Sie können tägliche Aufgabe in Ihrem Telefon, und überprüfen Sie diese Liste, aber zum Glück für uns viele Tools vorhanden und können Sie überprüfen, ob Abhängigkeiten anfällig sind. Sie können diese Tools für Ihre Codebasis ausgeführt oder besser noch, Hinzufügen der CI/CD-Pipeline zum automatisch als Teil des Entwicklungsprozesses für Probleme zu überprüfen.

- [OWASP Abhängigkeitsprüfung](https://www.owasp.org/index.php/OWASP_Dependency_Check), die eine [Jenkins-Plug-in](https://wiki.jenkins.io/display/JENKINS/OWASP+Dependency-Check+Plugin)
- [OWASP SonarQube](https://www.owasp.org/index.php/OWASP_SonarQube_Project)
- [Synk](https://snyk.io), dies ist kostenlos für open-Source-Repositorys auf GitHub
- [Black Duck](https://www.blackducksoftware.com) wird von vielen Unternehmen verwendet
- [RubySec](https://rubysec.com) einer Advise-Datenbank nur für Ruby
- [Retire.js](https://github.com/retirejs/retire.js/) ein Tool zum Überprüfen, wenn Ihre JavaScript-Bibliotheken veraltet; sind kann verwendet werden als Plug-In für die verschiedenen Tools, einschließlich [Burp Suite](https://www.portswigger.net)

Einige Tools, die speziell für die Analyse von statischem Code vorgenommen, können auch dafür verwendet werden.

- [Roslyn Security Guard](https://dotnet-security-guard.github.io)
- [Puma Scan](https://pumascan.com)
- [PT Application-Inspektor](https://www.ptsecurity.com/ww-en/products/ai/)
- [Apache Maven-Abhängigkeit-Plug-in](http://maven.apache.org/plugins/maven-dependency-plugin/)
- [Datenquelle löschen](https://www.sourceclear.com)
- [Sonatype](https://ossindex.sonatype.org)
- [Plattform für Knoten-Sicherheit](https://nodesecurity.io)
- [WhiteSource](https://www.whitesourcesoftware.com/what-is-whitesource/)
- [Hdiv](https://hdivsecurity.com)
- [Und vieles mehr...](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)

Weitere Informationen zu der Risiken im Zusammenhang mit gefährdeten Komponenten finden Sie auf die [OWASP-Seite](https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities) speziell für die in diesem Thema.

## <a name="summary"></a>Zusammenfassung

Bei Verwendung der Bibliotheken oder andere 3rd Party-Komponenten als Teil Ihrer Anwendung, die Sie auch auf alle Risiken dauert möglicherweise sie. Die beste Möglichkeit, dieses Risikos wird sichergestellt, dass Sie nur Komponenten verwenden, die keine bekannten Sicherheitsrisiken zugeordnet haben.
