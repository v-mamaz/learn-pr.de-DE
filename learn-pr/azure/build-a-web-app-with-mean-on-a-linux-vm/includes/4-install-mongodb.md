Die meisten Anwendungen benötigen eine Datenbank. Das „M“ im MEAN-Stapel steht für MongoDB, eine der beliebtesten NoSQL-Datenbanklösungen, bei der es sich um ein kostenloses Open-Source-Produkt handelt. Für eine NoSQL-Datenbank ist es nicht wie bei relationalen Datenbanken wie SQL Server und MySQL erforderlich, dass Daten auf zuvor festgelegte Weise strukturiert werden.

MongoDB speichert Daten in JSON-ähnlichen Dokumenten, für die keine festen Datenstrukturen erforderlich sind. Anschließend wird mithilfe von Abfragen und Befehlen, die als JavaScript Object Notation (JSON) gesendet werden, mit MongoDB interagiert.

## <a name="mongodb-versions"></a>MongoDB-Versionen

Es gibt zwei verfügbare MongoDB-Versionen:

- MongoDB Community Server
- MongoDB Enterprise Server

In diesem Modul wird MongoDB Community Server (Version 3.6 zum Zeitpunkt der Erstellung dieses Dokuments) als Datenspeicher für die Webanwendung verwendet.

## <a name="how-to-install-mongodb"></a>Installieren von MongoDB

MongoDB kann unter Linux, macOS und Windows installiert werden. In diesem Modul wird der Dienst auf unserer Ubuntu Linux-VM installiert. Es ist allerdings abhängig vom Betriebssystem und der Distribution, welcher Paket-Manager sich am besten eignet. Der Installationsprozess für alle Betriebssysteme ist in der [Dokumentation zum Installieren von MongoDB](https://docs.mongodb.com/manual/administration/install-community/) festgehalten.

In diesem Modul wird für die Ubuntu-VM der **apt-get**-Paket-Manager verwendet.