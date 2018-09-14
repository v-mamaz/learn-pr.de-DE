Mit einem kostenlosen Azure-Konto können Sie Unternehmensanwendungen erstellen, testen und bereitstellen, benutzerdefinierte Web- und mobile Umgebungen erstellen und über Machine Learning und leistungsstarke Analysen Einsichten aus Ihren Daten gewinnen.

## <a name="what-is-an-azure-account"></a>Was ist ein Azure-Konto?

Ein _Azure-Konto_ ist an eine bestimmte Identität gebunden und enthält z.B. folgende Informationen:

- Name, E-Mail und bevorzugte Optionen für die Kontaktaufnahme
- Abrechnungsinformationen wie z.B. Kreditkartendaten

Ein Azure-Konto ist einem oder mehreren _Abonnements_ zugeordnet.

## <a name="what-is-an-azure-subscription"></a>Was ist ein Azure-Abonnement?

Ein _Azure-Abonnement_ ist ein logischer Container, der zum Bereitstellen von Ressourcen in Microsoft Azure verwendet wird. Er enthält Details zu all Ihren Ressourcen wie z.B. zu Ihren virtuellen Computern, Datenbanken usw. Er hat außerdem eine Vertrauensstellung mit einem einzelnen Azure AD-_Mandanten_, der für die Authentifizierung von Benutzern und Rollen verwendet wird, die im Abonnement enthalten sind.

Die Abrechnung erfolgt auf Abonnementebene. Sie können Ausgabenlimits für jedes Abonnement festlegen, damit Sie am Ende des Monats keine Überraschung erwartet. 

## <a name="what-is-an-azure-ad-tenant"></a>Was ist ein Azure AD-Mandant?

Azure AD (Azure Active Directory) ist ein moderner Identitätsanbieter, der viele Authentifizierungsprotokolle unterstützt, um Anwendungen und Dienste in der Cloud zu schützen. Azure AD ist _nicht_ das gleiche wie Windows Active Directory – bei Windows Active Directory liegt der Fokus auf dem Schutz von Windows-Desktops und -Servern. Bei Azure AD geht es hauptsächlich um webbasierte Authentifizierungsstandards wie OpenID und OAuth.

Ein einzelner Mandant stellt eine logische Organisation dar und ermöglicht, dass mehrere Identitäten auf Ressourcen zugreifen können, die vom Mandanten geschützt werden und diese nutzen können. Ein Azure-Abonnement hat immer eine Vertrauensstellung mit einem _einzelnen_ Azure AD-Mandanten. Es können aber _mehrere_ Abonnements einen einzelnen Mandanten teilen. Diese Struktur ermöglicht Organisationen, mehrere Abonnements zu verwalten und Sicherheitsregeln für alle darin enthaltenen Ressourcen festzulegen.

Hier sehen Sie eine einfache Darstellung von Konten, Abonnements, Mandanten und Ressourcen.

![Diagramm des Zusammenwirkens von Konten, Mandanten, Abonnements und Ressourcen](../media/3-azure-ad-tenant.png)

Beachten Sie, dass jeder Azure AD-Mandant einen _Kontobesitzer_ hat. Dies ist das ursprüngliche Azure-Konto, das für die Abrechnung verwendet wird. Sie können dem Mandanten zusätzliche Benutzer hinzufügen und sogar Gästen von anderen Azure AD-Mandanten den Zugriff auf Ressourcen in Abonnements gewähren.

## <a name="azure-account-types"></a>Azure-Kontotypen

Azure bietet mehrere Kontotypen, die verschiedene Kundenwünsche erfüllen. Folgende Konten werden am häufigsten verwendet:

- Kostenlos
- Nutzungsbasierte Bezahlung
- Enterprise Agreement

### <a name="azure-free-account"></a>Kostenloses Azure-Konto

Ein kostenloses Azure-Konto enthält ein **Guthaben in Höhe von 200 USD**, das in den ersten 30 Tagen ausgegeben werden kann, 12 Monate lang kostenlosen Zugriff auf die beliebtesten Azure-Produkte sowie Zugriff auf über 25 Produkte, die immer kostenlos sind. Dieses Konto bietet neuen Benutzern eine hervorragende Möglichkeit für den Einstieg. Um ein kostenloses Konto einzurichten, benötigen Sie eine Telefonnummer, eine Kreditkarte und ein Microsoft-Konto.

> [!NOTE]
> Kreditkarteninformationen dienen nur der Identitätsüberprüfung. Ihnen werden keine Dienste in Rechnung gestellt bis Sie ein höheres Abonnement auswählen.

### <a name="azure-pay-as-you-go-account"></a>Azure-Konto mit nutzungsbasierter Bezahlung

Bei einem Konto mit nutzungsbasierter Bezahlung (PAYG) werden Ihnen monatlich die Dienste in Rechnung gestellt, die Sie genutzt haben. Dieser Kontotyp eignet sich für eine Vielzahl von Benutzern – von Einzelpersonen über kleine Unternehmen bis hin zu großen Organisationen.

### <a name="azure-enterprise-agreement"></a>Azure Enterprise Agreement

Ein Enterprise Agreement bietet Flexibilität für den Erwerb von Clouddiensten und Softwarelizenzen im Rahmen einer einzigen Vereinbarung sowie Rabatte für neue Lizenzen und Software Assurance. Dieser Kontotyp ist auf sehr große Organisationen ausgerichtet.

## <a name="summary"></a>Zusammenfassung

Um Azure-Dienste verwenden zu können, benötigen Sie ein Konto. Dabei spielt es keine Rolle, ob der Kontoinhaber eine Einzelperson, ein kleines Unternehmen oder ein großer Konzern ist. In der Regel starten neue Benutzer mit einem kostenlosen Konto, um Azure-Dienste testen zu können. Wenn der Testzeitraum abgelaufen ist, wird das kostenlose Konto zumeist in ein Konto mit nutzungsbasierter Bezahlung umgewandelt.