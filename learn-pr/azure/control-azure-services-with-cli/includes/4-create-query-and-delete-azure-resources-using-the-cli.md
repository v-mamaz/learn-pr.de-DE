## <a name="motivation"></a>Motivation
Mit der Azure CLI können Sie Befehle schreiben und diese sofort ausführen. Beachten Sie, dass das Ziel bei der Softwareentwicklung darin besteht, neue Builds einer Web-App zum Testen bereitzustellen. Hierzu wird im ersten Schritt eine Ressourcengruppe erstellt. Denken Sie daran, dass diese Ressourcen mithilfe einer lokalen Installation der Azure CLI erstellt werden sollen. 

In dieser Einheit erfahren Sie, wie Sie sich mithilfe der Azure CLI bei Ihrem Azure-Abonnement anmelden und eine neue Ressource erstellen.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>Welche Azure-Ressourcen können unter Verwendung der Azure CLI verwaltet werden?
Mithilfe der Azure CLI können Sie nahezu alle Aspekte jeder Azure-Ressource steuern. Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory (Azure AD), Containern, Machine Learning usw. arbeiten.

Befehle in der CLI sind in Gruppen und Untergruppen strukturiert. Jede Gruppe stellt einen von Azure bereitgestellten Dienst dar, und die Untergruppen unterteilen Befehle für diese Dienste in logische Gruppierungen. Beispielsweise enthält die Gruppe **storage** Untergruppen wie **account**, **blob**, **storage** und **queue**.

Wie können die benötigten Befehle ermittelt werden? Eine Möglichkeit ist die Verwendung von **az find**. Wenn Sie etwa nach Befehlen im Zusammenhang mit der Verwaltung eines **Speicherblobs** suchen möchten, verwenden Sie hierzu den folgenden Befehl:

```bash
az find -q blob
```

Wenn Sie den Namen des gewünschten Befehls bereits kennen, kann das Argument **--help** für diesen Befehl nützlicher sein. Sie erhalten ausführliche Informationen zum Befehl, und für eine Befehlsgruppe wird eine Liste der verfügbaren Unterbefehle angezeigt. In unserem Speicherbeispiel können Sie folgendermaßen eine Liste der Untergruppen und Befehle zum Verwalten von Blobspeicher abrufen:

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Erstellen einer Azure-Ressource
Beim Erstellen einer neuen Azure-Ressource werden typischerweise drei Schritte durchlaufen: Verbindungsherstellung mit Ihrem Azure-Abonnement, Erstellung der Ressource und Überprüfung der erfolgreichen Erstellung (siehe unten).

![Schritte zum Erstellen einer Ressource mit der Azure CLI](../media-drafts/4-create-resources-overview.png)

Jeder Schritt entspricht einem anderen Azure CLI-Befehl.

### <a name="connect"></a>Verbinden
Da Sie mit einer lokalen Installation der Azure CLI arbeiten, müssen Sie sich zunächst mithilfe des Azure CLI-Befehls **login** authentifizieren, um Azure-Befehle ausführen zu können. 

```bash
az login
```

Die Azure CLI verwendet typischerweise Ihren Standardbrowser, um die Seite für die Azure-Anmeldung zu öffnen. Falls dies nicht funktioniert, folgen Sie den Befehlszeilenanweisungen, und geben Sie unter [https://aka.ms/devicelogin](https://aka.ms/devicelogin) einen Autorisierungscode ein.

Nach der erfolgreichen Anmeldung wird eine Verbindung mit Ihrem Azure-Abonnement hergestellt. 

### <a name="create"></a>Erstellen
Häufig müssen Sie eine neue Ressourcengruppe erstellen, bevor Sie einen neuen Azure-Dienst erstellen. Deshalb verwenden wir Ressourcengruppen als Beispiel dafür, wie Azure-Ressourcen über die CLI erstellt werden.

Mit dem Azure CLI-Befehl **group create** wird eine Ressourcengruppe erstellt. Sie müssen einen Namen und einen Standort angeben. Der Name muss innerhalb Ihres Abonnements eindeutig sein. Der Standort bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden. Sie verwenden Zeichenfolgen wie „West US“, „North Europe“ oder „West India“, um den Standort anzugeben. Alternativ können Sie aus einem Wort bestehende Äquivalente eingeben, z.B. „westus“, „northeurope“ oder „westindia“. Die grundlegende Syntax lautet wie folgt:

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a>Überprüfen
Für viele Azure-Ressourcen stellt die Azure CLI einen Unterbefehl **list** bereit, mit dem Ressourcendetails angezeigt werden können. Beispielsweise können Sie mit dem Azure CLI-Befehl **group list** Ihre Azure-Ressourcengruppen auflisten. So können wir hier überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde:

```bash
az group list
```

Um eine kompaktere Ansicht zu erhalten, können Sie die Ausgabe als einfache Tabelle formatieren:

```bash
az group list --output table
```
