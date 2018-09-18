Früher wurden Unternehmensdaten in erster Linie durch Netzwerkgrenzen und die dazugehörigen Firewalls und physischen Zugriffssteuerungen geschützt. Aufgrund der explosionsartig zunehmenden Verbreitung von BYOD (Bring Your Own Device), mobilen Apps und Cloudanwendungen werden Netzwerkgrenzen jedoch immer durchlässiger. 

Die neue primäre Sicherheitsgrenze heißt deshalb „Identität“. Ordnungsgemäße Authentifizierung und eine sorgfältige Zuweisung von Berechtigungen sind unverzichtbar, um die Kontrolle über die eigenen Daten nicht zu verlieren.

Contoso nimmt sich dieser Probleme umgehend an. Die neue Hybrid Cloud-Lösung des Unternehmens muss für mobile Apps konzipiert sein, die Zugriff auf vertrauliche Daten haben, wenn ein autorisierter Benutzer angemeldet ist. Darüber hinaus verfügt das Unternehmen über Lieferfahrzeuge, die kontinuierlich einen Datenstrom mit Telemetriedaten senden, die dringend zur Optimierung des Geschäfts benötigt werden.

## <a name="single-sign-on"></a>Einmaliges Anmelden

Je mehr Identitäten ein Benutzer verwalten muss, desto größer ist das Risiko eines Sicherheitsincidents in Zusammenhang mit Anmeldeinformationen. Mehrere Identitäten implizieren mehrere Kennwörter, die verwaltet und geändert werden müssen. Kennwortrichtlinien können zwischen den Anwendungen variieren, und da die erforderliche Kennwortkomplexität zunimmt, wird es für Benutzer immer schwieriger, sich an diese zu erinnern.

Außerdem ist die Verwaltung all dieser Identitäten erforderlich. Helpdesks werden beim Bearbeiten von Kontosperrungen und Kennwortzurücksetzungen zusätzlich belastet. Wenn ein Benutzer ein Unternehmen verlässt, kann es zudem schwierig sein, alle seine Identitäten zu finden und zu deaktivieren. Falls eine Identität übersehen wird, könnte der Benutzer weiterhin unerwünschten Zugriff erhalten.

Einmaliges Anmelden erfordert nur eine Identität und nur ein Kennwort. Der anwendungsübergreifende Zugriff wird einer einzigen, benutzerspezifischen Identität gewährt, wodurch das Sicherheitsmodell vereinfacht wird. Wenn Benutzer die Rolle wechseln oder ein Unternehmen verlassen, sind Zugriffsänderungen an die einzelne Identität gebunden. So wird der Aufwand für das Ändern oder Deaktivieren von Konten erheblich reduziert. Das einmalige Anmelden für Konten erleichtert Benutzern die Verwaltung ihrer Identitäten und erhöht die Sicherheitsfunktionen in Ihrer Umgebung.

### <a name="sso-with-azure-active-directory"></a>Einmaliges Anmelden mit Azure Active Directory

Azure Active Directory (AAD) ist ein cloudbasierter Identitätsdienst. Er hat eine integrierte Unterstützung für die Synchronisierung mit Ihrem vorhandenen lokalen Active Directory-Verzeichnis oder kann einzeln verwendet werden.

Das bedeutet, dass alle Ihre Anwendungen – ob lokal, in der Cloud (einschließlich Office 365) oder mobil – dieselben Anmeldeinformationen verwenden können. 

Administratoren und Entwickler können den Zugriff auf Daten und Anwendungen mithilfe zentralisierter Regeln und Richtlinien steuern, die in Azure AD konfiguriert sind.

Darüber hinaus ist Microsoft in der einzigartigen Position, mehrere Datenquellen zu einem Intelligent Security Graph zu kombinieren, der Bedrohungsanalysen und Echtzeit-Identitätsschutz für alle Konten in Azure Active Directory bietet. Dies gilt auch für Konten, die von Ihrem lokalen AD synchronisiert werden.

