<span data-ttu-id="0f4e2-101">In dieser Übung erstellen Sie eine einfache, in Node.js gehostete AngularJS-Anwendung und verwenden Express für das Routing.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-101">In this unit, you're going to create a simple AngularJS application hosted in Node.js and use Express for routing.</span></span> <span data-ttu-id="0f4e2-102">Auf dem Back-End dient Ihnen MongoDB als Datenspeicher.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-102">On the back end, MongoDB will serve as your data store.</span></span> <span data-ttu-id="0f4e2-103">Die Anwendung ist eine Buchdatenbank, in der Sie Bücher auflisten, hinzufügen und löschen können.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-103">The application is a book database, where you will be able to list, add, and delete books.</span></span>

> [!Important]
> <span data-ttu-id="0f4e2-104">Dies ist eine einfache Anwendung.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-104">This is a simple application.</span></span> <span data-ttu-id="0f4e2-105">Sie dient zum Testen des neu installierten MEAN-Stapels.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-105">Its purpose is to test the newly installed MEAN stack.</span></span> <span data-ttu-id="0f4e2-106">Diese Anwendung ist weder ausreichend sicher noch bereit für die Produktion.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-106">This application is not sufficiently secure or ready for production use.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="0f4e2-107">Herstellen der Verbindung mit der VM</span><span class="sxs-lookup"><span data-stu-id="0f4e2-107">Connect to the VM</span></span>

<span data-ttu-id="0f4e2-108">Wenn die Verbindung mit Ihrer VM noch nicht besteht, müssen Sie den folgenden Befehl ausführen.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-108">If you aren't still connected to your VM, run the following command.</span></span> <span data-ttu-id="0f4e2-109">Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der zuvor erwähnten VM.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-109">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="create-the-back-end"></a><span data-ttu-id="0f4e2-110">Erstellen des Back-Ends</span><span class="sxs-lookup"><span data-stu-id="0f4e2-110">Create the back end</span></span>

1. <span data-ttu-id="0f4e2-111">Erstellen Sie mit dem folgenden Befehl eine Ordnerstruktur für die neue Beispielanwendung.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-111">Create a folder structure for your new sample application with the following command.</span></span>

    ```bash
    mkdir ~/Books
    mkdir ~/Books/app
    mkdir ~/Books/public
    ```

    <span data-ttu-id="0f4e2-112">Am Hauptstandort Ihres Administratorbenutzers haben Sie einen Ordner namens „Books“ erstellt, der die App Ihres Projekts und deren Abhängigkeiten enthält.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-112">In your admin user's home location, you created a folder called "Books" to contain your project's app and its dependencies.</span></span> <span data-ttu-id="0f4e2-113">In diesem Ordner haben Sie einen Ordner „app“ erstellt, der alle Ihre Anwendungsressourcen und Skripts enthält.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-113">Within that folder, you created an "app" folder to contain all your application resources and scripts.</span></span> <span data-ttu-id="0f4e2-114">Schließlich erstellen wir auch einen „public“-Ordner zum Speichern aller clientseitigen Dateien, die direkt auf entsprechende HTTP-Anforderungen hin bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-114">Finally, we will also create a "public" folder to hold all of the client-side files that will be served up directly to appropriate HTTP requests.</span></span>

1. <span data-ttu-id="0f4e2-115">Installieren Sie **Express** zur Verarbeitung des Routings Ihrer HTTP-Anforderungen, wobei entschieden wird, welche Inhalte an einen Benutzer Ihrer Webanwendung zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-115">Install **Express** to handle routing of your HTTP requests, to decide what content to return to a user of your web application.</span></span>

    <span data-ttu-id="0f4e2-116">Führen Sie den folgenden Befehl zum Hinzufügen von Express als Paket für Ihre zu verwendende Webanwendung aus.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-116">Run the following command to add Express as a package for your web application to use.</span></span>

      ```bash
      npm install express
      ```

