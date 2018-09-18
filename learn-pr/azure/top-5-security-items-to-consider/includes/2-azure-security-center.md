Eines der größten Probleme in Bezug auf die Sicherheit besteht darin, alle Bereiche zu erkennen, die geschützt werden müssen, und Sicherheitsrisiken zu ermitteln, bevor Hackern dies gelingt. Azure stellt den Azure Security Center-Dienst bereit, um dies zu vereinfachen.

## <a name="what-is-azure-security-center"></a>Was ist Azure Security Center?

Azure Security Center (ASC) ist ein Überwachungsdienst, der Schutz vor Bedrohungen für Ihre gesamten Dienste ermöglicht – sowohl in Azure als auch lokal. Sie haben damit folgende Möglichkeiten:

- Bereitstellen von Sicherheitsempfehlungen basierend auf Ihren Konfigurationen, Ressourcen und Netzwerken
- Überwachen von Sicherheitseinstellungen für Workloads lokal und in der Cloud und automatisches Anwenden der erforderlichen Sicherheitsmaßnahmen auf neue Dienste, wenn diese in den Onlinezustand versetzt werden
- Fortlaufendes Überwachen Ihrer gesamten Dienste und Durchführen von automatischen Sicherheitsbewertungen zur Identifikation von potenziellen Sicherheitsrisiken, bevor diese ausgenutzt werden können
- Verwenden des maschinellen Lernens zum Erkennen und Blockieren der Installation von Schadsoftware in Ihren Diensten und auf Ihren virtuellen Computern. Sie können Anwendungen auch auf eine Positivliste setzen, um sicherzustellen, dass die von Ihnen überprüften Apps ausgeführt werden dürfen.
- Analysieren und Identifizieren von potenziellen eingehenden Angriffen und Untersuchen von Bedrohungen und etwaigen Aktivitäten nach Sicherheitsverletzungen
- Just-In-Time-Zugriffssteuerung für Ports zur Reduzierung Ihrer Angriffsfläche, indem sichergestellt wird, dass für das Netzwerk nur benötigter Datenverkehr zugelassen wird

ASC ist Teil der Empfehlungen des [Center for Internet Security](https://www.cisecurity.org/cis-benchmarks/) (CIS).

## <a name="activating-azure-security-center"></a>Aktivieren von Azure Security Center

Aufgrund der Vorteile von ASC hat das Sicherheitsteam Ihres Unternehmens die Entscheidung getroffen, den Dienst für alle genutzten Abonnements zu aktivieren. Sie haben heute Morgen eine E-Mail mit dem Hinweis erhalten, den Dienst für Ihre Anwendungen zu aktivieren. Wir sehen uns also an, wie Sie dies erreichen.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com?azure-portal=true), und wählen Sie im Menü auf der linken Seite die Option **Azure Security Center**. Wenn die Option nicht angezeigt wird, können Sie **Alle Dienste** wählen und wie unten gezeigt im Sicherheitsabschnitt nach **Security Center** suchen.

![Öffnen von Azure Security Center](../media-draft/ASC-Menu.png)

2. Falls Sie ASC zum ersten Mal öffnen, wird das Blatt mit dem Eintrag **Erste Schritte** gestartet, und Sie werden ggf. aufgefordert, ein Upgrade für Ihr Abonnement durchzuführen. Ignorieren Sie dies vorerst, und wählen Sie unten auf der Seite die Option **Überspringen** und dann **Übersicht**.
    - Eine allgemeine Sicherheitsübersicht für alle verfügbaren Elemente Ihres Abonnements wird angezeigt.
    - Sie können viele verschiedene Informationen erkunden.

3. Wählen Sie als Nächstes unter „Policy and Compliance“ (Richtlinie und Konformität) die Option **Abdeckung**. Es wird angezeigt, welche Abonnementelemente mit ACS abgedeckt bzw. nicht abgedeckt werden. Hier können Sie ACS für alle Abonnements aktivieren, auf die Sie Zugriff haben. Versuchen Sie, zwischen den drei Abdeckungsbereichen zu wechseln: „Nicht abgedeckt“, „Basic-Abdeckung“ und „Standard-Abdeckung“.

