Azure Active Directory (Azure AD) ist nicht einfach ein Domänencontroller in der Cloud. Azure AD ist ein mehrinstanzenfähiger, cloudbasierter Verzeichnis- und Identitätsverwaltungsdienst. Er kombiniert grundlegende Verzeichnisdienste, Application Access Management und Identitätsschutz in einer einzigen Lösung. Azure AD kann in Verbindung mit einer vorhandenen Windows Server Active Directory-Umgebung über Azure AD Connect arbeiten. Dies ermöglicht Ihnen die Nutzung bestehender lokaler Identitätsinvestitionen.

Azure AD ist in vier Editionen erhältlich. Für diese Übung konzentrieren wir uns nur auf Features in den Editionen Azure AD Premium P1 und P2.

In diesem Modul erstellen wir ein Azure AD-Verzeichnis, in dem alle unsere Benutzer und Gruppen gespeichert sind, ähnlich wie in einem lokalen Verzeichnis.

Wenn wir das Verzeichnis erstellen, werden unserem Konto automatisch globale Administratorrechte zugeordnet. Konten mit globalen Administratorrechten sollten reguliert werden, da sie Vollzugriff auf alle administrativen Features von Azure AD haben. Sie können mehrere globale Administratoren festlegen, aber nur globale Administratoren können Benutzern eine der weiteren Administratorrollen zuweisen.

## <a name="how-can-azure-ad-help-you-protect-access-to-applications"></a>Wie kann Azure AD dabei helfen, den Zugriff auf Anwendungen zu schützen?

Azure AD Premium umfasst Features wie Multi-Factor Authentication und Richtlinien für bedingten Zugriff. Wenn diese Features zusammen verwendet werden, bieten diese beim Schutz des Zugriffs auf Anwendungen die meiste Granularität.

Eine Richtlinie für bedingten Zugriff setzt sich wie folgt zusammen:
   * Benutzer oder Gruppen
   * Anwendungen, auf die versucht wird zuzugreifen
   * Zu erfüllende Steuerelemente, z.B. Multi-Factor Authentication

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie die Grundlagen von Azure AD kennengelernt und erfahren, welche Features zum Sichern des Zugriffs auf Anwendungen zur Verfügung stehen. Nun, da Sie die Grundlagen kennen, können wir mit den ersten Schritten mit Azure AD beginnen. Der Rest dieses Moduls enthält praktische Übungen zum Aktivieren und Testen von Multi-Factor Authentication mithilfe des bedingten Zugriffs.
