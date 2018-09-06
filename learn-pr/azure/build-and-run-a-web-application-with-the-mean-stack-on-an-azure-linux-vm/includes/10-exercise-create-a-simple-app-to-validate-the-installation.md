In dieser Übung erstellen Sie eine einfache, in Node.js gehostete AngularJS-Anwendung und verwenden Express für das Routing. Auf dem Back-End dient Ihnen MongoDB als Datenspeicher. Die Anwendung ist eine Buchdatenbank, in der Sie Bücher auflisten, hinzufügen und löschen können.

> [!Important]
> Einziger Zweck dieser sehr einfachen Anwendung ist das Testen des neu installierten MEAN-Stapels. Da diese Anwendung weder ausreichend sicher noch bereit für die Produktion ist, verwenden Sie sie entsprechend.

## <a name="connect-to-the-vm"></a>Herstellen der Verbindung mit der VM

Wenn die Verbindung mit Ihrer VM noch nicht besteht, müssen Sie den folgenden Befehl ausführen. Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der zuvor erwähnten VM.

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="create-the-back-end"></a>Erstellen des Back-Ends

1. Erstellen Sie mit dem folgenden Befehl eine Ordnerstruktur für die neue Beispielanwendung.

    ```bash
    mkdir ~/Books
    mkdir ~/Books/app
    mkdir ~/Books/public
    ```

    Am Hauptstandort Ihres Administratorbenutzers haben Sie einen Ordner namens „Books“ erstellt, der die App Ihres Projekts und deren Abhängigkeiten enthält. In diesem Ordner haben Sie einen Ordner „app“ erstellt, der alle Ihre Anwendungsressourcen und Skripts enthält. Schließlich erstellen wir auch einen „public“-Ordner zum Speichern aller clientseitigen Dateien, die direkt auf entsprechende HTTP-Anforderungen hin bereitgestellt werden.

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

    Auf dem Back-End dient body-parser als Middleware zwischen Node.js und Express zum Analysieren der eingehenden JSON-Anforderungsdaten.

    Führen Sie den folgenden Befehl zum Hinzufügen von body-parser als Paket für Ihre zu verwendende Webanwendung aus.

        ```bash
        npm install body-parser
        ```

    > [!Note]
    > Wenn Sie mehrere npm-Pakete installieren, können Sie auch alle in einen einzigen Befehl wie diesen einschließen.
    > ```bash
    > npm install express mongoose body-parser
    > ```

1. Erstellen Sie das Datenmodell-Back-End für Ihre Bücherwebanwendung mithilfe von Mongoose.

    1. Erstellen Sie im **app**-Ordner Ihres **Books**-Anwendungsordners eine neue JavaScript-Datei namens **model.js**, die das Mongoose-basierte Datenmodell Ihrer Bücher enthält.

        ```bash
        nano ~/Books/app/model.js
        ```

    1. Fügen Sie zum Erstellen unseres Buchschemas mithilfe von Mongoose den folgenden Code in diese neue Datei ein.

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

        > [!Note]
        > Zum Speichern der aktuellen Datei in **nano** müssen Sie **STRG**+**O** drücken, und um **nano** zu beenden, müssen Sie **STRG**+**X** drücken.

        Dieser Code stellt eine Verbindung mit einer Datenbank namens `Books` auf dem MongoDB-Server des lokalen virtuellen Computers her. Er erstellt dann ein Dokument namens `Book` mit dem von der `bookSchema`-Variablen definierten Schema her.

1. Erstellen Sie die Express-Routen für die Anwendung zur Verarbeitung der verschiedenen HTTP-Anforderungen.

    1. Erstellen Sie im **app**-Ordner eine neue JavaScript-Datei namens **routes.js**.

        ```bash
        nano ~/Books/app/routes.js
        ```

    1. Fügen Sie den folgenden Code in diese neue Datei ein, um die Routen mit Express herzustellen.

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

        Express kann HTTP-Antworten direkt an den Routenverarbeitungscode leiten oder statischen Inhalt aus Dateien bereitstellen. Wir werden in diesem Beispiel einer Webanwendung beides ausführen, mit JSON-Daten auf API-Buchanforderungen und mit HTML-Daten direkt aus der Datei „index.html“ antworten.

1. Erstellen Sie eine **server.js**-Datei im **Books**-Ordner, um das Node.js-Hosting zu konfigurieren (mit den Express-Routen).

    1. Erstellen Sie zurück im Anwendungsstammordner **Books** eine neue JavaScript-Datei namens **server.js**.

        ```bash
        nano ~/Books/server.js
        ```

    1. Fügen Sie zum Konfigurieren Ihrer Webanwendung und Starten der Überwachung des HTTP-Standardports den folgenden Code in diese neue Datei ein.

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

        Dieser Code erstellt die Webanwendung selbst. Er stellt statische Dateien aus einem Ordner mit dem Namen **public** (als Nächstes erstellt) bereit und verwendet die im vorherigen Schritt definierten Routen.

1. Erstellen Sie die Front-End-HTML- und die clientseitige JavaScript-Anwendung.

    1. Erstellen Sie im **public**-Inhaltsordner eine neue JavaScript-Datei namens **script.js**.

        ```bash
        nano ~/Books/public/script.js
        ```

    1. Fügen Sie zum Konfigurieren Ihrer clientseitigen Webanwendung den folgenden Code zum Durchführen der Kommunikation mit dem Webserver in diese neue Datei ein.

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

    1. Erstellen Sie im **public**-Inhaltsordner auch eine neue HTML-Datei namens **index.html**.

        ```bash
        nano ~/Books/public/index.html
        ```

    1. Fügen Sie das folgende Markup in diese neue Datei ein, um die HTML-Benutzeroberfläche Ihrer Webanwendung einzurichten.

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

        Dieser Code erstellt ein einfaches HTML-Formular mit vier Feldern zum Übermitteln von neuen Buchdaten und eine Tabelle zum Anzeigen aller Bücher, die bereits in der Datenbank gespeichert sind. Die verschiedenen `ng-`-HTML-Attribute verknüpfen den AngularJS-Code mit der Benutzeroberfläche.

1. Testen Sie die vollständige Bücherwebanwendung.

    1. Starten Sie die Anwendung mit dem folgenden Befehl mit Node.js.

        ```bash
        sudo node ~/Books/server.js
        ```

        Dadurch wird das Back-End der Anwendung, gestartet, das dann Port 80 auf eingehende HTTP-Anforderungen überwacht.

    1. Testen Sie die Anwendungsfunktionalität.

        Öffnen Sie Ihren bevorzugten Browser, und navigieren Sie zur öffentlichen IP-Adresse Ihrer Azure-VM als URL.

        ```bash
        http://<vm-public-ip>
        ```

        Wenn alles in Ordnung ist, sehen Sie etwa folgenden Bildschirm:

        Der folgende Screenshot zeigt die Benutzeroberfläche zum Übermitteln von Buchdetails zur Speicherung in der MongoDB-Datenbank.


        ![Screenshot eines Webbrowsers mit dem Dateneingabeformular zum Hinzufügen eines Buchs.](../media-draft/10-book-page.png)

    Sie sollten jetzt Bücher zum Speichern in der MongoDB-Datenbank übermitteln können. Außerdem sehen Sie die vollständige Liste der aus der Datenbank geladenen Bücher.
