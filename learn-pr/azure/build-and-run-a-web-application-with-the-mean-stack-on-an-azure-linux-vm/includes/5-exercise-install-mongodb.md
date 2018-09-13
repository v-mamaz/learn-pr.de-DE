In dieser Einheit installieren Sie MongoDB als Datenspeicher für Beispielwebanwendungen auf ihrem virtuellen Ubuntu Linux-Computer (virtual machine, VM).

## <a name="connect-to-the-vm"></a>Herstellen der Verbindung mit der VM

Sie müssen mithilfe von **ssh** eine Verbindung mit der VM herstellen, um MongoDB zu installieren. Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der zuvor erwähnten VM.

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-mongodb"></a>Installieren von MongoDB

> [!Important]
> Ubuntu stellt ein inoffizielles Paket namens **mongodb** bereit. Dieses Paket wird nicht von MongoDB Inc. verwaltet.

1. Importieren Sie den Verschlüsselungsschlüssel für das MongoDB-Repository. So kann der Paket-Manager prüfen, ob die mongodb-Pakete, die Sie installieren, wirklich von MongoDB Inc. stammen.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    Der Befehl **sudo** impliziert, dass der angegebene Befehl mit Administratorberechtigungen ausgeführt werden soll.

1. Registrieren Sie das Ubuntu-Repository für MongoDB, damit der Paket-Manager die mongodb-Pakete finden kann.

    > [!NOTE]
    > Dieser Befehl unterscheidet sich je nach Ubuntu-Version. Führen Sie `uname -v` aus, um zu prüfen, welche Ubuntu-Version Sie verwenden.
    > Die Ausgabe dieses Befehls sieht in etwa wie folgt aus: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.
    >
    > Diese Ausgabe lässt darauf schließen, dass Sie Version 16.04.1 von Ubuntu ausführen.
    > Den genauen Befehl für die jeweiligen Versionen finden Sie in der Dokumentation zum Installieren von MongoDB Community unter Ubuntu: [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/).

    Führen Sie unter Ubuntu 16.04 diesen Befehl aus:

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. Laden Sie die Paketdatenbank neu, damit Sie über aktuelle Paketinformationen verfügen.

    ```bash
    sudo apt-get update
    ```

1. Installieren Sie das MongoDB-Paket auf der VM.

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. Starten Sie den MongoDB-Dienst, damit Sie später eine Verbindung mit diesem herstellen können.

    ```bash
    sudo service mongod start
    ```

## <a name="summary"></a>Zusammenfassung

MongoDB ist jetzt auf Ihrer Ubuntu Linux-VM installiert. MongoDB dient als Sicherungsdatenspeicher für die Informationen, die Sie in Ihrer Webanwendung speichern und aus dieser abrufen.