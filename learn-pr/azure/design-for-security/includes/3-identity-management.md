Lamna Healthcare hostet eine ältere interne Anwendung und ein Webportal für Ärzte zur Verwaltung von Patientendaten. Die Organisation hat viele Anfragen erhalten, diese Anwendung Pflegekräften zur Verfügung zu stellen, die sich oft vor Ort bei Patienten und somit außerhalb des Netzwerks befinden. 

Aufgrund eines kürzlich durch schädliche Agents verursachten Datenverlusts hat das Unternehmen die Kennwortrichtlinien verschärft. Benutzer müssen nun ihre Kennwörter häufiger ändern und längere, komplexere Kennwörter verwenden. Dies hat den unerwünschten Nebeneffekt, dass Benutzer Schwierigkeiten haben, komplexe Kennwörter aufzubewahren, die mehrere Sätze Anmeldeinformationen enthalten, die für verschiedene Administratorrollen erstellt wurden. 

Hier werden Identität als Sicherheitsebene für interne und externe Anwendungen, die Vorteile des einmaligen Anmeldens (Single Sign-On, SSO) und der mehrstufigen Authentifizierung (MFA) zur Gewährleistung der Identitätssicherheit und die Gründe für die Replikation lokaler Identitäten in Azure Active Directory behandelt.

## <a name="identity-as-a-layer-of-security"></a>Identität als Sicherheitsebene

Digitale Identitäten sind ein integraler Bestandteil der heutigen geschäftlichen und sozialen Interaktionen vor Ort und online. In der Vergangenheit beschränkten sich Identitäts- und Zugriffsdienste auf das interne Netzwerk eines Unternehmens unter Verwendung von Protokollen wie Kerberos und LDAP, die für diesen Zweck entwickelt wurden. In jüngster Zeit sind mobile Geräte zur wichtigsten Form der Interaktion mit digitalen Diensten geworden. Kunden und Mitarbeiter erwarten, dass sie jederzeit und von überall auf Dienste zugreifen können. Dies hat die Entwicklung von Identitätsprotokollen vorangetrieben, die im Internet über mehrere verschiedene Geräte und Betriebssysteme hinweg ausgeführt werden können.

Während die Fähigkeiten der Architektur rund um die Identität bewertet werden, prüft Lamna Healthcare, wie die folgenden Funktionen in Anwendungen integriert werden können:

- Bereitstellen des einmaligen Anmeldens für Anwendungsbenutzer
- Verbessern der älteren Anwendung, um moderne Authentifizierung mit minimalem Aufwand zu nutzen
- Erzwingen der mehrstufigen Authentifizierung für alle Anmeldungen außerhalb des Unternehmensnetzwerks
- Entwickeln einer Anwendung, mit der Patienten ihre Kontodaten registrieren und sicher verwalten können

## <a name="single-sign-on"></a>Einmaliges Anmelden

Je mehr Identitäten ein Benutzer verwalten muss, desto größer ist das Risiko eines Sicherheitsincidents in Zusammenhang mit Anmeldeinformationen. Mehrere Identitäten implizieren mehrere Kennwörter, die verwaltet und geändert werden müssen. Kennwortrichtlinien können zwischen den Anwendungen variieren, und da die erforderliche Kennwortkomplexität zunimmt, wird es für Benutzer immer schwieriger, sich an diese zu erinnern.

Außerdem ist die Verwaltung all dieser Identitäten erforderlich. Helpdesks werden beim Bearbeiten von Kontosperrungen und Kennwortzurücksetzungen zusätzlich belastet. Wenn ein Benutzer ein Unternehmen verlässt, kann es zudem schwierig sein, alle seine Identitäten zu finden und zu deaktivieren. Falls eine Identität übersehen wird, könnte der Benutzer weiterhin unerwünschten Zugriff erhalten.

