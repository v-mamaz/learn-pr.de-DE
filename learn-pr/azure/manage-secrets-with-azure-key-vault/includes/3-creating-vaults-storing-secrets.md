## <a name="creating-key-vaults-for-your-applications"></a>Erstellen von Key Vaults für Ihre Anwendungen

Es empfiehlt sich, für jede Bereitstellungsumgebung (Entwicklung, Test und Produktion) Ihrer verschiedenen Anwendungen einen separaten Tresor bereitzustellen. Es ist zwar möglich, Tresore zum plattformübergreifenden Freigeben von Geheimnissen zu verwenden, allerdings nehmen die Auswirkungen eines Angriffs, bei dem Lesezugriff auf einen Tresor erlangt wurde, mit der Anzahl der Geheimnisse im Tresor zu.

> [!TIP]
> Wenn Sie in verschiedenen Umgebungen einer Anwendung dieselben Namen für Geheimnisse verwenden, ist die Tresor-URL die einzige umgebungsspezifische Konfiguration, die in Ihrer Anwendung geändert werden muss.

Das Erstellen eines Tresors erfordert keine anfängliche Konfiguration. Ihrer Benutzeridentität werden automatisch alle Berechtigungen für die Verwaltung von Geheimnissen erteilt, und Sie können sofort mit dem Hinzufügen von Geheimnissen beginnen. Sobald Sie einen Tresor haben, können Sie Geheimnisse über jede Azure-Verwaltungsschnittstelle hinzufügen und verwalten, einschließlich Azure-Portal, Azure CLI und Azure PowerShell. Wenn Sie Ihre Anwendung für die Verwendung des Tresors einrichten, müssen Sie ihr die ordnungsgemäßen Berechtigungen zuweisen, womit wir uns in der nächsten Einheit beschäftigen.

## <a name="vault-authentication-and-permissions"></a>Tresorauthentifizierung und -berechtigungen

Die Azure Key Vault-API verwendet Azure Active Directory zum Authentifizieren von Benutzern und Anwendungen. Tresorzugriffsrichtlinien basieren auf *Aktionen* und gelten für einen gesamten Tresor. Beispiel: Eine Anwendung mit den Berechtigungen **Get (Abrufen)** (Werte von Geheimnissen lesen), **List (Auflisten)** (Namen aller Geheimnisse auflisten) und **Set (Festlegen)** (Werte von Geheimnissen erstellen oder aktualisieren) kann Geheimnisse erstellen, alle Namen von Geheimnissen auflisten und alle Werte von Geheimnissen in diesem Tresor abrufen und festlegen.

*Alle* Aktionen, die für einen Tresor erfolgen, erfordern eine Authentifizierung und Autorisierung. Ein anonymer Zugriff ist nicht möglich.

> [!TIP]
> Wenn Sie Entwicklern und Anwendungen Zugriff auf den Tresor gewähren, sollten Sie nur die erforderlichen Mindestberechtigungen gewähren. Berechtigungsbeschränkungen helfen, Unregelmäßigkeiten durch Codefehler zu vermeiden und die Auswirkungen von gestohlenen Anmeldeinformationen oder bösartigem Code in Ihrer Anwendung zu reduzieren.

Entwickler benötigen für einen Entwicklungsumgebungstresor normalerweise nur die Berechtigungen **Get** und **List**. Ein Chef- oder leitender Entwickler benötigt Vollzugriff auf den Tresor, um bei Bedarf Geheimnisse zu ändern und hinzuzufügen. Vollzugriffsberechtigungen für Tresore in Produktionsumgebungen sind in der Regel für leitende Mitarbeiter reserviert.

Für Apps sind in der Regel nur **Get**-Berechtigungen erforderlich. Einige Anwendungen können **List** erfordern, je nachdem, wie die App implementiert ist. Die App, die wir in der Übung dieses Moduls implementieren werden, benötigt die Berechtigung **List** aufgrund der Technik, mit der sie Geheimnisse aus dem Tresor liest.

## <a name="exercise"></a>Übung

Angesichts der ganzen Schwierigkeiten, die das Unternehmen mit Anwendungsgeheimnissen hatte, hat die Geschäftsleitung Sie gebeten, eine kleine Einstiegs-App zu erstellen, um die anderen Entwickler auf den richtigen Weg zu bringen. Die App muss bewährte Methoden veranschaulichen, wie Geheimnisse so einfach und sicher wie möglich verwaltet werden können.

Als Erstes erstellen Sie einen Tresor, in dem Sie ein Geheimnis speichern.

### <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe
<!---TODO: Update for sandbox?--->

Erstellen Sie für alle Ressourcen in dieser Einheit eine Ressourcengruppe namens `keyvault-exercise-group`. Am Ende dieses Moduls löschen wir diese Ressourcengruppe, um alles auf einmal zu bereinigen. Wir verwenden `eastus` als Speicherort für alles in dieser Einheit.

Verwenden Sie das Azure Cloud Shell-Terminalfenster auf der rechten Seite, um den folgenden Azure CLI-Befehl auszuführen. Dadurch wird die Ressourcengruppe in Ihrem Abonnement erstellt.

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### <a name="create-the-vault-and-store-the-secret-in-it"></a>Erstellen Sie den Tresor, und speichern sie das Geheimnis darin.

Als Nächstes erstellen wir den Tresor und speichern unser Geheimnis darin.

**Key Vault-Namen müssen global eindeutig sein. Daher Sie müssen einen eindeutigen Namen auswählen**. Tresornamen müssen 3-24 Zeichen lang sein und dürfen nur alphanumerische Zeichen und Bindestriche enthalten.

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

Nach Abschluss des Vorgangs sehen Sie die JSON-Ausgabe mit einer Beschreibung des neuen Tresors.

Fügen Sie nun das Geheimnis hinzu. Unser Geheimnis erhält den Namen **SecretPassword** mit dem Wert **Reindeer_flotilla**.

```azurecli
az keyvault secret set --name SecretPassword --value reindeer_flotilla --vault-name <your-unique-vault-name>
```

Notieren Sie sich den Tresornamen, da Sie ihn bald wieder benötigen.

Wir schreiben in Kürze den Code für unsere Anwendung. Aber zuerst müssen wir ein wenig darüber lernen, wie sich unsere App bei einem Tresor authentifiziert.