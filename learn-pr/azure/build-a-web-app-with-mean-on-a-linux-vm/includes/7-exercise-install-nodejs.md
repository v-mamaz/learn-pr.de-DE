In dieser Einheit installieren Sie Node.js (das **N** im Akronym MEAN) auf einem virtuellen Ubuntu Linux-Computer, der in Azure gehostet wird. Node.js wird als Runtime verwendet, über die der HTTP-Datenverkehr verarbeitet und unsere Webanwendung gehostet wird.

## <a name="install-nodejs"></a>Installieren von Node.js

1. **Wenn Sie per immer noch mit Ihrem virtuellen Computer aus der vorherigen Übung sind**, SSH in.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. Registrieren Sie das Node.js-Paketrepository, damit **apt-get** das richtige Paket zur Installation auf Ihrem virtuellen Computer finden kann.

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. Installieren Sie das Node.js-Paket auf Ihrem Linux-System.

    ```bash
    sudo apt-get install -y Node.js
    ```

1. Überprüfen Sie mit dem folgenden Befehl, ob die Installation von Node.js erfolgreich war.

    ```bash
    node -v
    ```

    Die Ausgabe sollte etwa so wie in `v8.11.4` aussehen und die aktuelle Version von Node.js enthalten, die Sie bei der Installation angegeben haben.

## <a name="summary"></a>Zusammenfassung

Sie haben Node.js auf Ihrem virtuellen Computer installiert. Nun können Sie eine Webanwendung erstellen, die vom virtueller Computer ausgeführt wird.