Contoso integriert das bereits vorhandene Active Directory des Unternehmens in Azure AD, um innerhalb der Organisation eine einheitliche Zugriffssteuerung zu implementieren. Außerdem können Benutzer so ganz einfach auf Ihre E-Mails und Office 365-Dokumente zugreifen, ohne sich erneut authentifizieren zu müssen.

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication

Multi-Factor Authentication (MFA) bietet zusätzliche Sicherheit für Identitäten, indem mindestens zwei Methoden für eine vollständige Authentifizierung benötigt werden. Diese Methoden umfassen drei Kategorien:

- *Authentifizierung mit einem Kennwort*
- *Authentifizierung mit einem Gerät*
- *Authentifizierung mit persönlichen Merkmalen*

Für die **Authentifizierung mit einem Kennwort** können Sie ein Kennwort oder die Antwort auf eine Sicherheitsfrage verwenden. Für die **Authentifizierung mit einem Gerät** können Sie eine mobile App verwenden, die eine Benachrichtigung empfängt, oder ein Gerät, das Token generiert. Die **Authentifizierung mit persönlichen Merkmalen** erfolgt in der Regel anhand biometrischer Eigenschaften, z.B. über einen Fingerabdruck oder einen Gesichtsscan auf vielen mobilen Geräten.

Die mehrstufige Authentifizierung erhöht die Sicherheit Ihrer Identität, indem sie die Auswirkungen der Offenlegung von Anmeldeinformationen einschränkt. Ein Angreifer, der das Kennwort eines Benutzers hat, benötigt ebenfalls sein Telefon oder einen Scan von seinem Gesicht, um sich vollständig zu authentifizieren. Die Authentifizierung mit einer einzigen Methode ist nicht möglich, und der Angreifer kann diese Anmeldeinformationen nicht zum Authentifizieren verwenden. Die Sicherheitsvorteile sind enorm, sodass die Verwendung von MFA sofern möglich dringend empfohlen wird.

Azure AD verfügt über integrierte MFA-Funktionen und lässt sich in andere Drittanbieter-MFA integrieren. Die Verwendung steht jedem Benutzer mit der Rolle „Globaler Administrator“ in Azure AD kostenlos zur Verfügung, da es sich um sehr sensible Konten handelt. Für alle anderen Konten können Sie MFA aktivieren, indem Sie spezielle Lizenzen erwerben und diese dem Konto zuweisen.

Für Contoso Shipping soll MFA immer dann aktiviert werden, wenn sich ein Benutzer über einen Computer anmeldet, der nicht mit der Domäne verbunden ist. Dazu gehören auch die mobilen Apps.

## <a name="providing-identities-to-services"></a>Bereitstellen von Identitäten für Dienste

Für Dienste ist es oft nützlich, eine Identität zu besitzen. Anmeldeinformationen sind entgegen allen bewährten Methoden häufig in Konfigurationsdateien enthalten. Wenn für diese Konfigurationsdateien keine Sicherheitsrichtlinien gelten, kann jeder Benutzer mit Zugriff auf die Systeme oder Repositorys auf diese Anmeldeinformationen zugreifen und stellt somit ein potenzielles Risiko dar.

Bei Azure AD wurde dieses Problem auf zwei Arten gelöst: mit Dienstprinzipalen und verwalteten Dienstidentitäten.

### <a name="service-principals"></a>Dienstprinzipale

Zum Verständnis des Konzepts von Dienstprinzipalen müssen zunächst die Begriffe **Identität** und **Prinzipal** erläutert werden, da diese in der Welt der Identitätsverwaltung verwendet werden.

Eine **Identität** ist lediglich etwas, das authentifiziert werden kann. Hierzu gehören natürlich Benutzer mit Benutzername und Kennwort, aber auch Anwendungen und andere Server, die möglicherweise mit geheimen Schlüsseln oder Zertifikaten authentifiziert werden. Zusätzliche Definition: Bei einem **Konto** handelt es sich um Daten, die einer Identität zugeordnet sind.

