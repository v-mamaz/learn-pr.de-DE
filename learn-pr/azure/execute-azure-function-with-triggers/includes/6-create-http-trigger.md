In this unit, we're going to create an Azure function that accepts an HTTP request with a single string. The function returns a string back to the caller to represent success or failure.

## Create an HTTP trigger

Let's continue using our existing Azure Functions application and add an HTTP trigger.

1. Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).

1. Point to **Functions** and select the plus (+) icon.

1. Select **HTTP trigger**.

1. Select **C#** as the language.

1. Leave the **Name** set to the default value.

1. Set the **Authorization level** to **Anonymous**.

1. Select **Create**.

1. Take a quick look at the auto-generated code to get an idea about what's going on. The *req* parameter represents the incoming request and contains a *name* parameter. We check to see if *name* has a value. If it does, we return a greeting. Otherwise, we return an error message.

## Get your function URL

Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.

1. Select your HTTP trigger to open the code screen.

1. To the right of **Run**, select **Get function URL**.

1. Select **Copy**.

1. Select **Run** to start your function.

## Issue a GET request to your HTTP trigger

We now have our function URL copied to our clipboard. Let's issue a GET request to see if we get a response.

1. Open a new tab in your web browser.

1. Paste the URL into the address bar.

1. Add a query string parameter called *name* with your name for example `.../api/HttpTriggerCSharp1?name=Jesse`

1. Select ENTER to submit the request.

## Clean up
<!---TODO: Update for sandbox?--->

To ensure that you aren't charged for this function, select **Pause** above the log window.
