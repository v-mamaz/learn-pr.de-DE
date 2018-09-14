Bei Lamna Healthcare ist vor Kurzem bei einer Kunden betreffenden Webanwendung ein erheblicher Ausfall aufgetreten. Einem Techniker wurde Vollzugriff auf eine Ressourcengruppe gewährt, die die Produktionswebanwendung enthält. Dieser hat versehentlich die Ressourcengruppe mit allen untergeordneten Ressourcen sowie die Datenbank gelöscht, in der aktive Kundendaten gehostet werden. 

Zum Glück waren Anwendungsquellcode und Ressourcen in der Quellcodeverwaltung verfügbar und die Datenbank wurde regelmäßig nach einem Zeitplan automatisch gesichert. Daher konnte der Dienst relativ einfach wiederhergestellt werden. Hier untersuchen wir nun, wie dieser Ausfall mithilfe der Funktionen in Azure zum Schutz des Zugriffs auf die Infrastruktur hätte vermieden werden können.

## <a name="criticality-of-infrastructure"></a>Bedeutung der Infrastruktur

Die Cloudinfrastruktur ist inzwischen ein wichtiger Bestandteil vieler Unternehmen. Dabei muss darauf geachtet werden, dass Benutzer und Prozesse nur die Rechte erhalten, die sie benötigen, um ihre Arbeit zu erledigen. Zuweisen von falsch kann keine Daten verloren gehen, Datenlecks oder dazu führen, dass Dienste nicht mehr verfügbar ist. 

Systemadministratoren können für eine große Anzahl von Benutzern, Systeme zuständig und Berechtigungssätze. Daher kann die ordnungsgemäße Zuweisung von Zugriffsberechtigungen schnell unüberschaubar werden und eine Universallösung zur Folge haben. Damit wird die Verwaltung zwar unkomplizierter, es ist jedoch wesentlich einfacher, versehentlich einen freizügigeren Zugriff als erforderlich zu gewähren.

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

Hier bietet die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) ein etwas anderes Konzept. Rollen werden als Sammlungen von Zugriffsberechtigungen definiert. Sicherheitsprinzipale werden Rollen direkt oder über eine Gruppenmitgliedschaft zugeordnet. Die Trennung von Sicherheitsprinzipalen, Zugriffsberechtigungen und Ressourcen ermöglicht eine einfachere Verwaltung und differenziertere Steuerung.

In Azure werden Benutzer, Gruppen und Rollen in Azure Active Directory (Azure AD) gespeichert. Bei der Azure Resource Manager-API wird die rollenbasierte Zugriffssteuerung verwendet, um die Verwaltung des Zugriffs auf alle Ressourcen innerhalb von Azure zu gewährleisten.

![ACL-basierter Zugriff](../media-draft/ACL_Based_Access.png)

<!-- ![Role-based access control](../media-draft/Role_Based_Access.png)
 -->

### <a name="roles-and-management-groups"></a>Rollen und -Verwaltungsgruppen

Rollen sind bestimmte Berechtigungen, z. B. "Schreibgeschützt" oder "Mitwirkender", dass Benutzer den Zugriff auf ein Azure-Dienst-Instanz erteilt werden können. Rollen können auf der jeweiligen Instanz Dienstebene erteilt werden, aber diese auch in der Azure Resource Manager-Hierarchie ausgetauscht. Rollen, die auf einer höheren Ebene zugewiesen werden, wie etwa ein ganzes Abonnement, werden an untergeordnete Ebenen, wie etwa Dienstinstanzen, vererbt. 

Bei Verwaltungsgruppen handelt es sich um eine zusätzliche hierarchische Ebene, die vor Kurzem beim RBAC-Modell eingeführt wurde. Verwaltungsgruppen bieten die zusätzliche Möglichkeit, Abonnements zu gruppieren und Richtlinien auf einer noch höheren Ebene anzuwenden.

Dank der Möglichkeit der Weitergabe von Rollen in einer beliebig definierten Abonnementhierarchie können Administratoren authentifizierten Benutzern auch vorübergehenden Zugriff auf eine ganze Umgebung gewähren. Dies ist beispielsweise möglich, wenn ein Prüfer temporären schreibgeschützten Zugriff auf alle Abonnements benötigt.

![Verwaltungsgruppen](../media-draft/management_groups.png)

### <a name="privileged-identity-management"></a>Privileged Identity Management

Bei einem umfassenden Konzept zum Schutz der Infrastruktur sollte neben der Verwaltung des Zugriffs auf Azure-Ressourcen mittels RBAC mit Änderung und Weiterentwicklung der Organisation die Einbindung einer laufenden Überwachung von Rollenmitgliedern in Betracht gezogen werden. Azure AD Privileged Identity Management (PIM) ist ein zusätzliches kostenpflichtiges Angebot, das einen Überblick über Rollenzuweisungen, die Aktivierung von Self-Service- und Just-In-Time-Rollen sowie die Überprüfung des Zugriffs auf Azure AD- und Azure-Ressourcen bereitstellt.