Einmaliges Anmelden erfordert nur eine Identität und nur ein Kennwort. Der anwendungsübergreifende Zugriff wird einer einzigen, benutzerspezifischen Identität gewährt, wodurch das Sicherheitsmodell vereinfacht wird. Wenn Benutzer die Rolle wechseln oder ein Unternehmen verlassen, sind Zugriffsänderungen an die einzelne Identität gebunden. So wird der Aufwand für das Ändern oder Deaktivieren von Konten erheblich reduziert. Das einmalige Anmelden für Konten erleichtert Benutzern die Verwaltung ihrer Identitäten und erhöht die Sicherheitsfunktionen in Ihrer Umgebung.

### <a name="sso-with-azure-active-directory"></a>Einmaliges Anmelden mit Azure Active Directory

Azure Active Directory (AAD) ist ein cloudbasierter Identitätsdienst. Er hat eine integrierte Unterstützung für die Synchronisierung mit Ihrem vorhandenen lokalen Active Directory-Verzeichnis oder kann einzeln verwendet werden.

Das bedeutet, dass alle Ihre Anwendungen – ob lokal, in der Cloud (einschließlich Office 365) oder mobil – dieselben Anmeldeinformationen verwenden können. 

Administratoren und Entwickler können den Zugriff auf Daten und Anwendungen mithilfe zentralisierter Regeln und Richtlinien steuern, die in Azure AD konfiguriert sind.

Darüber hinaus ist Microsoft in der einzigartigen Position, mehrere Datenquellen zu einem Intelligent Security Graph zu kombinieren, der Bedrohungsanalysen und Echtzeit-Identitätsschutz für alle Konten in Azure Active Directory bietet. Dies gilt auch für Konten, die von Ihrem lokalen AD synchronisiert werden.

### <a name="synchronize-directories-with-ad-connect"></a>Synchronisieren von Verzeichnissen mit AD Connect

Azure AD Connect integriert Ihre lokalen Verzeichnisse in Azure Active Directory. Azure AD Connect bietet die neuesten Funktionen und ersetzt ältere Versionen von Identitätsintegrationstools wie DirSync und Azure AD Sync.

Es handelt sich um ein einzelnes Tool, das die einfache Bereitstellung für Synchronisierung und Anmeldung bietet.

![AAD Connect](../media-draft/AADCONNECTxprs_960.jpg)

Lamna Healthcare erfordert die Authentifizierung primär gegen lokale Domänencontroller (DC) und eine Cloudauthentifizierung in einem Notfallwiederherstellungsszenario. Es gibt keine Anforderungen, die nicht von Azure AD unterstützt werden.

Lamna Healthcare hat sich entschieden, mit der folgenden Konfiguration fortzufahren:

- Verwenden von Azure AD Connect, um Gruppen, Benutzerkonten und Kennworthashes aus dem lokalen Active Directory-Verzeichnis mit Azure AD zu synchronisieren.
  - Dies kann der Sicherung dienen, wenn die Passthrough-Authentifizierung nicht verfügbar ist.
- Konfigurieren der Passthrough-Authentifizierung mit einem lokalen Authentifizierungs-Agent (auf einem lokalen Windows Server).
- Einmaliges Anmelden mit der nahtlos integrierten Azure AD-Funktion, um Benutzer von lokalen PCs, die in Domänen eingebunden sind, automatisch anzumelden.
  - Reibungslose Benutzeranmeldung durch Unterdrückung mehrerer Authentifizierungsanforderungen.

## <a name="authentication--access"></a>Authentifizierung und Zugriff

Die Sicherheitsrichtlinie von Lamna Healthcare verlangt, dass alle Anmeldungen, die außerhalb des Umkreisnetzwerks des Unternehmens erfolgen, mit einer zusätzlichen Authentifizierungsstufe authentifiziert werden. Diese Anforderung vereint zwei Aspekte des Azure AD-Dienstes: Multi-Factor Authentication und Richtlinien für bedingten Zugriff.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication

Multi-Factor Authentication (MFA) bietet zusätzliche Sicherheit für Identitäten, indem mindestens zwei Methoden für eine vollständige Authentifizierung benötigt werden. Diese Methoden umfassen drei Kategorien:

- *Authentifizierung mit einem Kennwort*
- *Authentifizierung mit einem Gerät*
- *Authentifizierung mit persönlichen Merkmalen*

