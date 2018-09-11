The true power of the Microsoft Custom Vision Service is the ease with which developers can incorporate its intelligence into their own applications using the [Custom Vision Prediction API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814). In this unit, you will use Visual Studio Code to modify an app named Artwork to use the model you built and trained in previous exercises.

1. If Node.js isn't installed on your system, go to https://nodejs.org and install the latest LTS version for your operating system.

   > If you aren't sure whether Node.js is installed, open a command prompt or terminal window and type **node -v**. If you don't see a Node.js version number, then Node.js isn't installed. If a version of Node.js older than 6.0 is installed, we highly recommend that you download and install the latest version.

1. If Visual Studio Code isn't installed on your workstation, go to http://code.visualstudio.com and install it now.

1. Start Visual Studio Code and select **Open Folder...** from the **File** menu. In the ensuing dialog, select the "Client\Artworks" folder included in the module resources.

    ![Selecting the Artworks folder](../media/5-fe-select-folder.png)

1. Use the **View** > **Integrated Terminal** command to open an integrated terminal window in Visual Studio Code. Then execute the following command in the integrated terminal to load the packages required by the app:

	```
	npm install
	```

1. Return to the Artwork project in the Custom Vision Service portal, click **Performance**, and then click **Make default** to make sure the latest iteration of the model is the default iteration.

    ![Specifying the default iteration](../media/5-portal-make-default.png)

1. Before you can run the app and use it to call the Custom Vision Service, it must be modified to include endpoint and authorization information. To that end, click **Prediction URL**.

    ![Viewing Prediction URL information](../media/5-portal-prediction-url.png)

1. The ensuing dialog lists two URLs: one for uploading images via URL, and another for uploading local images. Copy the Prediction API URL for image files to the clipboard.

    ![Copying the Prediction API URL](../media/5-copy-prediction-url.png)

1. Return to Visual Studio Code and click **predict.js** to open it in the code editor.

    ![Opening predict.js](../media/5-vs-predict-file.png)

1. Replace "PREDICTION_ENDPOINT" in line 3 with the URL on the clipboard.

    ![Adding the Prediction API URL](../media/5-vs-prediction-endpoint.png)

1. Return to the Custom Vision Service portal and copy the Prediction API key to the clipboard.

    ![Copying the Prediction API key](../media/5-copy-prediction-key.png)

1. Return to Visual Studio Code and replace "PREDICTION_KEY" in line 4 of **predict.js** with the API key on the clipboard.

    ![Adding the Prediction API key](../media/5-vs-prediction-key.png)

1. Scroll down in **predict.js** and examine the block of code that begins on line 34. This is the code that calls out to the Custom Vision Service using AJAX. Using the Custom Vision Prediction API is as easy as making a simple, authenticated POST to a REST endpoint.

    ![Making a call to the Prediction API](../media/5-vs-code-block.png)

1. Return to the integrated terminal in Visual Studio Code and execute the following command to start the app:

	```
	npm start
	```

1. Confirm that the Artworks app starts and displays a window like this one:

    ![The Artworks app](../media/5-app-startup.png)

Artworks is a cross-platform app written with Node.js and [Electron](https://electron.atom.io/). As such, it is equally capable of running on Windows, macOS, and Linux. In the next exercise, you will use it to classify images by the artists who painted them.