1. <span data-ttu-id="0f4e2-117">Installieren Sie **Mongoose** zur Unterstützung des Weiterleitens Ihrer Buchdaten zwischen MongoDB und dem HTTP-Anforderungsrouting.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-117">Install **Mongoose** to help relay your book data between MongoDB and the HTTP request routing.</span></span>

    <span data-ttu-id="0f4e2-118">Die Buchinformationen werden über REST-API-Anforderungen abgefragt.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-118">The book information will be queried via REST API requests.</span></span> <span data-ttu-id="0f4e2-119">Um die Übertragung von Daten in MongoDB und heraus an unsere API zu vereinfachen, verwenden wir Mongoose.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-119">To simplify the transfer of data in and out of MongoDB to our API, we will use Mongoose.</span></span> <span data-ttu-id="0f4e2-120">Mongoose ist ein schemabasiertes System für die Modellierung von Daten.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-120">Mongoose is a schema-based system for modeling data.</span></span> <span data-ttu-id="0f4e2-121">Wir werden es in unserer Beispielanwendung verwenden, um unsere Datenmodelle über die verschiedenen GET-, POST- und DELETE-HTTP-Anforderungen hinweg konsistent zu halten.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-121">We will be using it in our sample application to keep our data models consistent through the various GET, POST, and DELETE HTTP requests.</span></span>

    <span data-ttu-id="0f4e2-122">Führen Sie den folgenden Befehl zum Hinzufügen von Mongoose als Paket für Ihre zu verwendende Webanwendung aus.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-122">Run the following command to add Mongoose as a package for your web application to use.</span></span>

      ```bash
      npm install mongoose
      ```

1. <span data-ttu-id="0f4e2-123">Installieren Sie **body-parser**, um JSON-Anforderungsdaten für die Verwendung in unserem Express-Routing vorzuverarbeiten.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-123">Install **body-parser** to pre-process JSON request data for use in our Express routing.</span></span>

    <span data-ttu-id="0f4e2-124">Auf dem Back-End dient `body-parser` als Middleware zwischen Node.js und Express zum Analysieren der eingehenden JSON-Anforderungsdaten.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-124">On the back end, `body-parser` will serve as a middleware between Node.js and Express for parsing incoming JSON request data.</span></span>

    <span data-ttu-id="0f4e2-125">Führen Sie den folgenden Befehl zum Hinzufügen von `body-parser` als Paket für Ihre zu verwendende Webanwendung aus.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-125">Run the following command to add `body-parser` as a package for your web application to use.</span></span>

      ```bash
      npm install body-parser
      ```

    > [!TIP]
    > <span data-ttu-id="0f4e2-126">Wenn Sie mehrere npm-Pakete installieren, können Sie auch alle in einen einzigen Befehl wie diesen einschließen.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-126">When installing multiple npm packages, you can also include them all in a single command such as this.</span></span>
    > ```bash
    > npm install express mongoose body-parser
    > ```

1. <span data-ttu-id="0f4e2-127">Erstellen Sie das Datenmodell-Back-End für Ihre Bücherwebanwendung mithilfe von Mongoose.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-127">Create the data model back end for your books web application using Mongoose.</span></span>

    1. <span data-ttu-id="0f4e2-128">Erstellen Sie im **app**-Ordner Ihres **Books**-Anwendungsordners eine neue JavaScript-Datei namens **model.js**, die das Mongoose-basierte Datenmodell Ihrer Bücher enthält.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-128">In the **app** folder within your **Books** application folder, create a new JavaScript file called **model.js** to contain your book's Mongoose-based data model.</span></span>

        ```bash
        nano ~/Books/app/model.js
        ```

    1. <span data-ttu-id="0f4e2-129">Fügen Sie zum Erstellen unseres Buchschemas mithilfe von Mongoose den folgenden Code in diese neue Datei ein.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-129">Paste the following code into this new file to create our book schema using Mongoose.</span></span>

        ```javascript
        var mongoose = require('mongoose');
        var dbHost = 'mongodb://localhost:27017/Books';
        mongoose.connect(dbHost,  { useNewUrlParser: true } );
        mongoose.connection;
        mongoose.set('debug', true);
        var bookSchema = mongoose.Schema( {
            name: String,
            isbn: {type: String, index: true},
            author: String,
            pages: Number
        });
        var Book = mongoose.model('Book', bookSchema);
        module.exports = Book // mongoose.model('Book', bookSchema);
        ```

        > [!TIP]
        > <span data-ttu-id="0f4e2-130">Drücken Sie zum Speichern der aktuellen Datei in **nano** **STRG**+**O**.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-130">To save the current file in **nano**, you need to press **Ctrl**+**O**.</span></span> <span data-ttu-id="0f4e2-131">Drücken Sie zum Beenden von **nano** **STRG**+**X**.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-131">To exit **nano**, you need to press **Ctrl**+**X**.</span></span>

        <span data-ttu-id="0f4e2-132">Dieser Code stellt eine Verbindung mit einer Datenbank namens „Books“ auf dem MongoDB-Server des lokalen virtuellen Computers her.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-132">This code is connecting to a database called "Books" on the local VM's MongoDB server.</span></span> <span data-ttu-id="0f4e2-133">Er erstellt dann ein Dokument namens „Book“ mit dem von der `bookSchema`-Variablen definierten Schema.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-133">It then creates a database document called "Book" with the schema defined by the `bookSchema` variable.</span></span>

