Azure Key Vault verwendet **Azure Active Directory** zum Authentifizieren von Benutzern und Anwendungen, die versuchen, auf einen Tresor zuzugreifen. Um unserer Webanwendung Zugriff auf den Tresor zu gewähren, müssen wir unsere App zunächst bei Azure Active Directory registrieren. Bei der Registrierung wird eine Identität für die App erstellt. Sobald eine Identität vorliegt, können ihr Tresorberechtigungen zugewiesen werden.

Anwendungen und Benutzer authentifizieren sich bei Key Vault mit einem Azure Active Directory-Authentifizierungstoken. Um ein Token von Azure Active Directory zu beziehen, ist ein Geheimnis oder Zertifikat erforderlich, da jeder mit einem Token die Anwendungsidentität verwenden kann, um auf alle Geheimnisse im Tresor zuzugreifen.

Unsere Anwendungsgeheimnisse sind im Tresor sicher, aber wir benötigen trotzdem noch ein Geheimnis oder Zertifikat außerhalb des Tresors, um darauf zugreifen zu können! Dieses Problem wird *Bootstrapping* genannt, wofür Azure allerdings eine Lösung hat.

## <a name="managed-identities-for-azure-resources"></a>Verwaltete Identitäten für Azure-Ressourcen

Verwaltete Identitäten für Azure-Ressourcen ist ein Azure-Feature, mit denen Ihre app Key Vault und andere Azure-Dienste zugreifen, ohne selbst einen einzelnen geheimen Schlüssel außerhalb des Tresors verwalten zu müssen. Mithilfe einer verwalteten Identität ist eine einfache und sichere Möglichkeit zu Key Vault aus Ihrer Web-app nutzen.

Wenn Sie verwaltete Identität für Ihre Web-app aktivieren, aktiviert Azure einen separaten-Token-granting-REST-Dienst speziell für die Verwendung von Ihrer app. Ihre App fordert Token nicht direkt von Azure Active Directory, sondern von diesem Dienst an. Für den Zugriff auf den Dienst muss Ihre App ein Geheimnis verwenden. Dieses wird beim Start Ihrer App von App Service eingefügt und den Umgebungsvariablen zugewiesen. Müssen Sie nicht zum Verwalten oder speichern diese geheimniswert an einer beliebigen Stelle, und nichts außerhalb Ihrer app kann auf dieses Geheimnis oder die verwaltete Identität Sicherheitstoken-Dienstendpunkt zugreifen.

Verwaltete Identitäten für Azure-Ressourcen auch Ihrer app in Azure Active Directory registriert sich für Sie und die Registrierung wird gelöscht, wenn Sie die Web-app zu löschen oder deaktivieren die zugehörige verwaltete Identität.

Verwaltete Identitäten sind verfügbar in allen Editionen von Azure Active Directory, einschließlich der kostenlosen Edition, die in einem Azure-Abonnement enthalten. Seine Verwendung in App Service ist kostenlos, erfordert keine Konfiguration und kann jederzeit in einer App aktiviert oder deaktiviert werden.

> [!NOTE]
> Verwaltete Identitäten für Azure-Ressourcen wird derzeit nicht für Linux oder Container-Web-apps unterstützt.

Aktivieren eine verwaltete Identität für eine Web-app erfordert nur einen einzelnen Azure-CLI-Befehl ohne Konfiguration. Diesen Schritt führen Sie später aus, wenn Sie eine App Service-App einrichten und in Azure bereitstellen. Davor werden jedoch wir unsere Informationen von verwalteten Identitäten in den Code für unsere app schreiben anwenden.