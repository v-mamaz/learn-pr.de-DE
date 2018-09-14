Bevor wir starten, sehen wir uns die Syntax für das Azure CLI-Tool an. Wenn Sie das Modul **Steuern von Azure-Diensten mit der Azure CLI** abgeschlossen haben, wissen Sie bereits, dass die Azure CLI-Befehle folgende Form aufweisen:

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

Der `[command]` identifiziert den Azure-Bereich, den Sie steuern möchten. Sie können z.B. Abonnementinformationen mit dem `account`-Befehl oder SQL-Datenbanken mit dem `sql`-Befehl verwalten. „`[subcommand]`“ und „`[--parameters]`“ richten sich dann nach dem Befehl, mit dem Sie arbeiten. 

Sie können eine Liste der Befehle, Unterbefehle und Parameter anzeigen, indem Sie einen Teilbefehl eingeben. Wenn Sie beispielsweise „`az`“ in der Befehlszeile eingeben, erhalten Sie einen Hilfebildschirm auf der obersten Ebene. Mit der Eingabe von „`az vm`“ erhalten Sie alle Unterbefehle für virtuelle Computer. Dieser Ansatz bietet eine hervorragende Möglichkeit, das Azure CLI-Tool zu erkunden.

> [!NOTE]
> Wir verwenden den im Browser gehosteten Azure Cloud Shell-Dienst, um mit der Azure CLI zu arbeiten. Wenn Sie lieber auf Ihrem lokalen Computer arbeiten, können Sie alle hier erläuterten Befehle auch über die Befehlszeile ausführen, indem Sie die [Azure CLI installieren](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest). Wir haben diese Aufgabe im behandelt die **Steuerelement Azure-Dienste mit der Azure-Befehlszeilenschnittstelle** Modul.

## <a name="login-to-azure"></a>Anmelden an Azure

Normalerweise ist zunächst, die Sie erledigen, bei der Arbeit mit der Azure-Befehlszeilenschnittstelle für die Anmeldung beim Azure-Konto ein. Dies erfolgt über den `az login`-Befehl. Dieser Befehl startet ein Browserfenster und ermöglicht Ihnen die Auswahl des Microsoft-Kontos, das Sie verwenden möchten. Da wir die Azure-Sandbox Verwenden dieser Schritt ist nicht erforderlich ist, müssen Sie stattdessen zum Aktivieren der Azure-Sandbox.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="working-with-subscriptions"></a>Arbeiten mit Abonnements

In diesem Modul wir in ein temporäres Abonnement arbeiten, aber ein Abonnement in der Regel von Ihrem eigenen Konto verwenden. Wenn Sie über mehrere Abonnements verfügen, können Sie mit der `az account list --output table`-Anweisung eine formatierte Liste der Abonnements abrufen.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Beachten Sie, dass der Befehl auch das _standardmäßige_ Abonnement identifiziert, in dem all Ihre Befehle gelten. Wenn Sie lieber mit einem anderen Abonnement arbeiten möchten, können Sie den `az account set --subscription "[name]"`-Befehl verwenden. Sie können z.B. das aktuelle Abonnement mit dem folgenden Befehl auf „`Visual Studio Enterprise`“ aus der oben stehenden Liste festlegen:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```