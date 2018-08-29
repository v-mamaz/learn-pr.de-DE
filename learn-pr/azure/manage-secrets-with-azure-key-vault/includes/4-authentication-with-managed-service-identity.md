Azure Key Vault verwendet **Azure Active Directory** zum Authentifizieren von Benutzern und Anwendungen, die versuchen, auf einen Tresor zuzugreifen. Um unserer Webanwendung Zugriff auf den Tresor zu gewähren, müssen wir unsere App zunächst bei Azure Active Directory registrieren. Bei der Registrierung wird eine Identität für die App erstellt. Sobald eine Identität vorliegt, können wir ihr Tresorberechtigungen zuweisen.

Anwendungen und Benutzer authentifizieren sich bei Key Vault mit einem Azure Active Directory-Authentifizierungstoken. Um ein Token von Azure Active Directory zu beziehen, ist ein Geheimnis oder Zertifikat erforderlich, da jeder mit einem Token die Anwendungsidentität verwenden kann, um auf alle Geheimnisse im Tresor zuzugreifen.

Unsere Anwendungsgeheimnisse sind im Tresor sicher, aber wir benötigen trotzdem noch ein Geheimnis oder Zertifikat außerhalb des Tresors, um darauf zugreifen zu können! Dieses Problem wird *Bootstrapping* genannt, wofür Azure allerdings eine Lösung hat.

## <a name="managed-service-identity"></a>Verwaltete Dienstidentität

*Verwaltete Dienstidentität* (Managed Service Identity, MSI) ist ein Feature von Azure App Service, mit dem Ihre App auf Key Vault und andere Azure-Dienste zugreifen kann, ohne selbst ein Geheimnis verwalten zu müssen. Die Verwendung von MSI ist einfacher und sicherer als die Verwaltung eines Geheimnisses durch Sie.

Wenn Sie MSI aktivieren, aktiviert Azure einen separaten ein Token gewährenden REST-Dienst speziell für Ihre Anwendung. Wenn Ihre Anwendung ein Token vom MSI-Tokendienst anfordert, kontaktiert der Dienst Azure Active Directory, um ein Token für die MSI-Identität zu beziehen, das an Ihre Anwendung zur Verwendung mit Key Vault zurückgegeben wird. Der wichtigste Teil dieses Workflows ist die Art und Weise, in der sich Ihre Anwendung beim MSI-Tokendienst authentifiziert. Anstatt ein Geheimnis oder Zertifikat zu benötigen, das Sie in Ihrer Konfiguration verwalten müssen, verwendet Ihre Anwendung ein Geheimnis, das Azure beim Start sicher in seine Umgebungsvariablen einfügt. Sie müssen diesen geheimen Wert nirgendwo mehr verwalten oder speichern. Nichts außerhalb Ihrer Anwendung kann auf dieses Geheimnis oder den Endpunkt des MSI-Tokendiensts zugreifen.

MSI registriert Ihre Anwendung auch für Sie in Azure Active Directory und löscht die Registrierung, sobald Sie MSI deaktivieren oder die Anwendung löschen.

MSI ist in allen Editionen von Azure Active Directory verfügbar, einschließlich der Free Edition, die in einem Azure-Abonnement enthalten ist. Seine Verwendung in App Service ist kostenlos, erfordert keine Konfiguration und kann jederzeit in einer App aktiviert oder deaktiviert werden.

> [!NOTE]
> MSI wird für Linux- oder Container-Web-Apps derzeit nicht unterstützt.

Für die Aktivierung von MSI muss nur ein einziger Azure CLI-Befehl ohne Konfiguration ausgeführt werden. Das machen wir in Einheit 5, wenn wir eine App Service-App einrichten und in Azure bereitstellen. Vorher werden wir jedoch unser Wissen über MSI nutzen, um den Code für unsere App zu schreiben.