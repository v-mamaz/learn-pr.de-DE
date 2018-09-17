Mit einem kostenlosen Azure-Konto können Sie Unternehmensanwendungen erstellen, testen und bereitstellen, benutzerdefinierte webbasierte und mobile Umgebungen erstellen und über Machine Learning und leistungsstarke Analysen Einblicke in Ihre Daten gewinnen.

## <a name="what-is-an-azure-account"></a>Was ist ein Azure-Konto?

Ein _Azure-Konto_ ist an eine bestimmte Identität gebunden und enthält unter anderem folgende Informationen:

- Name, E-Mail-Adresse und bevorzugte Optionen für die Kontaktaufnahme
- Abrechnungsinformationen wie z.B. Kreditkartendaten

Ein Azure-Konto ist mindestens einem _Abonnement_ zugeordnet.

## <a name="what-is-an-azure-subscription"></a>Was ist ein Azure-Abonnement?

Ein _Azure-Abonnement_ ist ein logischer Container zur Bereitstellung von Ressourcen in Microsoft Azure. Es enthält Details zu all Ihren Ressourcen (etwa zu Ihren virtuellen Computern und Datenbanken). Darüber hinaus hat es eine Vertrauensstellung mit einem einzelnen Azure AD-_Mandanten_, der für die Authentifizierung der im Abonnement enthaltenen Benutzer und Rollen verwendet wird.

Die Abrechnung erfolgt auf Abonnementebene. Sie können Ausgabenlimits für jedes Abonnement festlegen, damit Sie am Ende des Monats keine Überraschung erleben. 

## <a name="what-is-an-azure-ad-tenant"></a>Was ist ein Azure AD-Mandant?

Azure AD (Azure Active Directory) ist ein moderner Identitätsanbieter, der mehrere Authentifizierungsprotokolle unterstützt, um Anwendungen und Dienste in der Cloud zu schützen. Azure AD ist _nicht_ dasselbe wie Windows Active Directory: Bei Windows Active Directory liegt der Fokus auf dem Schutz von Windows-Desktops und -Servern. Bei Azure AD stehen dagegen webbasierte Authentifizierungsstandards wie OpenID und OAuth im Mittelpunkt.

Ein einzelner Mandant stellt eine logische Organisation dar und ermöglicht mehreren Identitäten den Zugriff auf und die Nutzung von Ressourcen, die durch diesen Mandanten geschützt werden. Ein Azure-Abonnement hat immer eine Vertrauensstellung mit einem _einzelnen_ Azure AD-Mandanten. Ein einzelner Mandant kann aber von _mehreren_ Abonnements genutzt werden. Diese Struktur ermöglicht es Organisationen, mehrere Abonnements zu verwalten und Sicherheitsregeln für alle darin enthaltenen Ressourcen festzulegen.

Hier sehen Sie eine einfache Darstellung von Konten, Abonnements, Mandanten und Ressourcen.

![Diagramm des Zusammenwirkens von Konten, Mandanten, Abonnements und Ressourcen](../media/3-azure-ad-tenant.png)

Beachten Sie, dass jeder Azure AD-Mandant einen _Kontobesitzer_ hat. Dies ist das ursprüngliche Azure-Konto, das für die Abrechnung verwendet wird. Sie können dem Mandanten zusätzliche Benutzer hinzufügen und sogar Gästen aus anderen Azure AD-Mandanten Zugriff auf Ressourcen in Abonnements gewähren.

## <a name="azure-account-types"></a>Azure-Kontotypen

Azure bietet mehrere Kontotypen für unterschiedliche Arten von Kunden. Folgende Konten werden am häufigsten verwendet:

- Kostenlos
- Nutzungsbasierte Bezahlung
- Enterprise Agreement

### <a name="azure-free-account"></a>Kostenloses Azure-Konto

Ein kostenloses Azure-Konto beinhaltet ein **Guthaben in Höhe von 200 USD**, das in den ersten 30 Tagen ausgegeben werden kann, und bietet 12 Monate lang kostenlosen Zugriff auf die beliebtesten Azure-Produkte sowie Zugriff auf über 25 Produkte, die immer kostenlos sind. Dieses Konto ist eine hervorragende Einstiegsmöglichkeit für neue Benutzern. Für die Einrichtung eines kostenlosen Kontos benötigen Sie eine Telefonnummer, eine Kreditkarte und ein Microsoft-Konto.

> [!NOTE]
> Kreditkarteninformationen dienen nur der Identitätsüberprüfung. Ihnen werden keine Dienste in Rechnung gestellt, bis Sie ein Upgrade durchführen.

### <a name="azure-pay-as-you-go-account"></a>Azure-Konto mit nutzungsbasierter Bezahlung

Bei einem Konto mit nutzungsbasierter Bezahlung (PAYG) werden Ihnen monatlich die Dienste in Rechnung gestellt, die Sie genutzt haben. Dieser Kontotyp eignet sich für eine Vielzahl von Benutzern – von Einzelpersonen über kleine Unternehmen bis hin zu großen Organisationen.

### <a name="azure-enterprise-agreement"></a>Azure Enterprise Agreement

Ein Enterprise Agreement bietet Flexibilität für den Erwerb von Clouddiensten und Softwarelizenzen im Rahmen einer einzigen Vereinbarung sowie Rabatte für neue Lizenzen und Software Assurance. Dieser Kontotyp ist auf sehr große Organisationen ausgerichtet.

## <a name="summary"></a>Zusammenfassung

Für die Verwendung von Azure-Diensten wird ein Konto benötigt. Das gilt für Einzelpersonen ebenso wie für kleine Unternehmen oder große Konzerne. In der Regel beginnen neue Benutzer mit einem kostenlosen Konto, um Azure-Dienste testen zu können. Nach Ablauf des Testzeitraums wird das kostenlose Konto zumeist in ein Konto mit nutzungsbasierter Bezahlung umgewandelt.