## Creating Key Vaults for your applications

Good practice is to create a separate vault for each deployment environment of each of your applications, such as development, test, and production. It's possible to use vaults to share secrets across multiple apps, but the impact of an attacker gaining read access to a vault increases with the number of secrets in the vault.

> [!TIP]
> If you use the same names for secrets across different environments for an application, the only environment-specific configuration that has to change in your app is the vault URL.

Creating a vault requires no initial configuration. Your user identity is automatically granted the full set of secret management permissions and you can start adding secrets immediately. Once you have a vault, adding and managing secrets can be done from any Azure administrative interface, including the Azure portal, the Azure CLI, and Azure PowerShell. When you set up your application to use the vault, you'll need to assign the correct permissions to it; we'll see that in the next unit.

## Vault authentication and permissions

Azure Key Vault's API uses Azure Active Directory to authenticate users and applications. Vault access policies are based on *actions*, and are applied across an entire vault. For example, an application with **Get** (read secret values), **List** (list names of all secrets), and **Set** (create or update secret values) permissions to a vault is able to create secrets, list all secret names, and get and set all secret values in that vault.

*All* actions performed on a vault require authentication and authorization &mdash; there is no way to grant any kind of anonymous access.

> [!TIP]
> When granting vault access to developers and apps, grant only the minimum set of permissions needed. Permissions restrictions help avoid accidents caused by code bugs and reduce the impact of stolen credentials or malicious code injected into your app.

Developers will usually only need **Get** and **List** permissions to a development-environment vault. A lead or senior developer will need full permissions to the vault to change and add secrets when necessary. Full permissions to production-environment vaults are typically reserved for senior operations staff.

For apps, typically only **Get** permissions are required. Some apps may require **List** depending on the way the app is implemented. The app we'll implement in this module's exercise requires the **List** permission because of the technique it uses to read secrets from the vault.

## Exercise

Given all the trouble the company's been having with application secrets, management has asked you to create a small starter app to set the other developers on the right path. The app needs to demonstrate best practices for managing secrets as simply and securely as possible.

To start, you'll create a vault and store one secret.

### Create a resource group
<!---TODO: Update for sandbox?--->

Create a resource group called `keyvault-exercise-group` for all of the resources In this unit. At the end of this module, we'll be deleting this resource group to cleanup everything at once. We'll use `eastus` as the location for everything In this unit.

Use the Azure Cloud Shell terminal on the right to run the following Azure CLI command. This will create the resource group in your subscription.

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### Create the vault and store the secret in it

Next, we'll create the vault and store our secret in it.

**Key Vault names must be globally unique, so you'll need to pick a unique name**. Vault names must be 3-24 characters long and contain only alphanumeric characters and dashes.

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

When it finishes, you'll see JSON output describing the new vault.

Now add the secret: our secret will be named **SecretPassword** with a value of **reindeer_flotilla**.

```azurecli
az keyvault secret set --name SecretPassword --value reindeer_flotilla --vault-name <your-unique-vault-name>
```

Make a note of the vault name &mdash; you'll be needing it again soon.

We'll write the code for our application shortly, but first we need to learn a little bit about how our app is going to authenticate to a vault.