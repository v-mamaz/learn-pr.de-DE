Eines der größten Probleme mit Sicherheit wird allen Bereichen angezeigt, die Sie benötigen, um zu schützen sowie zum Suchen von Sicherheitslücken vor Hackern. Azure bietet, dass ein Dienst, der dadurch wesentlich einfacher wird Azure Security Center aufgerufen.

## <a name="what-is-azure-security-center"></a>Was ist Azure Security Center?

Azure Security Center (ASC) ist ein Überwachungsdienst, der Schutz vor Bedrohungen über alle Dienste in Azure und lokalen bereitstellt. Sie können:

- Bereitzustellen Sie sicherheitsempfehlungen, die basierend auf Ihrer Konfigurationen, Ressourcen und Netzwerke.
- Überwachen von Sicherheitseinstellungen für lokale und cloud-Workloads und erforderlichen Sicherheitsmaßnahmen automatisch auf neue Dienste anwenden, wie sie online geschaltet.
- Kontinuierlich überwachen Sie alle Ihre Dienste aus, und führen Sie die automatische sicherheitsbewertungen, um mögliche Sicherheitsrisiken zu erkennen, bevor sie ausgenutzt werden können.
- Verwenden Sie für maschinelles lernen zum Erkennen und blockieren Schadsoftware in Ihre Dienste und virtuellen Computern installiert werden. Sie können auch die Positivliste Anwendungen sicherstellen, dass nur die apps, die Sie überprüfen, ausgeführt werden dürfen.
- Analysieren und potenzielle eingehende Angriffe zu identifizieren und Untersuchen von Bedrohungen und alle Aktivitäten nach einer sicherheitsverletzung die aufgetreten sind.
- Just-In-Time-Zugriffssteuerung für Ports, die Ihre Angriffsfläche zu verkleinern, indem sichergestellt wird nur für die Netzwerk-Verkehr, die Sie benötigen.

