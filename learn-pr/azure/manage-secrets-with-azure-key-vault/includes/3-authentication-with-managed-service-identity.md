Key Vault verwendet **Azure Active Directory** zum Authentifizieren von Benutzern und Anwendungen, die versuchen, einen Tresor zugreifen. Um unsere Web-Anwendungszugriff auf den Tresor zu gewähren, müssen wir zuerst unsere app in Azure Active Directory zu registrieren. Registrieren eine Identität für die app erstellt wird. Sobald wir eine Identität verfügen, können wir es Vault-Berechtigungen zuweisen.

Apps und Benutzer in den Schlüsseltresor verwenden ein Azure Active Directory-Authentifizierungstoken zu authentifizieren. Abrufen eines Tokens aus Azure Active Directory erfordert einen geheimen Schlüssel oder das Zertifikat, da jeder Benutzer mit einem Token die Identität verwenden kann, alle geheimen Schlüssel im Tresor den Zugriff auf.

Unsere geheime Schlüssel für Anwendungen sind im Tresor sicher, jedoch müssen noch ein Geheimnis oder Zertifikat außerhalb des Tresors zu lassen, um den Zugriff! Dieses Problem wird aufgerufen, die *bootstrapping Problem*, und Azure verfügt über eine Lösung dafür.

## <a name="managed-service-identity"></a>Verwaltete Dienstidentität

*Verwaltete Dienstidentität* (MSI) ist ein Feature von Azure App Service, mit denen Ihre app Key Vault und andere Azure-Dienste zugreifen, ohne selbst einen einzelnen geheimen Schlüssel verwalten zu müssen. Mithilfe der MSI-Datei ist einfacher und sicherer als die ein geheimen Schlüssels selbst verwalten.

Wenn Sie MSI aktivieren, aktiviert Azure einen separaten-Token-granting-REST-Dienst speziell für die Verwendung von Ihrer app. Wenn Ihre app ein Token vom Tokendienst MSI-Datei anfordert, wird der Dienst Azure Active Directory zum Abrufen eines Tokens für die MSI-Identität kontaktiert und übergibt es wieder zu Ihrer app für die Verwendung mit Key Vault. Der wichtigste Teil dieses Workflows ist die Möglichkeit, die Ihre app in der MSI-token-Dienst authentifiziert &mdash; benötigen ein Geheimnis oder Zertifikat, die Sie in Ihrer Konfiguration verwalten müssen, nicht Ihre app verwendet einen geheimen Schlüssel, die Azure sicher in fügt die Umgebungsvariablen, wenn sie wird gestartet. Sie müssen nicht verwalten oder speichern Sie diesen geheimen Wert an eine beliebige Stelle. "Nothing" außerhalb Ihrer app kann auf dieses Geheimnis oder den MSI-Sicherheitstoken-Dienstendpunkt zugreifen.

MSI-Datei auch Ihre app in Azure Active Directory für Sie registriert, und die Registrierung wird gelöscht, wenn Sie die MSI-Datei zu deaktivieren oder löschen Sie die app.

MSI-Datei ist verfügbar in allen Editionen von Azure Active Directory, einschließlich der kostenlosen Edition, die in einem Azure-Abonnement enthalten. Verwenden sie in App Service verfügt über keine zusätzlichen Kosten und erfordert keine Konfiguration, und es kann aktiviert oder deaktiviert für eine app zu einem beliebigen Zeitpunkt.

> [!NOTE]
> MSI wird für Linux oder Container-Web-apps derzeit nicht unterstützt.

Die MSI-Aktivierung erfordert nur einen einzelnen Azure-CLI-Befehl ohne Konfiguration. Wir tun dies Einheit 5 Wenn wir eine App Service-app einrichten und in Azure bereitstellen. Davor werden jedoch wir unseren Erkenntnissen der MSI-Datei zum Schreiben von Code für die app angewendet.