Netzwerkperimeter und ihren Firewalls und physischen zugriffssteuerungen verwendet werden, um den primären Schutz für Unternehmensdaten werden. Aber Netzwerkperimeter sind mit der explosiven Entwicklung immer durchlässiger geworden, bringen Sie Ihr eigenes Gerät (BYOD), mobile apps und cloud-Anwendungen. 

Identität ist die neue primäre Sicherheits-Grenze geworden. Ordnungsgemäßer Authentifizierung und die Zuweisung von Berechtigungen ist entscheidend für die Kontrolle über Ihre Daten.

Versand von Contoso ist diese Probleme sofort, adressiert. Die neuen Hybrid Cloud-Lösung muss für mobile apps-Konto, die Zugriff auf vertrauliche Daten verfügen, wenn ein autorisierter Benutzer angemeldet ist. Sie haben außerdem den Versand von Fahrzeugen, senden einen Konstanten Stream von Telemetriedaten, die zur Optimierung ihres Unternehmens von entscheidender Bedeutung ist.

## <a name="single-sign-on"></a>Einmaliges Anmelden

Je mehr Identitäten ein Benutzer verwalten muss, desto größer ist das Risiko eines Sicherheitsincidents in Zusammenhang mit Anmeldeinformationen. Mehrere Identitäten implizieren mehrere Kennwörter, die verwaltet und geändert werden müssen. Richtlinien für Kennwörter können variieren zwischen Anwendungen und Anforderungen an die Komplexität zu erhöhen, erleichtert es schwieriger zu merken sie.

Außerdem ist die Verwaltung all dieser Identitäten erforderlich. Helpdesks werden beim Bearbeiten von Kontosperrungen und Kennwortzurücksetzungen zusätzlich belastet. Wenn ein Benutzer ein Unternehmen verlässt, kann es zudem schwierig sein, alle seine Identitäten zu finden und zu deaktivieren. Falls eine Identität übersehen wird, könnte der Benutzer weiterhin unerwünschten Zugriff erhalten.

Mit single Sign-on (SSO) müssen Benutzer nur eine ID und ein Kennwort merken. Der anwendungsübergreifende Zugriff wird einer einzigen, benutzerspezifischen Identität gewährt, wodurch das Sicherheitsmodell vereinfacht wird. Wenn Benutzer die Rolle wechseln oder ein Unternehmen verlassen, sind Zugriffsänderungen an die einzelne Identität gebunden. So wird der Aufwand für das Ändern oder Deaktivieren von Konten erheblich reduziert. Mithilfe von einmaliges Anmelden für Konten für Benutzer zur Verwaltung ihrer Identitäten erleichtert, und erhöhen die Sicherheitsfunktionen in Ihrer Umgebung.

### <a name="sso-with-azure-active-directory"></a>Einmaliges Anmelden mit Azure Active Directory

Azure Active Directory (Azure AD) ist ein cloudbasierter Identitätsdienst. Es bietet eine integrierte Unterstützung für die Synchronisierung mit Ihrem vorhandenen lokalen Active Directory-Instanz, oder kann verwendet werden eigenständige.

Das bedeutet, dass alle Ihre Anwendungen – ob lokal, in der Cloud (einschließlich Office 365) oder mobil – dieselben Anmeldeinformationen verwenden können. 

Administratoren und Entwickler können den Zugriff auf Daten und Anwendungen mithilfe zentralisierter Regeln und Richtlinien steuern, die in Azure AD konfiguriert sind.

Darüber hinaus ist Microsoft hervorragend geeignet, um mehrere Datenquellen zu einem intelligent Security Graph zu kombinieren, die bereitstellen zu können, Bedrohungsanalyse und in Echtzeit Identity Protection an alle Konten in Azure Active Directory (auch Konten, die synchronisiert werden aus Ihrer lokalen Active Directory-Instanz).

