Im Vergleich zu üblichen lokalen Bereitstellungen bietet das Hosten von Anwendungen auf einer Cloudplattform mehrere Vorteile. Im Rahmen des Cloudmodells „Shared Responsibility“ (gemeinsame Verantwortung) unterliegen Sicherheitsaspekte auf der Ebene des physischen Netzwerks sowie auf der Gebäude- und Hostebene der Verantwortung des Cloudanbieters. Für einen Angreifer würde sich die Kompromittierung der Plattform auf dieser Ebene kaum lohnen, da dessen Aufwand erheblichen Investitionen und umfassenden Erkenntnissen des Anbieters gegenübersteht, der seine Infrastruktur auf diese Weise sichert und überwacht.

Angreifer sind daher vielmehr an der Ausnutzung von Sicherheitsrisiken interessiert, die durch Kunden der Cloudplattform auf der Anwendungsebene eingeführt werden. Durch den Einsatz einer PaaS-Strategie (Platform-as-a-Service) zum Hosten von Anwendungen müssen Kunden darüber hinaus ihre Ressourcen nicht mehr zum Verwalten der Betriebssystemsicherheit aufwenden. Stattdessen können diese zur Härtung von Anwendungscode und Überwachung von Identitäten im Zusammenhang mit dem Zugriff auf Anwendungen eingesetzt werden. In dieser Einheit erfahren Sie, wie die Anwendungssicherheit über das Anwendungsdesign verbessert werden kann.

## <a name="scenario"></a>Szenario

Kunden des Unternehmens Lamna Healthcare müssen über ein Webportal auf ihre Patientenakten zugreifen können. Die Einhaltung des US-amerikanischen HIPAA-Gesetzes (Health Insurance Portability and Accountability Act) ist verpflichtend und setzt das Unternehmen einem erheblichen Risiko für Strafzahlungen aus, falls durch eine Sicherheitsverletzung personenbezogene Daten gestohlen werden. Die Absicherung der Anwendung sowie der personenbezogenen Daten der Patienten ist daher von größter Wichtigkeit.

Für Kundenanwendungen sind primär die folgenden Bereiche relevant:

- sicherer Anwendungsentwurf
- Datensicherheit
- Identitäts- und Zugriffsverwaltung
- Sicherheit des Endpunkts

## <a name="security-development-lifecycle"></a>Security Development Lifecycle