Für die **Authentifizierung mit einem Kennwort** können Sie ein Kennwort oder die Antwort auf eine Sicherheitsfrage verwenden. Für die **Authentifizierung mit einem Gerät** können Sie eine mobile App verwenden, die eine Benachrichtigung empfängt, oder ein Gerät, das Token generiert. Die **Authentifizierung mit persönlichen Merkmalen** erfolgt in der Regel anhand biometrischer Eigenschaften, z.B. über einen Fingerabdruck oder einen Gesichtsscan auf vielen mobilen Geräten.

Die mehrstufige Authentifizierung erhöht die Sicherheit Ihrer Identität, indem sie die Auswirkungen der Offenlegung von Anmeldeinformationen einschränkt. Ein Angreifer, der das Kennwort eines Benutzers hat, benötigt ebenfalls sein Telefon oder einen Scan von seinem Gesicht, um sich vollständig zu authentifizieren. Die Authentifizierung mit einer einzigen Methode ist nicht möglich, und der Angreifer kann diese Anmeldeinformationen nicht zum Authentifizieren verwenden. Die Sicherheitsvorteile sind enorm, sodass die Verwendung von MFA sofern möglich dringend empfohlen wird.

Azure AD verfügt über integrierte MFA-Funktionen und lässt sich in andere Drittanbieter-MFA integrieren. Die Verwendung steht jedem Benutzer mit der Rolle „Globaler Administrator“ in Azure AD kostenlos zur Verfügung, da es sich um sehr sensible Konten handelt. Für alle anderen Konten können Sie MFA aktivieren, indem Sie spezielle Lizenzen erwerben und diese dem Konto zuweisen.

### <a name="conditional-access-policies"></a>Richtlinien für bedingten Zugriff

Sie können eine weitere Schutzebene hinzufügen, indem Sie neben der mehrstufigen Authentifizierung Richtlinien für bedingten Zugriff verwenden, die sicherstellen, dass zusätzliche Anforderungen erfüllt werden, bevor der Zugriff gewährt wird. Wenn Sie Anmeldungen von einer verdächtigen IP-Adresse blockieren oder den Zugriff von Geräten ohne Malwareschutz verweigern, kann der Zugriff von riskanten Anmeldungen eingeschränkt werden.

Azure Active Directory bietet eine Funktion für Richtlinien für den bedingten Zugriff, die die Unterstützung von Zugriffsrichtlinien basierend auf Gruppen, Standort oder Gerätestatus umfasst. Die Standortfunktion ermöglicht Lamna, IP-Adressen zu erkennen, die nicht zu Ihrem Netzwerk gehören, und erfüllt die Sicherheitsanforderung der mehrstufigen Authentifizierung für alle entsprechenden Standorte.

Lamna Healthcare hat eine [Richtlinie für bedingten Zugriff](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/overview) erstellt, die erfordert, dass Benutzer, die von einer IP-Adresse außerhalb des Unternehmensnetzwerks auf die Anwendung zugreifen, MFA verwenden müssen.

![Bedingter Zugriff](../media-draft/conditional-access.png)

## <a name="securing-legacy-applications"></a>Sichern von älteren Anwendungen

Lamna Healthcare-Mitarbeiter benötigen einen sicheren Remotezugriff auf ihre Verwaltungsanwendung, die lokal gehostet wird. Benutzer authentifizieren sich in der Anwendung derzeit über die integrierte Windows-Authentifizierung (IWA) von ihren in die Domäne eingebundenen Computern hinter der Unternehmensfirewall. Auch wenn ein Projekt zur Integration moderner Authentifizierungsmechanismen in die Anwendung geplant ist, sollen Remotezugriffsfunktionen so schnell wie möglich bereitgestellt werden. Der Azure Anwendungsproxy kann schnell, einfach und sicher den Remotezugriff auf die Anwendung ohne Codeänderungen ermöglichen.

Der Azure AD-Anwendungsproxy ist:

- Einfach
  - Sie müssen Ihre Anwendungen weder ändern noch aktualisieren, damit Sie mit dem Anwendungsproxy funktionieren.
  - Ihre Benutzer verwenden einen einheitlichen Authentifizierungsvorgang. Sie können über das MyApps-Portal das einmalige Anmelden für SaaS-Apps in der Cloud und Ihre lokalen Apps erhalten.
