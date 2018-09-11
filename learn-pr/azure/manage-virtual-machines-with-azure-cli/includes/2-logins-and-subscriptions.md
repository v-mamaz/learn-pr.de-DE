Before we start, let's review the syntax for the Azure CLI tool. If you've taken the **Control Azure services with the Azure CLI** module, then you know that Azure CLI commands take the form of:

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

The `[command]` identifies the specific area of Azure you want to control. For example, you can manage subscription information with the `account` command, or SQL databases with the `sql` command. The `[subcommand]` and `[--parameters]` are then dependent upon the command you're working with. 

You can view a list of commands, subcommands, and parameters by typing in a partial command. For example, typing `az` at the command line will give you the top-level help screen, and typing `az vm` will give you all the subcommands for virtual machines. This approach can be a great way to explore the Azure CLI tool.

> [!NOTE]
> We will be using browser-hosted Azure Cloud Shell to work with the Azure CLI. If you prefer to work from your local machine, all of the commands we cover can also be executed from the command line by [installing the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest). We covered this task in the **Control Azure services with the Azure CLI** module.

## Login to Azure

Normally, the first thing you'll do when working with the Azure CLI is to sign in to your Azure account. This is done with the `az login` command. This command will launch a browser window and allow you to select the Microsoft account you want to use. Since we are using the Azure Sandbox, this step is unnecessary, instead you will need to activate the Azure Sandbox.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## Working with subscriptions

In this module, we will work in a temporary subscription, but you will normally use a subscription from your own account. If you have more than one subscription, you can get a clearly formatted list of subscriptions using the `az account list --output table` statement.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Notice that the command also identifies the _default_ subscription where all your commands will apply. If you would prefer to work in a different subscription, you can use the `az account set --subscription "[name]"` command. For example, we could set our current subscription to be `Visual Studio Enterprise` from the above list through the following command:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```