Der [Security Development Lifecycle](https://www.microsoft.com/sdl) (SDL) von Microsoft kann während der Entwurfsphase der Anwendung verwendet werden, um sicherzustellen, dass Sicherheitsrisiken während des gesamten Lebenszyklus der Softwareentwicklung berücksichtigt werden. Sicherheits- und Konformitätsprobleme können in der Entwurfsphase einer Anwendung deutlicher leichter als in anderen Phasen behoben werden. So lassen sich häufig auftretende Fehler vermeiden, die zu Sicherheitslücken im Endprodukt führen können. Wenn Probleme in der frühen Entwicklungsphase behoben werden, führt dies außerdem zu geringeren Kosten. Für Softwareprojekt werden üblicherweise die folgenden SDL-Schritte umgesetzt:

1. Schulungen

    - Schulungen zum Thema grundlegender Sicherheit

1. Anforderungen

    - Definieren von Anforderungen und Quality Gates (Meilensteine, bei denen mithilfe definierter Qualitätskriterien über den weiteren Projektverlauf entschieden wird)
    - Analysieren von Risiken für Sicherheit und Datenschutz
 
1. Entwurf

    - Analysieren der Angriffsfläche
    - Bedrohungsmodellierung
 
1. Implementierung

    - Festlegen von Tools zur Messung der Codequalität
    - Festlegen von APIs und Funktionen, die nicht verwendet dürfen
    - Ausführen statischer Codeanalysen
    - Überprüfen von Repositorys auf gespeicherte Geheimnisse
 
1. Überprüfung

    - Dynamische Tests und Fuzzing
    - Überprüfen der Bedrohungsmodelle/Angriffsflächen
 
1. Release

    - Entwerfen eines Sicherheitsplans für Bedrohungen
    - Ausführen einer abschließenden Sicherheitsüberprüfung
    - Releasearchiv
 
1. Reaktion auf Bedrohungen 

    - Ausführen eines Reaktionsplans bei Bedrohungen

![Abbildung zu Security Development Lifecycle](../media/sdl.png)

SDL ist nicht einfach nur ein Prozess oder Toolset, sondern in gleichem Maße ein Aspekt einer Unternehmenskultur. Wenn es gelingt, eine Organisationskultur zu schaffen, in der das Thema Sicherheit bei der Anwendungsentwicklung ein Hauptschwerpunkt und zugleich eine Anforderung ist, kann dies deutlich zum Ausbau sicherheitsbezogener Kompetenzen in Organisationen führen.

<!-- Bear in mind that the migration of un-modified applications (especially COTS procured software systems) will not be able to perform many of the steps listed above.
 -->

## <a name="operational-security-assessment"></a>Bewertung der Betriebssicherheit

Nach der Bereitstellung einer Anwendung muss deren Sicherheitsstatus kontinuierlich überwacht werden. Außerdem muss festgelegt werden, wie mit möglichen Problemen umgegangen wird. Dieses Wissen muss anschließend in den Softwareentwicklungszyklus einfließen. Wie genau diese Vorgänge umgesetzt werden, entscheidet über den Reifegrad der Softwareentwicklung, der operativen Teams und der Datenschutzanforderungen.

Mit Scansoftware für Sicherheitsrisiken stehen Dienste bereit, mit denen Sie diesen Prozess automatisieren und mögliche Sicherheitsprobleme in regelmäßigen Abständen bewerten können, ohne dabei Teams mit kostspieligen manuellen Vorgängen wie Penetrationtests zu belasten.

Azure Security Center ist ein kostenloser Dienst, der mittlerweile standardmäßig für alle Azure-Abonnements aktiviert ist. Er ist fest in andere Azure-Dienste auf Anwendungsebene wie Azure Application Gateway und Azure Web Application Firewall integriert. Azure Security Center analysiert Protokolle dieser Dienste und meldet daraufhin Sicherheitsrisiken in Echtzeit. Außerdem werden Gegenmaßnahmen zur Verringerung der Risiken vorgeschlagen. Darüber hinaus kann der Dienst auch so konfiguriert werden, dass bei Angriffen automatisch Playbooks ausgeführt werden.

<!-- SDL culture
Key Vault / MSI
CSE = App  -> DB & App Storage
Mention approach of code scanning & SDL
Scanning for passwords - Git
 -->

## <a name="identity-as-the-perimeter"></a>Identität als Zugriffskriterium

Die Identitätsüberprüfung wird beim Schutz von Anwendungen zunehmend zur ersten Verteidigungslinie. Wenn der Zugriff auf eine Webanwendung durch die Authentifizierung und Autorisierung von Sitzungen eingeschränkt wird, kann dies die Angriffsfläche deutlich reduzieren. Azure AD und Azure AD B2C stellen eine wirksame Methode bereit, die Identitäts- und Zugriffsverwaltung an einen vollständig verwalteten Dienst auszulagern. Durch Richtlinien für bedingten Zugriff, Privileged Identity Management und Identity Protection können Kunden in Azure AD noch effektiver unbefugte Zugriffe verhindern und Änderungen überwachen.

## <a name="data-protection"></a>Schutz von Daten

Bei den meisten, wenn nicht sogar allen Angriffen auf Webanwendungen, sind Kundendaten das Ziel. Die sichere Speicherung und Übertragung von Daten zwischen einer Anwendung und der Datenspeicherebene ist von allergrößter Bedeutung.

Lamna Healthcare speichert überaus sensible Daten im Zusammenhang mit Patientenakten und greift auf diese Daten zu. Im HIPAA-Gesetz, das 1996 vom US-Kongress erlassen wurde, werden im Zusammenspiel mit einigen weiteren Regulierungen nationale Standards für elektronische Transaktionen von Patientendaten definiert. Diese Standards gelten für Gesundheitsdienstleister und Arbeitgeber. Lamna muss sicherstellen, dass Patienten und berechtigte Dritte, wie z.B. die Ärzte der Patienten, sicher auf die Krankendaten zugreifen können.

Um diese Anforderungen zu erfüllen, hat Lamna Healthcare seine Anwendungen so angepasst, dass alle ruhenden und übertragenen Patientendaten verschlüsselt werden. Mit Transport Layer Security (TLS) werden beispielsweise Daten zwischen der Webanwendung und den Back-End-SQL-Datenbanken verschlüsselt. Ruhende Daten werden auch in SQL Server mit Transparent Data Encryption (TDE) verschlüsselt. Dadurch wird sichergestellt, dass selbst bei einer Kompromittierung der Umgebung die Daten ohne die korrekten Entschlüsselungsschlüssel nicht lesbar sind.

Zum Verschlüsseln von gespeicherten Daten im Blobspeicher kann die clientseitige Verschlüsselung verwendet werden, um Daten im Speicher zu verschlüsseln, bevor diese in den Speicherdienst geschrieben werden. Bibliotheken, die diese Verschlüsselung unterstützen, sind für .NET, Java und Python verfügbar. Mit diesen können Technologien zur Datenverschlüsselung direkt in Anwendungen integriert werden, wodurch die Datenintegrität erhöht wird.

### <a name="secure-key-and-secret-storage"></a>Sichere Schlüssel und Geheimnisspeicher

Anwendungsgeheimnisse (beispielsweise Verbindungszeichenfolgen und Kennwörter) und Verschlüsselungsschlüssel, die für den Zugriff auf Daten benötigt werden, dürfen unter keinen Umständen in der Anwendung hinterlegt sein. Derartige Daten sollten nie im Anwendungscode von Konfigurationsdateien gespeichert werden. Stattdessen sollte ein sicherer Speicher wie Azure Key Vault verwendet werden. Dadurch kann der Zugriff auf vertrauliche Daten mithilfe verwalteter Dienstidentitäten auf Anwendungsidentitäten beschränkt werden. Außerdem kann durch eine regelmäßige Schlüsselrotation verhindert werden, dass Verschlüsselungsschlüssel im Fall einer unbeabsichtigten Veröffentlichung von Dritten verwendet werden können. Kunden können sich darüber hinaus dafür entscheiden, ihre eigenen Verschlüsselungsschlüssel zu nutzen, die von lokalen Hardwaresicherheitsmodulen (HSM) generiert werden. Des Weiteren können Kunden anordnen, dass Azure Key Vault-Instanzen in eigenständigen HSMs für nur einen Mandanten implementiert werden.

<!-- ### Secure and immutable file storage

All Azure storage accounts are encrypted by default using Microsoft managed keys. Azure customers also have the ability to use their own encryption keys (BYOK) to encrypt blob, file and queue data so that even the hosting provider has no access to unencrypted data. Data immutability is often required for auditing purposes or when legal disputes call for data to be effectively frozen for a determined amount of time. Azure has recently introduced an [immutable data storage](https://docs.microsoft.com/azure/storage/blobs/storage-blob-immutable-storage) option known as Write-Once, Read many (WORM) for this scenario. -->
