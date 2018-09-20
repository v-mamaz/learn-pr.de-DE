In dieser Übung erstellen Sie eine einfache, in Node.js gehostete AngularJS-Anwendung und verwenden Express für das Routing. Auf dem Back-End dient Ihnen MongoDB als Datenspeicher. Die Anwendung ist eine Buchdatenbank, in der Sie Bücher auflisten, hinzufügen und löschen können.

> [!Important]
> Dies ist eine einfache Anwendung. Sie dient zum Testen des neu installierten MEAN-Stapels. Diese Anwendung ist weder ausreichend sicher noch bereit für die Produktion.

## <a name="create-the-application"></a>Erstellen der Anwendung

Zuerst erstellen wir für Ihre Anwendung den Code, das Skript und die HTML-Dateien. Hierfür verwenden wir den Cloud Shell-Editor und kopieren die Dateien dann auf die VM.

1. Wenn die SSH-Verbindung mit Ihrer VM noch besteht, können Sie in Cloud Shell `exit` verwenden, um zum Cloud Shell-Dateisystem zurückzukehren.

    ```bash
    exit
    ```

1. Erstellen Sie die Ordner und Dateien für Ihre Anwendung, und öffnen Sie sie im Cloud Shell-Editor.

    ```bash
    cd ~
    mkdir Books
    mkdir Books/app
    mkdir Books/public
    touch Books/app/model.js
    touch Books/app/routes.js
    touch Books/server.js
    touch Books/public/script.js
    touch Books/public/index.html
    code Books
    ```

    Es wird ein Ordner mit dem Namen „Books“ für die App und die zugehörigen Abhängigkeiten Ihres Projekts erstellt. In diesem Ordner haben Sie einen Ordner „app“ erstellt, der alle Ihre Anwendungsressourcen und Skripts enthält. Schließlich erstellen wir auch einen „public“-Ordner zum Speichern aller clientseitigen Dateien, die direkt auf entsprechende HTTP-Anforderungen hin bereitgestellt werden.

## <a name="create-the-application"></a>Erstellen der Anwendung

1. Erstellen Sie das Mongoose-Datenmodell. Öffnen Sie im Editor die Datei `app/model.js`, und fügen Sie den folgenden Code ein.

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

    > [!IMPORTANT]
    > Achten Sie beim Einfügen oder Ändern von Code in einer Datei im Editor darauf, dass Sie anschließend speichern, indem Sie das Menü unter „...“ oder die Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux, <kbd>Cmd+S</kbd> unter macOS).

    Dieser Code stellt eine Verbindung mit einer Datenbank namens „Books“ auf dem MongoDB-Server des lokalen virtuellen Computers her. Er erstellt dann ein Datenbankdokument namens „Book“ mit dem von der `bookSchema`-Variablen definierten Schema.

2. Erstellen Sie die ExpressRoute-Verbindungen, mit denen die HTTP-Anforderungen behandelt werden. Öffnen Sie im Editor die Datei `app/routes.js`, und fügen Sie den folgenden Code ein.

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

    Dieser Code erstellt vier Routen für die Anwendung. Die ersten drei geben an, was zu tun ist, wenn jemand eine API-GET-, POST- oder DELETE-Anforderung an die `/book`-Ressource sendet. Die letzte ist eine alles abfangende Route, die die anfordernde Person zur Indexseite leitet.

    Express kann HTTP-Antworten direkt an den Routenverarbeitungscode leiten oder statischen Inhalt aus Dateien bereitstellen. In dieser Beispielwebanwendung wird beides durchgeführt. Wir antworten mit JSON-Daten auf Buch-API-Anforderungen und mit HTML-Daten direkt aus der Datei „index.html“.

3. Erstellen Sie den Express-Server, um die Anwendung zu hosten. Öffnen Sie im Editor die Datei `server.js`, und fügen Sie den folgenden Code ein:

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

    Mit diesem Code wird die eigentliche Webanwendung erstellt. Er stellt statische Dateien aus einem Ordner mit dem Namen **public** (wird als Nächstes erstellt) bereit und verwendet die im vorherigen Schritt definierten Routen.

4. Erstellen Sie die clientseitige JavaScript-Anwendung. Öffnen Sie die Datei `public/script.js` im Editor, und fügen Sie diesen Code ein:

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

    Dieser clientseitige AngularJS-Code erstellt eine neue angular-Anwendung `myApp` mit einem Controller `myCtrl`. Wenn die Anwendung im Browser des Betrachters ausgeführt wird, wird eine HTTP-GET-Anforderung zum Abrufen der Bücherliste in der Datenbank ausgegeben.