- Sicher
  - Wenn Sie Ihre Apps mit dem Azure AD-Anwendungsproxy veröffentlichen, können Sie die umfassenden Autorisierungssteuerungen und Sicherheitsanalysen in Azure nutzen. Sie erhalten Sicherheit auf Cloudebene und Azure-Sicherheitsfunktionen wie den bedingten Zugriff und die zweistufige Überprüfung.
  - Sie müssen keine eingehenden Verbindungen über Ihre Firewall öffnen, um Benutzern Remotezugriff zu gewähren.
- Kosteneffizient
  - Der Anwendungsproxy funktioniert in der Cloud, sodass Sie Zeit und Geld sparen können. Für lokale Lösungen müssen Sie in der Regel DMZs, Edgeserver oder andere komplexe Infrastrukturen einrichten und verwalten.

Der Azure AD-Anwendungsproxy besteht aus zwei Komponenten: Einem Connector-Agent, der sich auf einem Windows-Server in Ihrem Unternehmensnetzwerk befindet, und einem externen Endpunkt – dem MyApps-Portal oder einer externen URL. Wenn ein Benutzer zum Endpunkt navigiert, authentifiziert er sich bei Azure AD und wird über den Connector-Agent an die lokale Anwendung weitergeleitet.

## <a name="working-with-consumer-identities"></a>Verwenden von Endbenutzeridentitäten

Seit der Integration der modernen Authentifizierung in bestehende Anwendungen hat Lamna Healthcare schnell erkannt, welche Vorteile ein verwaltetes Identitätssystem wie Azure AD Unternehmen bringen kann. Das Führungsteam ist nun daran interessiert, andere Möglichkeiten zu erkunden, wie die Identitätsdienste von Microsoft den Geschäftswert steigern können. Sie haben nun ihre Aufmerksamkeit auf externe Kunden gerichtet und darauf, wie die Modernisierung bestehender Kundeninteraktionen eine enge Integration in externe Identitätsanbieter wie Google, Facebook und LinkedIn ermöglichen könnte.

Azure AD B2C ist ein Identitätsverwaltungsdienst, der auf den soliden Grundlagen von Azure Active Directory basiert, mit dem Sie die Kundenregistrierung und -anmeldung anpassen und steuern sowie Profile bei der Verwendung Ihrer Anwendungen verwalten können. Dazu gehören u.a. für iOS, Android und .NET entwickelte Anwendungen. Azure AD B2C bietet eine Identitätsanmeldung für soziale Netzwerke und schützt gleichzeitig Ihre Kundenidentitäts-Profilinformationen. Azure AD B2C-Verzeichnisse unterscheiden sich von Standard-Azure AD-Verzeichnissen und können im Azure-Portal erstellt werden.

## <a name="identity-management-at-lamna-healthcare"></a>Identitätsverwaltung mit Lamna Healthcare

Sie haben erfahren, wie Lamna Healthcare Identitätsverwaltungslösungen in Azure einsetzt, um die Umgebungssicherheit zu verbessern. Es wurde damit begonnen, Benutzern das einmalige Anmelden anzubieten, damit sie mit weniger Konten zu tun haben. Dies reduziert die Komplexität aufgrund zu vieler Konten. MFA wird für den Zugriff auf Anwendungen erzwungen und eine ältere Anwendung wurde aktualisiert, um moderne Authentifizierung mit minimalem Aufwand zu nutzen. Außerdem haben Sie erfahren, wie Lamna Healthcare die Arbeit mit Endbenutzeridentitäten und die Benutzerfreundlichkeit von Anwendungen für Patienten verbessern kann.

## <a name="summary"></a>Zusammenfassung

In dieser Lektion haben Sie gelernt, wie mehrere Azure Active Directory-Funktionen kombiniert werden können, um eine solide Identitätslösung für den sicheren Zugriff auf Anwendungen unabhängig vom Standort zu bieten. Identität ist eine wichtige Sicherheitsebene. Wenn sie gut konzipiert und in Ihre Architektur integriert ist, profitieren Sie von einer sicheren Umgebung.