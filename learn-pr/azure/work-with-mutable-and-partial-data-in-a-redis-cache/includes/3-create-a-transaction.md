Here, you'll create a simple transaction that inserts two data values into an Azure Redis Cache.

## Create an Azure Redis Cache

Let's start by creating an Azure Redis Cache in the Azure portal.

1. Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).

1. In the left navigation, select **Create a resource**.

1. Select **Databases**.

1. Locate and select **Redis Cache**. You can also optionally use the search bar to locate the template.

    ![Screenshot of the Azure portal showing the Create a resource blade with Redis Cache highlighted.](../media/4-click-redis-cache.png)

1. Enter a **DNS name**.

1. Select a **Subscription**.

1. Create a new **Resource Group**.

1. Select a **Location**.

1. Select **Basic C0** as your pricing tier. 

1. Check **Unblock port 6379 (not SSL encrypted)**.

1. Click **Create**.

## Create a C# console application

Next, create a C# console application, which will be used to insert data values into our Azure Redis Cache.

1. Open **Visual Studio**.

1. Select **File** > **New** > **Project**.

1. Select **Console App(.NET Core)**.

1. Enter an application name.

1. Click **OK**.

## Add the ServiceStack.Redis NuGet package

Now that we have our console application, we need to add the **ServiceStack.Redis** NuGet package. This will allow us to connect to the Redis Cache and issue commands in C#.

1. Right-click on your application’s project.

1. Select **Manage NuGet Packages...**.

1. On the Browse tab, search **ServiceStack.Redis**.

1. Install the **ServiceStack.Redis** package. This is the package that is published by **ServiceStack**.

## Get your Azure Redis Cache connection string

To connect to your Azure Redis Cache, you need a connection string that contains your password and URL. This connection string is unique to **ServiceStack.Redis** and is in the form of:

    [password]@[host name]:[port]

1. Go to the Azure portal.

1. Select **All resources** from the left navigation.

1. Locate and select your Azure Redis Cache.

1. In the **Overview** blade, select **Show access keys...**.

1. Copy your **Primary** key and paste it into Visual Studio as a comment. We're going to use this in a bit.

1. Close the **Manage keys** blade.

1. Copy your **Host name** and paste it into Visual Studio as a comment.

1. Create the following field.

    ```csharp
    static string redisConnectionString = "";
    ```

1. Paste in your connection string in the **redisConnectionString** field you just created and use 6379 as your port number. Remember, your connection string is in the form of: 

    [password]@[host name]:[port]

    For example, your connection string may look something like this:

    ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@mydns.redis.cache.windows.net:6379

## Insert two data values into your Azure Redis Cache

Finally, we're going to add data into your Azure Redis Cache.

1. Add the following using statement.

    ```csharp
    using ServiceStack.Redis;
    ```

1. Add the following snippet of code in your **Main** method.

    ```csharp
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create the transaction
        var transaction = redisClient.CreateTransaction();

        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        var transactionResult = transaction.Commit();

        if(transactionResult)
            Console.WriteLine("Transaction committed");
        else
            Console.WriteLine("Transaction failed to commit");
    }
    ```
1. Run the application and verify that the console says **Transaction committed**. 

## Verify your data

To finish off, let's verify that the data we added is in our Azure Redis Cache.

1. In the Azure portal, under the **Overview** blade, select **Console**. This will open a Redis console, which allows you to enter low-level Redis commands.

1. Type **get MyKey1**. Verify that the value returned is **MyValue1**.

1. Type **get MyKey2**. Verify that the value returned is **MyValue2**.

    ![Screenshot of the Azure Redis console showing the values of MyKey1 and MyKey2.](../media/4-redis-console.png)