Versand von Contoso wird ihre vorhandene Active Directory-Instanz in Azure AD integrieren. Steuern des Zugriffs wird in der gesamten Organisation konsistent gemacht. Es wird auch ein Kinderspiel, damit Benutzer in die e-Mail- und Office 365-Dokumente zu erhalten, ohne sich erneut authentifizieren, erleichtern.

## <a name="multi-factor-authentication"></a>Mehrstufige Authentifizierung

Die mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) bietet zusätzliche Sicherheit für Ihre Identität, weil mindestens zwei Methoden für eine vollständige Authentifizierung benötigt werden. Diese Methoden umfassen drei Kategorien:

- *Authentifizierung mit einem Kennwort*
- *Authentifizierung mit einem Gerät*
- *Authentifizierung mit persönlichen Merkmalen*

**Etwas, das Sie kennen** wäre, ein Kennwort oder die Antwort auf eine Sicherheitsfrage. **Etwas Sie besitzen** ist möglicherweise eine mobile app, die eine Benachrichtigung oder ein Token generiert Gerät empfängt. **Etwas Sie** ist in der Regel eine Art biometrische Eigenschaft, z. B. ein Fingerabdruck oder gesichtserkennung-Scan für viele mobile Geräte verwendet.

Verwendung von MFA erhöht die Sicherheit Ihrer Identität durch Beschränken der Auswirkungen einer Offenlegung von Anmeldeinformationen. Ein Angreifer, der das Kennwort eines Benutzers hat, benötigt ebenfalls sein Telefon oder einen Scan von seinem Gesicht, um sich vollständig zu authentifizieren. Authentifizierung mit nur einem Faktor überprüft reicht nicht aus, und der Angreifer würde in der Lage, diese Anmeldeinformationen zum Authentifizieren verwenden. Die Sicherheitsvorteile sind enorm, sodass die Verwendung von MFA sofern möglich dringend empfohlen wird.

Azure AD verfügt über MFA-Funktionen integriert und wird in andere Drittanbieter-MFA-Anbieter integriert. Er wird bereitgestellt, jeder Benutzer mit der globalen Administratorrolle in Azure AD, da diese hoch sensible Konten sind kostenlos. Für alle anderen Konten können Sie MFA aktivieren, indem Sie spezielle Lizenzen erwerben und diese dem Konto zuweisen.

Um den Rückversand für Contoso entscheiden Sie zum Aktivieren der MFA jedes Mal ein Benutzer von einem nicht-Domäne verbundene Computer anmeldet. Dazu gehören mobile apps.

## <a name="providing-identities-to-services"></a>Bereitstellen von Identitäten für Dienste

Für Dienste ist es oft nützlich, eine Identität zu besitzen. Häufig und mit bewährten Methoden werden Anmeldeinformationen in Konfigurationsdateien eingebettet. Wenn für diese Konfigurationsdateien keine Sicherheitsrichtlinien gelten, kann jeder Benutzer mit Zugriff auf die Systeme oder Repositorys auf diese Anmeldeinformationen zugreifen und stellt somit ein potenzielles Risiko dar.

Bei Azure AD wurde dieses Problem auf zwei Arten gelöst: mit Dienstprinzipalen und verwalteten Dienstidentitäten.

### <a name="service-principals"></a>Dienstprinzipale

Um die Dienstprinzipale zu verstehen, ist es sinnvoll, Sie zuerst verstehen, die Wörter **Identität** und **principal**, da sie in der Welt der Identity-Management verwendet werden.

Eine **Identität** ist lediglich etwas, das authentifiziert werden kann. Natürlich eingeschlossen sind Benutzer mit Benutzername und Kennwort, aber er kann auch enthalten, Anwendungen oder anderen Servern, die mit geheimen Schlüsseln oder Zertifikaten authentifiziert werden können. Hierzu eine zusätzliche Definition: Bei einem **Konto** handelt es sich um Daten, die einer Identität zugeordnet sind.

