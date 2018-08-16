## <a name="creating-key-vaults-for-your-applications"></a>Erstellen von Key Vault-Instanzen für Ihre Anwendungen

Bewährte Methode ist jede Anwendung einen separaten Tresor für jede bereitstellungsumgebung gewähren, die Sie, z. B. Entwicklung, Test und Produktion verwenden. Es möglicherweise sinnvoll, die Geheimnisse in apps gemeinsam nutzen, aber die Auswirkungen von ein Angreifer erhält Lesezugriff auf einen Tresor erhöht wird, mit der Anzahl von Geheimnissen aus dem Tresor.

> [!TIP]
> Wenn Sie die gleichen Namen für den geheimen Schlüssel für verschiedene Umgebungen verwenden, ist die nur bestimmte-Konfiguration, die Änderungen in Ihrer app an die schlüsseltresor-URL an.

Erstellen eines Tresors erfordert keine anfängliche Konfiguration. Ihre Benutzer-ID wird automatisch erteilt sämtliche Berechtigungen der Verwaltung von Geheimnissen ein, und Sie beginnen, geheime Schlüssel sofort hinzufügen. Nachdem Sie einen Tresor verfügen, können hinzufügen und Verwalten von Geheimnissen aus jeder Azure Verwaltungsoberfläche, einschließlich der im Portal der Azure-Befehlszeilenschnittstelle und Azure PowerShell erfolgen. Wenn Sie Ihre Anwendung zur Verwendung des Tresors eingerichtet haben, müssen Sie die richtigen Berechtigungen zuweisen; Wir sehen, die in der nächsten Einheit.

## <a name="vault-authentication-and-permissions"></a>Tresor-Authentifizierung und Berechtigungen

Key Vault API verwendet Azure Active Directory zum Authentifizieren von Benutzern und Anwendungen. Schlüsseltresor-Zugriffsrichtlinien basieren auf *Aktionen*, und für einen gesamten Tresor angewendet werden. Z. B. eine Anwendung mit **erhalten** (Lesen geheime Werte), **Liste** (Auflisten der Namen aller Geheimnisse), und **festgelegt** (erstellen oder aktualisieren Sie geheime Werte) Berechtigungen für einen Tresor kann. Listen Sie alle geheimen Namen, um geheime Schlüssel zu erstellen, abrufen Sie und legen Sie alle geheime Werte in diesem Tresor.

*Alle* Aktionen für einen Tresor erfordern eine Authentifizierung und Autorisierung &mdash; besteht keine Möglichkeit, um jegliche Art von anonymen Zugriff zu gewähren.

> [!TIP]
> Wenn Vault-Zugriff für Entwickler und apps zu gewähren, erteilen Sie nur den Minimalsatz an Berechtigungen, die erforderlich sind. Einschränkungen der Berechtigungen helfen, vermeiden von Störungen, die durch Fehler im Code verursacht, und reduzieren die Auswirkungen von gestohlenen Anmeldeinformationen oder bösartigen Code in Ihrer app eingefügt.

Entwickler werden in der Regel brauchen nur noch **erhalten** und **Liste** Berechtigungen für eine Entwicklungsumgebung Tresor. Einen Lead oder leitender Entwickler benötigen Vollzugriff auf den Tresor ändern und Hinzufügen von Geheimnissen, die bei Bedarf. Vollzugriff auf die produktionsumgebung Tresore sind in der Regel für leitende Mitarbeiter reserviert.

Für apps in der Regel nur **erhalten** Berechtigungen sind erforderlich. Einige apps erfordern **Liste** je nachdem, wie die app implementiert wird. Die app, die wir in diesem Modul des Übung implementieren erfordert die Berechtigung zum Auflisten, aufgrund der Technik, die zum Lesen von Geheimnissen aus dem Tresor verwendet.

# <a name="exercise"></a>Übung

Wenn alle Probleme, die das Unternehmen mit Geheimnissen aus Anwendungen wurden die, hat Management Sie zum Erstellen einer kleinen Starter-app zum Festlegen von anderen Entwickler auf dem richtigen Weg gebeten. Die app muss sich um bewährte Methoden für die Verwaltung geheimer Schlüssel als einfach und sicher wie möglich zu veranschaulichen.

Um Sie zu starten. erstellen Sie einen Tresor und ein Geheimnis zu speichern.

### <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Erstellen Sie eine Ressourcengruppe namens `keyvault-exercise-group` für alle Ressourcen in dieser Übung. Am Ende dieses Modul werden wir diese Ressourcengruppe auf, um alles auf einmal zu bereinigen, werden gelöscht. Wir verwenden `eastus` als Speicherort für alles, was in dieser Übung.

Verwenden Sie die Cloud Shell-Terminal auf der rechten Seite, um den folgenden Azure CLI-Befehl ausführen. Dadurch wird die Ressourcengruppe in Ihrem Abonnement erstellt.

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### <a name="create-the-vault-and-store-the-secret-in-it"></a>Erstellen Sie den Tresor, und speichern sie den geheimen Schlüssel

Als Nächstes, wir erstellen den Tresor und geheimen Schlüssel in der sie speichern.

**Key Vault-Namen müssen global eindeutig sein, daher Sie einen eindeutigen Namen auswählen müssen**. Tresornamen müssen 3 bis 24 Zeichen lang sein und darf nur alphanumerische Zeichen und Bindestriche enthalten.

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

Wenn sie abgeschlossen ist, sehen Sie die JSON-Ausgabe, die den neuen Tresor beschreibt.

Fügen Sie nun den geheimen Schlüssel hinzu: geheimen Schlüssel erhält **SecretPassword** mit einem Wert von **Reindeer_flotilla**.

```azurecli
az keyvault secret set --name SecretPassword --value open_sesame --vault-name <your-unique-vault-name>
```

Notieren Sie sich den Namen des schlüsseltresors &mdash; Sie werde benötigen sie es später noch mal.

Schreiben wir den Code für die Anwendung kurz, aber zunächst müssen wir ein bisschen erfahren Sie, wie unsere app geht, einen Tresor zu authentifizieren.