5. Erstellen Sie die Benutzeroberfläche für die App. Öffnen Sie die Datei `public/index.html` im Editor, und fügen Sie diesen Code ein:

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

    Dieser Code erstellt ein einfaches HTML-Formular mit vier Feldern zum Übermitteln von neuen Buchdaten und einer Tabelle zum Anzeigen aller Bücher, die bereits in der Datenbank gespeichert sind. Die verschiedenen `ng-`-HTML-Attribute verknüpfen den AngularJS-Code mit der Benutzeroberfläche.

6. Wir sind mit dem Bearbeiten der Dateien jetzt fertig. Vergewissern Sie sich, dass Sie alle Dateien gespeichert haben, und führen Sie dann den folgenden Befehl aus, um sie auf die VM zu kopieren. Geben Sie Ihr Kennwort ein, wenn Sie dazu aufgefordert werden.

    ```bash
    scp -r ~/Books <vm-admin-username>@<vm-public-ip>:~/Books
    ```

## <a name="install-node-packages"></a>Installieren von Node-Paketen

1. Wechseln Sie für die SSH-Verbindung wieder auf Ihre VM.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. Wechseln Sie in das Verzeichnis `Books`.

    ```bash
    cd ~/Books
    ```

1. Installieren Sie **Express** zur Verarbeitung des Routings Ihrer HTTP-Anforderungen, wobei entschieden wird, welche Inhalte an einen Benutzer Ihrer Webanwendung zurückgegeben werden.

    Führen Sie den folgenden Befehl zum Hinzufügen von Express als Paket für Ihre zu verwendende Webanwendung aus.

    ```bash
    npm install express
    ```

1. Installieren Sie **Mongoose** zur Unterstützung des Weiterleitens Ihrer Buchdaten zwischen MongoDB und dem HTTP-Anforderungsrouting.

    Die Buchinformationen werden über REST-API-Anforderungen abgefragt. Um die Übertragung von Daten in MongoDB und heraus an unsere API zu vereinfachen, verwenden wir Mongoose. Mongoose ist ein schemabasiertes System für die Modellierung von Daten. Wir werden es in unserer Beispielanwendung verwenden, um unsere Datenmodelle über die verschiedenen GET-, POST- und DELETE-HTTP-Anforderungen hinweg konsistent zu halten.

    Führen Sie den folgenden Befehl zum Hinzufügen von Mongoose als Paket für Ihre zu verwendende Webanwendung aus.

      ```bash
      npm install mongoose
      ```

1. Installieren Sie **body-parser**, um JSON-Anforderungsdaten für die Verwendung in unserem Express-Routing vorzuverarbeiten.

    Auf dem Back-End dient `body-parser` als Middleware zwischen Node.js und Express zum Analysieren der eingehenden JSON-Anforderungsdaten.

    Führen Sie den folgenden Befehl zum Hinzufügen von `body-parser` als Paket für Ihre zu verwendende Webanwendung aus.

      ```bash
      npm install body-parser
      ```

    > [!TIP]
    > Wenn Sie mehrere npm-Pakete installieren, können Sie alle in einen einzigen Befehl wie diesen einschließen:
    >
    > ```bash
    > npm install express mongoose body-parser
    > ```

## <a name="test-the-application"></a>Testen der Anwendung

1. Starten Sie die Anwendung mit dem folgenden Befehl mit Node.js.

    ```bash
    sudo node server.js
    ```

    Dadurch wird das Back-End der Anwendung gestartet, das dann an Port 80 auf eingehende HTTP-Anforderungen lauscht.

1. Testen Sie die Anwendungsfunktionalität.

    Öffnen Sie Ihren bevorzugten Browser, und navigieren Sie zur öffentlichen IP-Adresse Ihrer Azure-VM als URL.

    ```bash
    http://<vm-public-ip>
    ```

    Wenn alles in Ordnung ist, sehen Sie etwa folgenden Bildschirm:

    Der folgende Screenshot zeigt die Benutzeroberfläche zum Übermitteln von Buchdetails zur Speicherung in der MongoDB-Datenbank.

    ![Screenshot eines Webbrowsers mit dem Dateneingabeformular zum Hinzufügen eines Buchs.](../media/10-book-page.png)

    Sie sollten jetzt Bücher zum Speichern in der MongoDB-Datenbank übermitteln können. Außerdem sehen Sie die vollständige Liste der aus der Datenbank geladenen Bücher.