1. <span data-ttu-id="0f4e2-134">Erstellen Sie die Express-Routen für die Anwendung zur Verarbeitung der verschiedenen HTTP-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-134">Create the Express routes for the application to handle the various HTTP requests.</span></span>

    1. <span data-ttu-id="0f4e2-135">Erstellen Sie im **app**-Ordner eine neue JavaScript-Datei namens **routes.js**.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-135">Within the **app** folder, create a new JavaScript file called **routes.js**.</span></span>

        ```bash
        nano ~/Books/app/routes.js
        ```

    1. <span data-ttu-id="0f4e2-136">Fügen Sie den folgenden Code in diese neue Datei ein, um die Routen mit Express herzustellen.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-136">Paste the following code into this new file to establish the routes using Express.</span></span>

        ```javascript
        var path = require('path');
        var Book = require('./model');
        var routes = function(app) {
            app.get('/book', function(req, res) {
                Book.find({}, function(err, result) {
                    if ( err ) throw err;
                    res.json(result);
                });
            });
            app.post('/book', function(req, res) {
                var book = new Book( {
                    name:req.body.name,
                    isbn:req.body.isbn,
                    author:req.body.author,
                    pages:req.body.pages
                });
                book.save(function(err, result) {
                    if ( err ) throw err;
                    res.json( {
                        message:"Successfully added book",
                        book:result
                    });
                });
            });
            app.delete("/book/:isbn", function(req, res) {
                Book.findOneAndRemove(req.query, function(err, result) {
                    if ( err ) throw err;
                    res.json( {
                        message: "Successfully deleted the book",
                        book: result
                    });
                });
            });
            app.get('*', function(req, res) {
                res.sendFile(path.join(__dirname + '/public', 'index.html'));
            });
        };
        module.exports = routes;
        ```

        <span data-ttu-id="0f4e2-137">Dieser Code erstellt vier Routen für die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-137">This code will create four routes for our application.</span></span> <span data-ttu-id="0f4e2-138">Die ersten drei geben an, was zu tun ist, wenn jemand eine API-GET-, POST- oder DELETE-Anforderung an die `/book`-Ressource sendet.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-138">The first three specify what to do when someone sends an API GET, POST, or DELETE request to the `/book` resource.</span></span> <span data-ttu-id="0f4e2-139">Die letzte ist eine alles abfangende Route, die die anfordernde Person zur Indexseite leitet.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-139">The last one is a catch-all route to send the requester to the index page.</span></span>

        <span data-ttu-id="0f4e2-140">Express kann HTTP-Antworten direkt an den Routenverarbeitungscode leiten oder statischen Inhalt aus Dateien bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-140">Express can serve up HTTP responses directly in the route handling code, or it can serve up static content from files.</span></span> <span data-ttu-id="0f4e2-141">In dieser Beispiel-Web-Anwendung findet beides statt.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-141">We are doing both in this sample web application.</span></span> <span data-ttu-id="0f4e2-142">Wir antworten mit JSON-Daten auf Buch-API-Anforderungen und mit HTML-Daten direkt aus der Datei „index.html“.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-142">We respond with JSON data for book API requests and with HTML data direct from the index.html file.</span></span>

