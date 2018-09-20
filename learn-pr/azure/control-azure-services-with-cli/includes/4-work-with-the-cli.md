Mit der Azure CLI können Sie Befehle eingeben und diese sofort über die Befehlszeile ausführen. Beachten Sie, dass das Ziel bei der Softwareentwicklung darin besteht, neue Builds einer Web-App zum Testen bereitzustellen. Zunächst befassen Sie sich mit den Aufgaben, die mithilfe der Azure CLI erledigt werden können.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>Welche Azure-Ressourcen können unter Verwendung der Azure CLI verwaltet werden?

Mithilfe der Azure CLI können Sie nahezu alle Aspekte jeder Azure-Ressource steuern. Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory (Azure AD), Containern, maschinellem Lernen usw. arbeiten.

Befehle in der CLI sind in _Gruppen_ und _Untergruppen_ strukturiert. Jede Gruppe stellt einen von Azure bereitgestellten Dienst dar, und die Untergruppen unterteilen Befehle für diese Dienste in logische Gruppierungen. Beispielsweise enthält die Gruppe `storage` Untergruppen wie **account**, **blob**, **storage** und **queue**.

Wie können die benötigten Befehle ermittelt werden? Eine Möglichkeit ist die Verwendung von `az find`. Wenn Sie etwa nach Befehlen im Zusammenhang mit der Verwaltung eines Speicherblobs suchen möchten, können Sie hierzu den folgenden Befehl verwenden:

```azurecli
az find -q blob
```

Wenn Sie bereits den Namen des Befehls kennen, erhalten Sie mit dem `--help`-Argument ausführliche Informationen zu diesem Befehl. Im Fall einer Befehlsgruppe wird eine Liste der verfügbaren Unterbefehle angezeigt. Im Speicherbeispiel können Sie folgendermaßen eine Liste der Untergruppen und Befehle zum Verwalten des Blobspeichers abrufen:

```azurecli
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Erstellen einer Azure-Ressource

Beim Erstellen einer neuen Azure-Ressource werden typischerweise drei Schritte durchlaufen: Verbindungsherstellung mit Ihrem Azure-Abonnement, Erstellung der Ressource und Überprüfung der erfolgreichen Erstellung. Die folgende Abbildung zeigt eine allgemeine Prozessübersicht.

![Illustration zur Erstellung einer Azure-Ressource mithilfe der Befehlszeilenschnittstelle.](../media/4-create-resources-overview.png)

Jeder Schritt entspricht einem anderen Azure CLI-Befehl.

### <a name="connect"></a>Verbinden

Da Sie mit einer lokalen Installation der Azure CLI arbeiten, müssen Sie sich zunächst mithilfe des Azure CLI-Befehls **login** authentifizieren, um Azure-Befehle ausführen zu können.

```azurecli
az login
```

Die Azure CLI verwendet typischerweise Ihren Standardbrowser, um die Seite für die Azure-Anmeldung zu öffnen. Falls dies nicht funktioniert, folgen Sie den Befehlszeilenanweisungen, und geben Sie unter [https://aka.ms/devicelogin](https://aka.ms/devicelogin) einen Autorisierungscode ein.

Nach der erfolgreichen Anmeldung wird eine Verbindung mit Ihrem Azure-Abonnement hergestellt.

### <a name="create"></a>Erstellen

Häufig müssen Sie eine neue Ressourcengruppe erstellen, bevor Sie einen neuen Azure-Dienst erstellen. Deshalb verwenden wir Ressourcengruppen als Beispiel dafür, wie Azure-Ressourcen über die CLI erstellt werden.

Mit dem Azure CLI-Befehl **group create** wird eine Ressourcengruppe erstellt. Sie müssen einen Namen und einen Standort angeben. Der Name muss innerhalb Ihres Abonnements eindeutig sein. Der Standort bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden. Sie verwenden Zeichenfolgen wie „West US“, „North Europe“ oder „West India“, um den Standort anzugeben. Alternativ können Sie aus einem Wort bestehende Äquivalente eingeben, z.B. „westus“, „northeurope“ oder „westindia“. Die grundlegende Syntax lautet wie folgt:

```azurecli
az group create --name <name> --location <location>
```

> [!IMPORTANT]
> Wenn Sie die kostenlose Azure-Sandbox nutzen, müssen Sie keine Ressourcengruppe erstellen. Stattdessen verwenden Sie eine vorab erstellte Ressourcengruppe.

### <a name="verify"></a>Überprüfen

Für viele Azure-Ressourcen stellt die Azure CLI einen Unterbefehl **list** bereit, mit dem Ressourcendetails angezeigt werden können. Beispielsweise können Sie mit dem Azure CLI-Befehl **group list** Ihre Azure-Ressourcengruppen auflisten. So können wir hier überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde:

```azurecli
az group list
```

Um eine kompaktere Ansicht zu erhalten, können Sie die Ausgabe als einfache Tabelle formatieren:

```azurecli
az group list --output table
```