4. Abonnements, die nicht abgedeckt sind, verfügen über eine Aufforderung zur Aktivierung von ACS. Sie können die Schaltfläche „Jetzt aktualisieren“ verwenden, um ACS für alle Ressourcen des Abonnements zu aktivieren.

![Aktualisieren der Abdeckung](../media-draft/Upgrade-Now.png)

### <a name="free-vs-standard-pricing-tier"></a>Vergleich: Tarif „Free“ und Tarif „Standard“

Sie können für ASC zwar auch einen kostenlosen Azure-Abonnementtarif verwenden, aber dann sind nur Bewertungen und Empfehlungen für Azure-Ressourcen möglich. Um ASC wirklich zu nutzen, müssen Sie wie oben gezeigt ein Upgrade auf ein Abonnement des Standard-Tarifs durchführen. Sie können Ihr Abonnement wie oben beschrieben über die Schaltfläche „Jetzt aktualisieren“ auf dem Blatt **Abdeckung** aktualisieren. Sie können auch im ASC-Menü zum Blatt **Erste Schritte** wechseln, auf dem das Ändern der Abonnementebene Schritt für Schritt beschrieben wird. Die Preise und Features können sich je nach Region ändern. Eine vollständige Übersicht finden Sie auf der [Seite mit den Preisen](https://azure.microsoft.com/en-us/pricing/details/security-center/). 

> [!NOTE]
> Um ein Abonnement auf den Standard-Tarif zu aktualisieren, muss Ihnen die Rolle „Abonnementbesitzer“, „Abonnementmitwirkender“ oder „Sicherheitsadministrator“ zugewiesen werden.

> [!IMPORTANT]
> Nachdem der Testzeitraum von 60 Tagen abgelaufen ist, beträgt der Preis für ASC **monatlich 15 USD/Knoten** und wird Ihrem Konto berechnet.

## <a name="turning-off-azure-security-center"></a>Deaktivieren von Azure Security Center

Für Produktionssysteme ist es ratsam, Azure Security Center deaktiviert zu lassen, damit darüber alle Ressourcen auf Bedrohungen überwacht werden können. Wenn Sie ASC aber lediglich ausprobieren möchten und nur zu diesem Zweck aktiviert haben, empfiehlt es sich, die Anwendung zu deaktivieren, damit keine Kosten anfallen. Dies führen wir nun durch.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com?azure-portal=true), und wählen Sie im Menü auf der linken Seite die Option **Azure Security Center**. Wenn die Option nicht angezeigt wird, können Sie **Alle Dienste** wählen und wie unten gezeigt im Sicherheitsabschnitt nach **Security Center** suchen.

![Öffnen von Azure Security Center](../media-draft/ASC-Menu.png)

2. Wählen Sie im Menü auf der linken Seite die Option **Sicherheitsrichtlinie**.

3. Wählen Sie als Nächstes neben dem Abonnement, für das Sie für ASC ein Downgrade durchführen möchten, die Option **Einstellungen bearbeiten**.

4. Wählen Sie im nächsten Fenster im Menü auf der linken Seite die Option „Tarif“.

5. Eine neue Seite wird angezeigt, die wie folgt aussieht. Klicken Sie links auf das Feld „Free (for Azure resources only)“ (Free (nur für Azure-Ressourcen)).

![Tarif](../media-draft/Pricing-Tier.png)

6. Klicken Sie oben auf der Seite auf „Speichern“.

Sie haben für Ihr Abonnement jetzt das Downgrade auf den Free-Tarif von Azure Security Center durchgeführt.

## <a name="knowledge-check"></a>Wissenstest
<!-- TODO: move into yaml --> Markieren Sie alle ASC-Features mit einem Häkchen.

* Empfehlungen (richtig)
* Entschärfungen (falsch)
* Schutzmaßnahmen (falsch)
* Just-in-Time (richtig)
* Bedrohungserkennung (richtig)

## <a name="summary"></a>Zusammenfassung

<!-- TODO: need link to module --> Glückwunsch! Sie haben den ersten (und wichtigsten) Schritt zum Schützen Ihrer Anwendung, der Daten und des Netzwerks getan! <!--If you want to learn more about Azure Security Center, you can go through the **Protect your resources with Azure Security Center** learning module.-->