1. <span data-ttu-id="0f4e2-143">Erstellen Sie eine **server.js**-Datei im **Books**-Ordner, um das Node.js-Hosting zu konfigurieren (mit den Express-Routen).</span><span class="sxs-lookup"><span data-stu-id="0f4e2-143">Create a **server.js** file in the **Books** folder to configure the Node.js hosting (using the Express routes).</span></span>

    1. <span data-ttu-id="0f4e2-144">Erstellen Sie zurück im Anwendungsstammordner **Books** eine neue JavaScript-Datei namens **server.js**.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-144">Back in the application root **Books** folder, create a new JavaScript file called **server.js**.</span></span>

        ```bash
        nano ~/Books/server.js
        ```

    1. <span data-ttu-id="0f4e2-145">Fügen Sie zum Konfigurieren Ihrer Webanwendung und Starten der Überwachung des HTTP-Standardports den folgenden Code in diese neue Datei ein.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-145">Paste the following code into this new file to configure your web application and start listening to the default HTTP port.</span></span>

        ```javascript
        var express = require('express');
        var bodyParser = require('body-parser');
        var app = express();
        app.use(express.static(__dirname + '/public'));
        app.use(bodyParser.json());
        require('./app/routes')(app);
        app.set('port', 80);
        app.listen(app.get('port'), function() {
            console.log('Server up: http://localhost:' + app.get('port'));
        });
        ```

        <span data-ttu-id="0f4e2-146">Dieser Code erstellt die Webanwendung selbst.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-146">This code creates the web application itself.</span></span> <span data-ttu-id="0f4e2-147">Er stellt statische Dateien aus einem Ordner mit dem Namen **public** (als Nächstes erstellt) bereit und verwendet die im vorherigen Schritt definierten Routen.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-147">It will serve static files from a folder named **public** (created next) and will use the routes defined in the previous step.</span></span>

1. <span data-ttu-id="0f4e2-148">Erstellen Sie die Front-End-HTML- und die clientseitige JavaScript-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-148">Create the front-end HTML and client-side JavaScript application.</span></span>

    1. <span data-ttu-id="0f4e2-149">Erstellen Sie im **public**-Inhaltsordner eine neue JavaScript-Datei namens **script.js**.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-149">Within the **public** content folder, create a new JavaScript file called **script.js**.</span></span>

        ```bash
        nano ~/Books/public/script.js
        ```

    1. <span data-ttu-id="0f4e2-150">Fügen Sie zum Konfigurieren Ihrer clientseitigen Webanwendung den folgenden Code zum Durchführen der Kommunikation mit dem Webserver in diese neue Datei ein.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-150">Paste the following code into this new file to configure your client-side web application to handle communicating with your web server.</span></span>

        ```javascript
        var app = angular.module('myApp', []);
        app.controller('myCtrl', function($scope, $http) {
            var getData = function() {
                return $http( {
                    method: 'GET',
                    url: '/book'
                }).then(function successCallback(response) {
                    $scope.books = response.data;
                }, function errorCallback(response) {
                    console.log('Error: ' + response);
                });
            };
            getData();
            $scope.del_book = function(book) {
                $http( {
                    method: 'DELETE',
                    url: '/book/:isbn',
                    params: {'isbn': book.isbn}
                }).then(function successCallback(response) {
                    console.log(response);
                    return getData();
                }, function errorCallback(response) {
                    console.log('Error: ' + response);
                });
            };
            $scope.add_book = function() {
                var body = '{ "name": "' + $scope.Name +
                '", "isbn": "' + $scope.Isbn +
                '", "author": "' + $scope.Author +
                '", "pages": "' + $scope.Pages + '" }';
                $http({
                    method: 'POST',
                    url: '/book',
                    data: body
                }).then(function successCallback(response) {
                    console.log(response);
                    return getData();
                }, function errorCallback(response) {
                    console.log('Error: ' + response);
                });
            };
        });
        ```

        <span data-ttu-id="0f4e2-151">Dieser clientseitige AngularJS-Code erstellt eine neue angular-Anwendung `myApp` mit einem Controller `myCtrl`.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-151">This client-side AngularJS code creates a new angular application `myApp` containing one controller `myCtrl`.</span></span> <span data-ttu-id="0f4e2-152">Wenn die Anwendung im Browser des Betrachters ausgeführt wird, wird eine HTTP-GET-Anforderung zum Abrufen der Bücherliste in der Datenbank ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-152">When the application is run in the viewer's browser, it will issue an HTTP GET request to retrieve the list of books in the database.</span></span>

    1. <span data-ttu-id="0f4e2-153">Erstellen Sie im **public**-Inhaltsordner auch eine neue HTML-Datei namens **index.html**.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-153">Also within the **public** content folder, create a new HTML file called **index.html**.</span></span>

        ```bash
        nano ~/Books/public/index.html
        ```

    1. <span data-ttu-id="0f4e2-154">Fügen Sie das folgende Markup in diese neue Datei ein, um die HTML-Benutzeroberfläche Ihrer Webanwendung einzurichten.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-154">Paste the following markup into this new file to set up your web application's HTML user interface.</span></span>

        ```html
        <!doctype html>
        <html ng-app="myApp" ng-controller="myCtrl">
        <head>
            <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
            <script src="script.js"></script>
        </head>
        <body>
            <div>
            <table>
                <tr>
                <td>Name:</td>
                <td><input type="text" ng-model="Name"></td>
                </tr>
                <tr>
                <td>Isbn:</td>
                <td><input type="text" ng-model="Isbn"></td>
                </tr>
                <tr>
                <td>Author:</td>
                <td><input type="text" ng-model="Author"></td>
                </tr>
                <tr>
                <td>Pages:</td>
                <td><input type="number" ng-model="Pages"></td>
                </tr>
            </table>
            <button ng-click="add_book()">Add</button>
            </div>
            <hr>
            <div>
            <table>
                <tr>
                <th>Name</th>
                <th>Isbn</th>
                <th>Author</th>
                <th>Pages</th>
                </tr>
                <tr ng-repeat="book in books">
                <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
                <td>{{book.name}}</td>
                <td>{{book.isbn}}</td>
                <td>{{book.author}}</td>
                <td>{{book.pages}}</td>
                </tr>
            </table>
            </div>
        </body>
        </html>
        ```

        <span data-ttu-id="0f4e2-155">Dieser Code erstellt ein einfaches HTML-Formular mit vier Feldern zum Übermitteln von neuen Buchdaten und eine Tabelle zum Anzeigen aller Bücher, die bereits in der Datenbank gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-155">This code will create a simple HTML form with four fields to submit new book data and a table to display all the books already stored in the database.</span></span> <span data-ttu-id="0f4e2-156">Die verschiedenen `ng-`-HTML-Attribute verknüpfen den AngularJS-Code mit der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-156">The various `ng-` HTML attributes will wire up the AngularJS code to the UI.</span></span>

