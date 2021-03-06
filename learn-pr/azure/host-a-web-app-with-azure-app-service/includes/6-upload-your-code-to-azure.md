Nun wollen wir uns ansehen, wie wir unsere Inhalte mit wenig oder ohne Ausfallzeit bereitstellen können.

## <a name="what-is-a-deployment-slot"></a>Was ist ein Bereitstellungsslot?

Ein Bereitstellungsslot ist eine **unabhängige** App in App Service mit eigenem Inhalt, eigener Konfiguration und sogar einem eindeutigen Hostnamen. Aus diesem Grund funktioniert er wie jede andere App in App Service.

Auf jeden Bereitstellungsslot kann über seine eindeutige URL zugegriffen werden. Angenommen, ich habe einen Bereitstellungsslot des Typs **Staging** mit dem Namen `BESTBIKE` hinzugefügt. Die URLs für die Anwendung und den Bereitstellungsslot sind wie folgt:

- https://BESTBIKE.azurewebsites.net/
- https://BESTBIKE-staging.azurewebsites.net/

## <a name="why-are-deployment-slots-useful"></a>Warum sind Bereitstellungsslots nützlich?

Die Bereitstellung Ihrer Webanwendung auf herkömmliche Weise, sei es per FTP, Web Deploy, Git oder auf andere Weise, hat gewisse Schwächen:

- Nach Abschluss der Bereitstellung wird die App möglicherweise neu gestartet, was zu einem **Kaltstart** der Anwendung führt. Die erste Anforderung an die Anwendung wird langsamer sein.

- Möglicherweise stellen Sie eine *fehlerbehaftete* Version Ihrer App bereit. Sie sollten sie vorher (in der Produktion) testen, bevor Sie sie an Ihren Kunden weitergeben.

Hier kommen Bereitstellungsslots ins Spiel. Sie können Änderungen an Ihrer App in einem Bereitstellungsslot des Typs **Staging** vornehmen und die Änderungen testen, ohne die Benutzer zu beeinträchtigen, die auf den Bereitstellungsslot **Produktion** zugreifen. Wenn Sie bereit sind, die neuen Features in die Produktion zu übernehmen, können Sie die Staging- und Produktionsslots **ohne Ausfallzeit** einfach **tauschen**.

Ein weiterer Vorteil der Verwendung von Bereitstellungsslots ist, dass Sie Ihre Anwendung in einem Stagingslot **aufwärmen** können, bevor Sie sie an den Produktionsslot übergeben. So vermeiden Sie die Verzögerungen eines **Kaltstarts** und lange Initialisierungscodes.

Schließlich können Sie zum vorherigen Bereitstellungsslot **zurückkehren**, wenn Sie feststellen, dass die neue Version Ihrer Anwendung nicht wie erwartet funktioniert.

## <a name="what-is-automated-deployment"></a>Was bedeutet automatisierte Bereitstellung?

Die automatisierte Bereitstellung oder Continuous Integration ist ein Prozess, der dazu dient, neue Funktionen und Fehlerkorrekturen in einem schnellen und sich wiederholenden Muster mit minimalen Auswirkungen auf die Endbenutzer zu implementieren.

Azure unterstützt die automatische Bereitstellung direkt aus verschiedenen Quellen. Die folgenden Optionen sind verfügbar:

- **Visual Studio Team Services (VSTS)**: Sie können Ihren Code per Push an VSTS übertragen, den Build für Ihren Code in der Cloud durchführen, die Tests ausführen, eine Version aus dem Code generieren und schließlich Ihren Code per Push an ein Azure-Web-App übertragen.

- **GitHub**: Azure unterstützt die automatische Bereitstellung direkt aus GitHub. Wenn Sie Ihr GitHub-Repository für die automatische Bereitstellung mit Azure verbinden, werden alle Änderungen, die Sie in Ihrem Produktions-Branch auf GitHub vornehmen, automatisch für Sie bereitgestellt.

- **Bitbucket**: Ähnlich wie mit GitHub können Sie mit Bitbucket eine automatisierte Bereitstellung konfigurieren.

- **OneDrive**: Sie können Ihr OneDrive-Konto mit App Service verbinden, sodass Azure das Ändern einer Datei in Ihrem OneDrive-Konto automatisch erkennt und alle Änderungen in die Web-App-Dateien einfließen lässt. Dies ist eine sehr nützliche Option für statische Websites. Sie haben das Gefühl, dass Sie es mit einem lokalen Dateisystem zu tun haben, das alle Änderungen in Azure sofort und reibungslos widerspiegelt.

- **Dropbox**: Ähnlich wie bei OneDrive können Sie Ihre Web-App-Dateien in einem Dropbox-Konto hosten und automatisch über eine Web-App verteilen lassen.

- **Externes Repository**: Sie können die automatische Bereitstellung mit einem externen Git-Repository konfigurieren.

### <a name="non-automated-deployment-to-azure"></a>Nicht automatisierte Bereitstellung in Azure

Ihnen stehen verschiedene Optionen zur Verfügung, um Ihren Code manuell per Push in Azure zu übertragen:

- **FTP/S**: FTP oder FTPS ist eine herkömmliche Methode, Ihren Code per Push in beliebige Hostingumgebungen zu übertragen. Trotz der Tatsache, dass diese Methode nicht mehr empfohlen wird, können Sie sie trotzdem weiterhin nutzen.

- **Web Deploy/IDE**: Sie können die integrierte Entwicklungsumgebung von Visual Studio zum Veröffentlichen Ihrer Web-App in Azure einsetzen. Der Visual Studio-Veröffentlichungsmechanismus nutzt Web Deploy-Technologie, um Ihren Code per Push in Azure zu übertragen.

- **Git**: Azure verwaltet ein **lokales Git-Repository** für Ihre Anwendung. Sie können Ihren Code einfach direkt in diesem **committen**.

> In diesem Modul führen wir eine nicht automatisierte Bereitstellung mit Git durch.

## <a name="summary"></a>Zusammenfassung

Azure bietet mehrere Möglichkeiten, Ihren Code entsprechend Ihrem aktuellen bevorzugten Workflow hochzuladen. Sie können auch Bereitstellungsslots verwenden, um Ausfallzeiten für Ihre Benutzer zu vermeiden.
