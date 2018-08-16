## <a name="motivation"></a>Motivation
Der Azure-Befehlszeilenschnittstelle können Sie die Befehle schreiben, und führen Sie sie. Denken Sie daran, dass das Ziel im Software Development Beispiel besteht darin, neue Builds zum Testen einer Web-app bereitstellen. Der erste Schritt ist die Erstellung eine Ressourcengruppe. Denken Sie daran, dass das Ziel hierbei ist, um diese Ressourcen, die mit einer lokalen Installation der Azure-Befehlszeilenschnittstelle zu erstellen. 

Diese Einheit erfahren Sie, wie Sie mit der Azure-CLI melden Sie sich bei Ihrem Azure-Abonnement, und Erstellen einer neuen Ressource.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>Welche Azure-Ressourcen können mithilfe der Azure CLI verwaltet werden?
Der Azure-Befehlszeilenschnittstelle können Sie fast jeden Aspekt aller Azure-Ressourcen zu steuern. Sie können mit Ressourcengruppen, Speicher, virtuelle Computer, Azure Active Directory, Container, Machine Learning und So weiter arbeiten.

Befehle in der CLI sind in Gruppen und Untergruppen aufgebaut. Jede Gruppe stellt einen von Azure bereitgestellten Dienst dar, und die Untergruppen unterteilen Befehle für diese Dienste in logische Gruppierungen. Z. B. die **Storage** Gruppe enthält, einschließlich Untergruppen **Konto**, **Blob**, **Storage**, und **Warteschlange**.

Also wie finden Sie die bestimmte Befehle, die Sie benötigen? Eine Möglichkeit ist die Verwendung **az Find**. Angenommen, Sie suchen, Befehle, mit denen Sie einen Speicher verwalten möchten **Blob**, würden Sie die folgenden Find-Befehl verwenden:

```bash
az find -q blob
```

Wenn Sie bereits den Namen des Befehls sollen wissen, die **– Hilfe** Argument für diesen Befehl kann nützlicher sein. Sie erhalten ausführliche Informationen zum Befehl "", und klicken Sie für eine Befehlsgruppe, die eine Liste der verfügbaren Unterbefehle. Mit unserem Beispiel Speicher also hier, wie Sie eine Liste mit den Untergruppen und Befehle zum Verwalten von BLOB-Speicher abrufen können

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Vorgehensweise: erstellen eine Azure-Ressource
Wenn Sie eine neue Azure-Ressource zu erstellen, in der Regel drei Schritte sind: eine Verbindung mit Ihrem Azure-Abonnement herstellen, erstellen Sie die Ressource, und stellen Sie sicher, dass die Erstellung erfolgreich (siehe unten) wurde.

![Schritte zum Erstellen einer Ressource, die mithilfe der Azure CLI](../images/create-resources-overview.png)

Jeder Schritt entspricht zu einem anderen Azure-CLI-Befehl.

### <a name="connect"></a>Verbinden
Da Sie mit einer lokalen Installation der Azure-Befehlszeilenschnittstelle verwenden, müssen Sie authentifizieren, bevor Sie Azure-Befehle ausführen können, mithilfe der Azure-Befehlszeilenschnittstelle **Anmeldung** Befehl. 

```bash
az login
```

Der Azure-Befehlszeilenschnittstelle startet den Standardbrowser zum Öffnen von Azure in der Regel Anmeldeseite. Wenn dies nicht funktioniert, befolgen Sie die Anweisungen über die Befehlszeile, und geben Sie einen Autorisierungscode an [ https://aka.ms/devicelogin ](https://aka.ms/devicelogin).

Nach ein erfolgreicher Anmeldung werden Sie mit Ihrem Azure-Abonnement verbunden sein. 

### <a name="create"></a>Erstellen
Häufig müssen Sie eine neue Ressourcengruppe zu erstellen, bevor Sie einen neuen Dienst erstellen, deshalb Ressourcengruppen als Beispiel wir verwenden veranschaulichen, wie Sie Azure-Ressourcen über die Befehlszeilenschnittstelle erstellen.

Der Azure-Befehlszeilenschnittstelle **Gruppe erstellen** Befehl erstellt eine Ressourcengruppe aus. Sie müssen einen Namen und Speicherort angeben. Der Name muss innerhalb Ihres Abonnements eindeutig sein. Die Position bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden sollen. Sie verwenden Zeichenfolgen wie "USA, Westen", "Nordeuropa" und "Indien (Westen)", um den Speicherort anzugeben. Alternativ können Sie einzelne Wort-Entsprechungen, z. B. USA, Westen, Northeurope oder Westindia verwenden. Die Core-Syntax lautet:

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a>Überprüfen
Für viele Azure-Ressourcen, die Azure-Befehlszeilenschnittstelle bietet eine **Liste** Unterbefehl Ressourcendetails anzeigen. Z. B. der Azure-Befehlszeilenschnittstelle **Gruppenliste** Befehl Listet Ihre Azure-Ressourcengruppen. Dies ist hier hilfreich zu überprüfen, ob die Erstellung der Ressourcengruppe erfolgreich war:

```bash
az group list
```

Um eine präzisere Ansicht zu erhalten, können Sie die Ausgabe als eine einfache Tabelle formatieren:

```bash
az group list --output table
```
