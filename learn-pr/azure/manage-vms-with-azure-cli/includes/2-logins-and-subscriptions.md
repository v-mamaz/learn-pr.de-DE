Bevor wir beginnen, können die Syntax für das Azure-CLI-Tool zu überprüfen. Wenn Sie ergriffen haben, die **Steuerelement Azure-Dienste mit der Azure-Befehlszeilenschnittstelle** -Modul, dann wissen Sie, dass es sich bei Azure CLI-Befehle in Form einer erfolgen:

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

Die `[command]` identifiziert den bestimmten Bereich von Azure, die Sie steuern möchten. Sie können z. B. Abonnementinformationen mit verwalten die `account` Befehls oder einer SQL-Datenbanken mit der `sql` Befehl. Die `[subcommand]` und `[--parameters]` sind abhängig von den Befehl mit dem Sie arbeiten. 

Sie können eine Liste der Befehle, Unterbefehle und Parameter anzeigen, geben Sie in einem Teilbefehl. Geben z. B. `az` in der Befehlszeile erhalten Sie den Bildschirm Hilfe auf oberster Ebene, und geben `az vm` erhalten Sie alle die Unterbefehle für virtuelle Computer. Dieser Ansatz kann eine hervorragende Möglichkeit, untersuchen das CLI-Tool sein.

> [!NOTE]
> Wir werden im Browser gehostete Cloud Shell verwenden, um mit der Azure CLI zu arbeiten. Wenn Sie von Ihrem lokalen Computer arbeiten möchten, alle geht es um Befehle können auch ausgeführt werden über die Befehlszeile [Installieren der Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="log-into-azure"></a>Anmelden bei Azure

Das erste, was Sie tun, bei der Arbeit mit der Azure-Befehlszeilenschnittstelle ist die Anmeldung beim Azure-Konto. Dies erfolgt mit der `login` Befehl. Wenn Sie Cloud Shell verwenden, fallen in eine Schaltfläche, um sich bei Azure anmelden.

```azurecli
az login
```

Dieser Befehl startet ein Browserfenster und ermöglichen es Ihnen, das Microsoft-Konto auswählen, die, das Sie verwenden möchten.

## <a name="working-with-subscriptions"></a>Arbeiten mit Abonnements

In diesem Modul wir in ein temporäres Abonnement erstellt haben, als einen Playground arbeiten, aber ein Abonnement in der Regel von Ihrem eigenen Konto verwenden. Wenn Sie über mehrere Abonnements verfügen, erhalten Sie eine eindeutig formatierte Liste von Abonnements unter Verwendung der `az account list --output table` Anweisung.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Beachten Sie, die der Befehl auch identifiziert den _Standard_ Abonnement, in dem alle Ihre Befehle gelten. Wenn Sie in einem anderen Abonnement arbeiten lieber, können Sie mithilfe der `az account set --subscription "[name]"` Befehl. Beispielsweise konnte wir unsere aktuelle Abonnement sein festgelegt `Visual Studio Enterprise` in der obigen Liste durch den folgenden Befehl aus:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```