![Privileged Identity Management](../media-draft/PIM_Dashboard.png)

## <a name="providing-identities-to-services"></a>Bereitstellen von Identitäten für Dienste

Für Dienste ist es oft nützlich, eine Identität zu besitzen. Anmeldeinformationen sind entgegen allen bewährten Methoden häufig in Konfigurationsdateien enthalten. Wenn für diese Konfigurationsdateien keine Sicherheitsrichtlinien gelten, kann jeder Benutzer mit Zugriff auf die Systeme oder Repositorys auf diese Anmeldeinformationen zugreifen und stellt somit ein potenzielles Risiko dar.

Azure AD löst dieses Problem durch zwei Methoden:-Prinzipale und verwalteten Identitäten für Azure-Dienste.

### <a name="service-principals"></a>Dienstprinzipale

Um Dienstprinzipale zu verstehen, ist es sinnvoll, Sie zuerst verstehen, die Wörter **Identität** und **principal** Identity Management-Welt verwendet wird.

Eine **Identität** ist lediglich etwas, das authentifiziert werden kann. Offensichtlich eingeschlossen sind Benutzer mit Benutzername und Kennwort, aber er kann auch enthalten, Anwendungen oder anderen Servern, die mit geheimen Schlüsseln oder Zertifikaten authentifiziert werden können. Hierzu eine zusätzliche Definition: Bei einem **Konto** handelt es sich um Daten, die einer Identität zugeordnet sind.

Ein **Prinzipal** ist eine Identität mit bestimmten Rollen oder Ansprüchen. Häufig ist es nicht sinnvoll, sich Identität und Prinzipal getrennt vorzustellen, sondern zu überlegen, „sudo“ über eine Bash-Eingabeaufforderung oder „Als Administrator ausführen“ unter Windows zu verwenden. In beiden Fällen Sie immer noch angemeldet sind als die gleiche Identität wie vor, aber Sie haben die Rolle, die unter der Sie ausgeführt werden geändert.

Ein **Dienstprinzipal** trägt somit seinen Namen zurecht. Er stellt eine Identität dar, die von einem Dienst oder einer Anwendung verwendet wird. Wie andere Identitäten können sie Rollen zugewiesen werden. 

Bei Lamna Healthcare können beispielsweise die eigenen Bereitstellungsskripts zugewiesen werden, sodass sie authentifiziert als Dienstprinzipal ausgeführt werden. Wenn dies die einzige Identität ist mit der Berechtigung zur Ausführung schädlicher Aktionen, wird Lamna aktiv sind einen wichtiger Beitrag, um sicherzustellen, dass sie nicht über eine Wiederholung des Löschvorgangs versehentlich Ressourcen verfügen.

### <a name="managed-identities-for-azure-resources"></a>Verwaltete Identitäten für Azure-Ressourcen

Die Erstellung von dienstprinzipalen kann eine mühsame Angelegenheit, und es gibt viele Berührungspunkte, die Verwaltung schwierig machen können. Verwalten von Identitäten für Azure-Ressourcen sehr viel einfacher sind, und die meiste Arbeit für Sie erledigt werden.

Eine verwaltete Identität kann sofort für alle Azure-Dienste erstellt werden, die es unterstützt (die Liste nimmt ständig zu). Wenn Sie eine verwaltete Identität für einen Dienst erstellen, erstellen Sie ein Konto in Azure AD-Mandanten. Die Azure-Infrastruktur übernimmt automatisch die Authentifizierung des Diensts und die Verwaltung des Kontos. Danach können Sie dieses Konto wie jedes andere AD-Konto verwenden und beispielsweise dafür sorgen, dass der authentifizierte Dienst sicher auf andere Azure-Ressourcen zugreift.

Lamna Healthcare geht ihre identitätsverwaltung einen Schritt weiter und verwaltete Identitäten verwendet, für alle unterstützten Dienste, die die Fähigkeit zum Ausführen der infrastrukturverwaltung und Bereitstellungen zu benötigen.

## <a name="infrastructure-protection-at-lamna-healthcare"></a>Infrastrukturschutz bei Lamna Healthcare

Wir haben gesehen,wie bei Lamna Healthcare die Probleme ab dem Vorfall angegangen wurden, bei dem versehentlich Infrastruktur gelöscht wurde. Sie rollenbasierte Zugriffssteuerung verwendet haben, um die Sicherheit ihrer Infrastruktur besser zu verwalten und zu ihren Anmeldeinformationen aus Code und einfache Verwaltung der Identitäten für ihre Dienste erforderlichen verwaltete Identitäten verwenden.

## <a name="summary"></a>Zusammenfassung

Um die Verfügbarkeit und Integrität der Infrastruktur sicherzustellen, muss die Infrastruktur entsprechend geschützt werden. Ordnungsgemäß mithilfe von Funktionen wie RBAC und die verwaltete Identitäten hilft beim Schutz Ihrer Azure-Umgebung vor nicht autorisierten oder unerwünschten Zugriff, und verbessern Sie die Identity-Sicherheitsfunktionen in Ihrer Architektur.