ASC ist Teil der [Center für internetsicherheit](https://www.cisecurity.org/cis-benchmarks/) (CIS) Empfehlungen.

## <a name="activating-azure-security-center"></a>Aktivieren von Azure Security Center

Azure Security Center bietet einheitliche sicherheitsverwaltung und erweiterten Schutz vor Bedrohungen für Hybrid Cloud-Workloads und wird in zwei Tarifen angeboten: Free und Standard. Im free-Tarif bietet Sicherheitsrichtlinien, Bewertungen und Empfehlungen und den Tarif "Standard" eine Reihe robuste Funktionen, einschließlich Informationen zu Bedrohungen.

Das Sicherheitsteam Ihres Unternehmens hat entschieden, dass sie für alle Abonnements am Arbeitsplatz aktiviert werden, wenn die Vorteile von ASC. Heute Morgen haben eine e-Mail, aktivieren Sie ihn für Ihre Anwendungen – wir uns an, die Vorgehensweise.

1. Öffnen der [Azure-Portal](https://portal.azure.com?azure-portal=true) , und wählen Sie **Azure Security Center** im linken Menü, wenn es dort nicht angezeigt wird können Sie auswählen **alle Dienste** und  **Security Center** im Abschnitt "Sicherheit" wie unten dargestellt.

![Öffnen Sie Azure Security Center](../media-draft/ASC-Menu.png)

2. Wenn Sie ASC nie geöffnet haben, startet auf das Blatt auf die **Einstieg** -Eintrag in dem Sie ein Upgrade Ihres Abonnements gebeten. Wählen Sie im Moment ignorieren **überspringen** am unteren Rand der Seite, und wählen Sie dann **Übersicht**.
    - Dadurch wird das "big Sicherheit Bild" auf alle Elemente, die in Ihrem Abonnement verfügbaren angezeigt.
    - Dies hat eine Menge mit nützlichen Informationen, die Sie untersuchen können.

3. Wählen Sie als Nächstes **Coverage**unter "Richtlinie und Kompatibilität". Dadurch wird angezeigt, was die Abonnement-Elemente abgedeckt (oder nicht behandelt), von ACS. Hier können Sie ACS für jedes Abonnement aktivieren, die, denen Sie können zugreifen. Wechseln Sie zwischen den drei Bereichen der Abdeckung: "Nicht abgedeckt", "Basic-Abdeckung" und "Standard-Abdeckung".

4. Eine Aufforderung zum Aktivieren von ACS-Abonnements, die nicht behandelt werden müssen. Drücken Sie die Schaltfläche "Jetzt aktualisieren", um ACS für alle Ressourcen im Abonnement zu aktivieren.

![Aktualisieren Sie Schutz](../media-draft/Upgrade-Now.png)

### <a name="free-vs-standard-pricing-tier"></a>Kostenlose Visual Studio. Tarif „Standard“

Während Sie eine kostenlose Azure-Abonnement-Ebene mit ASC verwenden können, ist es auf die Bewertung und Empfehlungen von Azure-Ressourcen beschränkt. Um ASC wirklich nutzen zu können, müssen Sie zum upgrade auf ein Standard-Tarif-Abonnement wie oben gezeigt. Sie können Ihr Abonnement über die Schaltfläche "Jetzt aktualisieren" im aktualisieren die **Coverage** auf dem Blatt, wie oben bereits erwähnt. Sie können auch zum Wechseln der **Einstieg** Blatt im Menü "ASC" Ändern von Ihrer Abonnementstufe schrittweise. Preisgestaltung und den Funktionen möglicherweise ändern sich in der Region, können Sie eine vollständige Übersicht über die bei der [Preisseite](https://azure.microsoft.com/en-us/pricing/details/security-center/). 

> [!NOTE]
> Um ein Abonnement auf den Standard-Tarif zu aktualisieren, muss Ihnen die Rolle „Abonnementbesitzer“, „Mitwirkender“ am Abonnement oder „Sicherheitsadministrator“ zugewiesen werden.

> [!IMPORTANT]
> Nach Ablauf der 60-Tage-Testzeitraum, themennachrichten ASC **15 $/ Knoten pro Monat** und auf Ihr Konto abgerechnet.

## <a name="turning-off-azure-security-center"></a>Das Deaktivieren des Azure Security Center

Für Produktionssysteme sollten Sie definitiv zu Azure Security Center aktiviert, so dass sie alle Ihre Ressourcen auf Bedrohungen überwachen kann. Aber wenn Sie sind mit ASC einfach herumgespielt, und es eingeschaltet, möchten Sie wahrscheinlich deaktivieren, um sicherzustellen, dass Sie nicht in Rechnung gestellt werden. Lassen Sie uns dies jetzt tun.

1. Öffnen der [Azure-Portal](https://portal.azure.com?azure-portal=true) , und wählen Sie **Azure Security Center** im linken Menü, wenn es dort nicht angezeigt wird können Sie auswählen **alle Dienste** und  **Security Center** im Abschnitt "Sicherheit" wie unten dargestellt.

![Öffnen Sie Azure Security Center](../media-draft/ASC-Menu.png)

2. Wählen Sie **Sicherheitsrichtlinie** im linken Menü.

3. Wählen Sie als Nächstes **Einstellungen Bearbeiten >** neben dem Abonnement, für die ASC herabgestuft werden sollen.

4. Wählen Sie auf dem nächsten Bildschirm "Tarif" im linken Menü aus.

5. Eine neue Seite wird angezeigt, die wie folgt aussieht. Klicken Sie auf das Feld auf der linken Seite, die besagt "Free (für Azure-Ressourcen nur)".

![Preisstufe](../media-draft/Pricing-Tier.png)

6. Drücken Sie die Schaltfläche "Speichern", am oberen Rand des Bildschirms aus.

Sie haben nun Ihr Abonnement für den free-Tarif von Azure Security Center herabgestuft.

## <a name="summary"></a>Zusammenfassung

<!-- TODO: need link to module --> Herzlichen Glückwunsch! Sie haben den ersten (und am wichtigsten) Schritt zum Schützen der Anwendung, Daten und Netzwerk weitergeleitet. <!--If you want to learn more about Azure Security Center, you can go through the **Protect your resources with Azure Security Center** learning module.-->
