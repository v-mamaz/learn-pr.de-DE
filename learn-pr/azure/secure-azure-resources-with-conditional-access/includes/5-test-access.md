In den vorherigen Übungen haben wir ein Verzeichnis, einen Benutzer, eine Gruppe und anschließend eine bedingte Zugriffsregel erstellt, sodass für den Zugriff auf das Azure-Portal Azure Multi-Factor Authentication erforderlich ist. Nun testen wir, ob wir auf unsere Ressourcen zugreifen können.

## <a name="test-access-to-resources"></a>Testen des Zugriffs auf Ressourcen

Da Sie wissen, dass Ihre Benutzer sich anmelden und über das MyApps-Portal auf all ihre SaaS-Anwendungen zugreifen werden, soll genau das getestet werden.

1. Öffnen Sie ein Browserfenster im InPrivate-Modus.

1. Navigieren Sie zu https://myapps.microsoft.com.

1. Melden Sie sich mit dem Benutzerkonto an, das in Einheit 3 erstellt wurde.

   * Beachten Sie, dass Sie ohne Multi-Factor Authentication am Portal angemeldet sind.

1. Navigieren Sie im gleichen Browserfenster zu https://portal.azure.com.

   * Beachten Sie, dass Sie zum Schützen Ihres Kontos weitere Informationen bereitstellen müssen. Diese Unterbrechung wird aufgrund der von uns erstellten Richtlinie für bedingten Zugriff von Azure Multi-Factor Authentication verursacht. An diesem Punkt können Sie die Arbeit beenden und das Browserfenster schließen.