1. <span data-ttu-id="0f4e2-157">Testen Sie die vollständige Bücherwebanwendung.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-157">Test the full books web application.</span></span>

    1. <span data-ttu-id="0f4e2-158">Starten Sie die Anwendung mit dem folgenden Befehl mit Node.js.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-158">Start the application with Node.js with the following command.</span></span>

        ```bash
        sudo node ~/Books/server.js
        ```

        <span data-ttu-id="0f4e2-159">Dadurch wird das Back-End der Anwendung gestartet, das dann Port 80 auf eingehende HTTP-Anforderungen überwacht.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-159">This will start the back end of our application, which will then start listening on port 80 for incoming HTTP requests.</span></span>

    1. <span data-ttu-id="0f4e2-160">Testen Sie die Anwendungsfunktionalität.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-160">Test the application functionality.</span></span>

        <span data-ttu-id="0f4e2-161">Öffnen Sie Ihren bevorzugten Browser, und navigieren Sie zur öffentlichen IP-Adresse Ihrer Azure-VM als URL.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-161">Open your preferred browser, and navigate to the public IP address of your Azure VM as the URL.</span></span>

        ```bash
        http://<vm-public-ip>
        ```

        <span data-ttu-id="0f4e2-162">Wenn alles in Ordnung ist, sehen Sie etwa folgenden Bildschirm:</span><span class="sxs-lookup"><span data-stu-id="0f4e2-162">If everything is in order, you should see a screen similar to this:</span></span>

        <span data-ttu-id="0f4e2-163">Der folgende Screenshot zeigt die Benutzeroberfläche zum Übermitteln von Buchdetails zur Speicherung in der MongoDB-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-163">The following screenshot displays the user interface to submit book details for storage in the MongoDB database.</span></span>


        ![Screenshot eines Webbrowsers mit dem Dateneingabeformular zum Hinzufügen eines Buchs.](../media-draft/10-book-page.png)

    <span data-ttu-id="0f4e2-165">Sie sollten jetzt Bücher zum Speichern in der MongoDB-Datenbank übermitteln können.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-165">You should now be able to submit books to save to the MongoDB database.</span></span> <span data-ttu-id="0f4e2-166">Außerdem sehen Sie die vollständige Liste der aus der Datenbank geladenen Bücher.</span><span class="sxs-lookup"><span data-stu-id="0f4e2-166">As well, you can see the full list of books loaded from the database.</span></span>