Ein **Prinzipal** ist eine Identität mit bestimmten Rollen oder Ansprüchen. Häufig ist es nicht sinnvoll, sich Identität und Prinzipal getrennt vorzustellen. Aber denken Sie an die Verwendung von „sudo“ an einer Bash-Eingabeaufforderung oder an „Als Administrator ausführen“ unter Windows. In beiden Fällen bleiben Sie mit derselben Identität wie bisher angemeldet, nehmen jedoch eine andere Rolle an, unter der Sie Befehle ausführen. Gruppen werden häufig auch als Prinzipale betrachtet, da ihnen Rechte zugewiesen werden können.

Ein **Dienstprinzipal** trägt somit seinen Namen zurecht. Er stellt eine Identität dar, die von einem Dienst oder einer Anwendung verwendet wird. Genau wie anderen Identitäten können auch ihm verschiedene Rollen zugewiesen werden. 

### <a name="managed-service-identities"></a>Verwaltete Dienstidentitäten

Die Erstellung von Dienstprinzipalen kann sehr aufwendig sein, und es gibt jede Menge Berührungspunkte, die die Verwaltung erschweren. Verwaltete Dienstidentitäten (Manage Service Identities, MSI) sind viel einfacher und nehmen Ihnen einen Großteil der Arbeit ab. 

Eine MSI kann sofort für jeden Azure-Dienst erstellt werden, der diese Funktionalität unterstützt. Diese Möglichkeit wird von immer mehr Diensten bereitgestellt. Wenn Sie eine MSI für einen Dienst erstellen, erstellen Sie ein Konto für den Azure Active Directory-Mandanten. Die Azure-Infrastruktur übernimmt automatisch die Authentifizierung des Diensts und die Verwaltung des Kontos. Danach können Sie dieses Konto wie jedes andere AD-Konto verwenden und beispielsweise dafür sorgen, dass der authentifizierte Dienst sicher auf andere Azure-Ressourcen zugreift.

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

Rollen sind bestimmte Berechtigungen (etwa „Schreibgeschützt“ oder „Mitwirkender“), die Benutzern für den Zugriff auf eine Azure-Dienstinstanz zugewiesen werden können. 

Identitäten werden Rollen direkt oder über eine Gruppenmitgliedschaft zugeordnet. Die Trennung von Sicherheitsprinzipalen, Zugriffsberechtigungen und Ressourcen ermöglicht eine einfache Verwaltung und eine differenzierte Steuerung. Administratoren können sicherstellen, dass nur die erforderlichen Mindestberechtigungen gewährt werden.

Rollen können auf der jeweiligen Dienstinstanzebene zugewiesen werden, werden jedoch auch in der Azure Resource Manager-Hierarchie nach unten weitergegeben. Rollen, die auf einer höheren Ebene zugewiesen werden (etwa auf Abonnementebene), werden an untergeordnete Ebenen (etwa Dienstinstanzen) vererbt. 

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Verwaltungsgruppen](../media-draft/3-role-assignment-scope.png)

### <a name="privileged-identity-management"></a>Privileged Identity Management

Bei einem umfassenden Konzept zum Schutz der Infrastruktur sollte neben der Verwaltung des Zugriffs auf Azure-Ressourcen mittels RBAC mit Änderung und Weiterentwicklung der Organisation die Einbindung einer laufenden Überwachung von Rollenmitgliedern in Betracht gezogen werden. Azure AD Privileged Identity Management (PIM) ist ein zusätzliches kostenpflichtiges Angebot, das einen Überblick über Rollenzuweisungen, die Aktivierung von Self-Service- und Just-In-Time-Rollen sowie die Überprüfung des Zugriffs auf Azure AD- und Azure-Ressourcen bietet.

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Privileged Identity Management](../media-COPIED-FROM-DESIGNFORSECURITY/PIM_Dashboard.PNG)

Identitäten ermöglichen die Implementierung eines Sicherheitsbereichs, der über unsere physische Kontrolle hinausgeht. Mit SSO und einer entsprechenden Konfiguration der rollenbasierten Zugriffssteuerung wissen wir immer genau, wer auf unsere Daten und Infrastruktur zugreifen kann.