Ein **Prinzipal** ist eine Identität mit bestimmten Rollen oder Ansprüchen. Es ist häufig nicht sinnvoll, sollten .NET-Identitäts- und-Prinzipalklassen getrennt, aber stellen Sie sich mit `sudo` in einer Bash-Eingabeaufforderung oder auf Windows mithilfe von "Ausführen als Administrator." In beiden Fällen diese Sie weiterhin angemeldet sind als die gleiche Identität wie vor, aber Du hast geändert, dass die Rolle, die unter der Sie ausgeführt werden. Gruppen werden häufig auch als Prinzipale betrachtet, da diese Rechte zugewiesen haben, können.

Also eine **Dienstprinzipal** buchstäblich heißt. Er stellt eine Identität dar, die von einem Dienst oder einer Anwendung verwendet wird. Wie andere Identitäten können sie Rollen zugewiesen werden. 

### <a name="managed-service-identities"></a>Verwaltete Dienstidentitäten

Die Erstellung von dienstprinzipalen kann eine mühsame Angelegenheit, und es gibt viele Berührungspunkte, die Verwaltung schwierig machen können. Verwaltete Dienstidentitäten sind wesentlich einfacher und die meiste Arbeit für Sie erledigt werden. 

Eine verwaltete Dienstidentität kann sofort für alle Azure-Dienste erstellt werden, die es unterstützt (die Liste nimmt ständig zu). Wenn Sie eine verwaltete Dienstidentität für einen Dienst erstellen, erstellen Sie ein Konto für den Azure Active Directory-Mandanten. Die Azure-Infrastruktur übernimmt automatisch beim Authentifizieren des Diensts und das Konto verwaltet. Sie können dann dieses Konto wie alle anderen Azure AD-Konto, z.B. sicher des authentifizierten-Diensts den Zugriff auf andere Azure-Ressourcen verwenden.

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

Rollen sind bestimmte Berechtigungen, z. B. "Schreibgeschützt" oder "Mitwirkender", dass Benutzer den Zugriff auf ein Azure-Dienst-Instanz erteilt werden können. 

Identitäten werden Rollen direkt oder über eine Gruppenmitgliedschaft zugeordnet. Die Trennung von Sicherheitsprinzipalen, Berechtigungen und Ressourcen bietet, einfache zugriffsverwaltung und eine präzisere Kontrolle. Administratoren können sicherstellen, dass die erforderlichen Mindestberechtigungen gewährt werden.

Rollen können auf der jeweiligen Instanz Dienstebene erteilt werden, aber diese auch in der Azure Resource Manager-Hierarchie ausgetauscht. Rollen, die auf einer höheren Ebene zugewiesen werden, wie etwa ein ganzes Abonnement, werden an untergeordnete Ebenen, wie etwa Dienstinstanzen, vererbt. 

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Verwaltungsgruppen](../media-draft/3-role-assignment-scope.png)

### <a name="privileged-identity-management"></a>Privileged Identity Management

Zusätzlich zum Verwalten von Zugriff auf Azure-Ressourcen mit rollenbasierte Zugriffssteuerung (RBAC), ein umfassender Ansatz zum Schutz der Infrastruktur, einschließlich der laufenden Überwachung der Mitglieder der Rolle als ihre Organisation Änderungen sollten, und weiterentwickelt. Azure AD Privileged Identity Management (PIM) ist eine zusätzliche, kostenpflichtiges Angebot, die Aufsicht über rollenzuweisungen, Self-Service- und just-in-Time bereitstellt rollenaktivierung und Azure AD und Azure-Ressource zu zugriffsüberprüfungen.

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Privileged Identitätsmanagement](../media-COPIED-FROM-DESIGNFORSECURITY/PIM_Dashboard.png)

Identität kann wir einen Sicherheitsbereich zu betrachten, sogar außerhalb unserer physische Kontrolle zu behalten. Einmaliges Anmelden und Konfiguration der entsprechenden rollenbasierten Zugriff können wir immer sicher sein, wer hat die Möglichkeit, anzeigen und Ändern von unserer Daten und Infrastruktur.