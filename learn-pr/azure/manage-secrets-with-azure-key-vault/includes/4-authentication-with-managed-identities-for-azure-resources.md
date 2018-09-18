Azure Key Vault verwendet **Azure Active Directory** zum Authentifizieren von Benutzern und Anwendungen, die versuchen, auf einen Tresor zuzugreifen. Um unserer Webanwendung Zugriff auf den Tresor zu gewähren, müssen wir unsere App zunächst bei Azure Active Directory registrieren. Bei der Registrierung wird eine Identität für die App erstellt. Sobald eine Identität vorliegt, können ihr Tresorberechtigungen zugewiesen werden.

Anwendungen und Benutzer authentifizieren sich bei Key Vault mit einem Azure Active Directory-Authentifizierungstoken. Um ein Token von Azure Active Directory zu beziehen, ist ein Geheimnis oder Zertifikat erforderlich, da jeder mit einem Token die Anwendungsidentität verwenden kann, um auf alle Geheimnisse im Tresor zuzugreifen.

Unsere Anwendungsgeheimnisse sind im Tresor sicher, aber wir benötigen trotzdem noch ein Geheimnis oder Zertifikat außerhalb des Tresors, um darauf zugreifen zu können! Dieses Problem wird *Bootstrapping* genannt, wofür Azure allerdings eine Lösung hat.

## <a name="managed-identities-for-azure-resources"></a>Verwaltete Identitäten für Azure-Ressourcen

Verwaltete Identitäten für Azure sind ein Azure-Feature, mit dem Ihre App auf Key Vault und andere Azure-Dienste zugreifen kann, ohne selbst ein Geheimnis außerhalb des Tresors verwalten zu müssen. Das Verwenden einer verwalteten Identität ist eine einfache und sichere Möglichkeit zur Nutzung von Key Vault in Ihrer Web-App.

Wenn Sie die verwaltete Identität für Ihre Web-App aktivieren, aktiviert Azure speziell für Ihre Anwendung einen eigenständigen REST-Dienst, der Token vergibt. Ihre App fordert Token nicht direkt von Azure Active Directory, sondern von diesem Dienst an. Für den Zugriff auf den Dienst muss Ihre App ein Geheimnis verwenden. Dieses wird beim Start Ihrer App von App Service eingefügt und den Umgebungsvariablen zugewiesen. Sie müssen diesen Geheimniswert nirgendwo verwalten oder speichern. Außerhalb Ihrer App sind das Geheimnis und der Endpunkt des Tokendiensts der verwalteten Identität nicht zugänglich.

Verwaltete Identitäten für Azure-Ressourcen registrieren Ihre Anwendung auch für Sie in Azure Active Directory und löschen die Registrierung, sobald Sie die Web-App löschen oder dessen verwaltete Identität deaktivieren.

Verwaltete Identitäten sind in allen Editionen von Azure Active Directory verfügbar, einschließlich der Free Edition, die in einem Azure-Abonnement enthalten ist. Ihre Verwendung in App Service ist kostenlos, erfordert keine Konfiguration und kann jederzeit in einer App aktiviert oder deaktiviert werden.

> [!NOTE]
> Verwaltete Identitäten für Azure-Ressourcen werden für Linux- oder Container-Web-Apps derzeit nicht unterstützt.

Für die Aktivierung einer verwalteten Identität für eine Web-App muss nur ein einziger Azure CLI-Befehl ohne Konfiguration ausgeführt werden. Diesen Schritt führen Sie später aus, wenn Sie eine App Service-App einrichten und in Azure bereitstellen. Vorher nutzen Sie jedoch Ihr Wissen über verwaltete Identitäten, um den Code für Ihre App zu schreiben.