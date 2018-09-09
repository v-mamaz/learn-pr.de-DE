You've discovered that spikes in traffic can overwhelm our middle-tier. To deal with this, you've decided to add a queue between the front-end and the middle tier in your article-upload application.

The first step in creating a queue is to create the Azure Storage Account that will store our data.

## Create a Storage Account with the Azure CLI

To start with, let's create an Azure Resource Group to hold our storage account.

1. In the Cloud shell on the right, select Bash if you are given a choice.

1. Use the `az group create` Azure CLI command to create a new resource group. Give it the name **ExerciseResources** and place it into a location near you. 
    - The example below uses "eastus" as the location.

    ```azurecli
    az group create -n ExerciseResources --location eastus
    ```
        
1. Next, use the `az storage account create` command to create the actual Storage Account. You'll need to supply several parameters:

| Parameter | Value |
|-----------|-------|
| `--name`  | Sets the name. Remember that storage accounts use the name to generate a public URL - so it has to be unique. In addition, the account name must be between 3 and 24 characters, and be composed of numbers and lowercase letters only. We recommend you use the prefix **articles** with a random number suffix but you can use whatever you like. |
| `-g`        | Supplies the Resource Group, use **ExerciseResources** as the value. |
| `--kind`    | Sets the Storage Account type - use **StorageV2** to create a general-purpose V2 account. |
| `-l`        | Sets the location independent of the Resource Group owner. It's optional, but you can use it to place the queue in a different region than the Resource Group. |
| `--sku`     | Sets the account type, it defaults to **Standard_RAGRS**, which is overkill for this demonstration. Let's use **Standard_LRS** which means it's only locally redundant within the data center. |

Here's an example command line that uses the above parameters. Make sure to change the `--name` parameter to be something unique if you decide to copy/paste this command.

```azurecli
az storage account create --name <name> -g ExerciseResources --kind StorageV2 -l eastus --sku Standard_LRS
```