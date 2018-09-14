Nun, dass Ihr virtueller Computer ausgeführt wird, führen wir etwas damit. Hier installieren Sie einen Webserver und stellen Sie eine einfache Webseite, in dem der Hostname der VM angezeigt.

Um einen virtuellen Computer zu konfigurieren, haben Sie mehrere Optionen. Sie können eine direkte Verbindung herstellen und interaktiv Konfiguration Ihres Systems. Auf Windows-Systemen können Sie z. B. eine Remotedesktopsitzung auf der Benutzeroberfläche der remote-Windows-Computer herstellen, als ob Sie sich säßen erstellen. Bei Linux-Systemen können Sie eine SSH-Verbindung sicher mit Ihrem Linux-Remotesystem über das Terminal arbeiten erstellen.

Manuelle Konfiguration ist ein guter Anfang, aber wenn Sie Systeme hinzufügen, können Sie Ihre Bereitstellungen automatisieren. Automation umfasst das Ausführen von wiederholbarer Prozessen wie z. B. Programme und Skripts, die die Schwerstarbeit für Sie erledigt.

::: zone pivot="windows-cloud"

Hier müssen Sie die IIS aus der Cloud Shell-Sitzung, die Verwendung eines Features der Windows-basierten virtuellen Azure-Computern wird aufgerufen, die benutzerdefinierte Skripterweiterung Remote konfigurieren.

::: zone-end

::: zone pivot="linux-cloud"

Hier werden Sie die Nginx aus der Cloud Shell-Sitzung, die über ein Feature von Linux-basierten virtuellen Azure-Computern wird aufgerufen, die benutzerdefinierte Skripterweiterung Remote konfigurieren.

::: zone-end

::: zone pivot="windows-cloud"

## <a name="what-is-iis"></a>Was ist IIS?

Internet Information Services oder IIS ist ein Webserver, der unter Windows ausgeführt wird. Sie können die IIS verwenden, zum Verarbeiten von standard-Web-Inhalt (HTML, CSS und JavaScript) oder Ausführen von ASP.NET und anderen Arten von Webanwendungen. IIS im Lieferumfang von Windows Server, jedoch müssen Sie darauf, um die beginnen mit dem Senden von Webseiten zu aktivieren.

## <a name="whats-the-custom-script-extension"></a>Was ist die benutzerdefinierte Skripterweiterung?

Die benutzerdefinierte Skripterweiterung ist eine einfache Möglichkeit zum Herunterladen und Ausführen von Skripts auf Ihre Azure-VMs. Es ist nur eine von vielen Möglichkeiten, die Sie Ihrem virtuellen Computer konfigurieren können, sobald Ihr virtueller Computer ausgeführt wird.

Sie können Ihre Skripts im Azure-Speicher oder in einem öffentlichen Speicherort wie z. B. GitHub speichern. Sie können Skripts manuell oder als Teil einer automatisierten Bereitstellung ausführen. Hier führen Sie einen Azure-CLI-Befehl zum Laden ein PowerShell-Skripts von GitHub herunter, und führen Sie es auf Ihrem virtuellen Computer. Das Skript ist IIS konfiguriert.

## <a name="configure-iis"></a>Konfigurieren von IIS

Hier verwenden Sie die benutzerdefinierte Skripterweiterung zum Konfigurieren von IIS Remote auf Ihrem virtuellen Computer über Cloud Shell aus. Sie müssen auch die Firewall für eingehenden Netzwerkzugriff auf Port 80 (HTTP) konfigurieren.

1. In Cloud Shell, führen Sie diesen `az vm extension set` Befehl zum Herunterladen und Ausführen eines PowerShell-Skripts, die IIS installiert und konfiguriert, eine einfache Startseite.

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myWindowsVM \
      --name CustomScriptExtension \
      --publisher Microsoft.Compute \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1"]}' \
      --protected-settings '{"commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"}'
    ```

    Der Vorgang dauert einige Minuten in Anspruch.

    In der Zwischenzeit können Sie [untersuchen Sie das PowerShell-Skript](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1?azure-portal=true) aus einer separaten Registerkarte des Browsers bei Bedarf. Das Skript wird IIS installiert und konfiguriert auf der Startseite, um eine Begrüßungsnachricht an zusammen mit den Computernamen des virtuellen Computers "MyWindowsVM" anzuzeigen.

1. Führen Sie diesen `az vm open-port` Befehl zum Öffnen von Port 80 (HTTP) über die Firewall.

    ```azurecli
    az vm open-port \
      --name myWindowsVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Nun, da IIS eingerichtet ist, wir stellen Sie sicher, dass er ausgeführt wird.

1. Führen Sie diesen `az vm list-ip-addresses` Befehl zum Auflisten der öffentlichen IP-Adresse Ihres virtuellen Computers behandelt.

    ```azurecli
    az vm list-ip-addresses \
      --name myWindowsVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > Dieser Befehl ist ziemlich komplex, vor allem `--query` Argument. Aber Sie werden ein Profi in diesem auf, wie Sie etwas tiefer gehen und erkunden Sie Azure.

    Daraufhin wird ein Ihres virtuellen Computers öffentliche IP-Adresse. Hier sehen Sie ein Beispiel.

    ```console
    104.211.9.245
    ```

1. Navigieren Sie in einer neuen Browserregisterkarte auf die IP-Adresse Ihres virtuellen Computers. Sie finden Sie unter Ihrem Begrüßungsnachricht und der VM-Namen.

    ![](../media/iis-browser.png)

::: zone-end

::: zone pivot="linux-cloud"

## <a name="what-is-nginx"></a>Was ist Nginx?

Nginx (ausgesprochen "-Engine-X") ist eine beliebte, kostenlos, Open-Source-Webserver, der auf Unix, Linux, MacOS und Windows ausgeführt wird. Hier werden Sie Nginx verwenden, um eine einfache Webseite bereitstellen.

## <a name="whats-the-custom-script-extension"></a>Was ist die benutzerdefinierte Skripterweiterung?

Die benutzerdefinierte Skripterweiterung ist eine einfache Möglichkeit zum Herunterladen und Ausführen von Skripts auf Ihre Azure-VMs. Es ist nur eine von vielen Möglichkeiten, die Sie Ihrem virtuellen Computer konfigurieren können, sobald Ihr virtueller Computer ausgeführt wird.

Sie können Ihre Skripts im Azure-Speicher oder in einem öffentlichen Speicherort wie z. B. GitHub speichern. Sie können Skripts manuell oder als Teil einer automatisierten Bereitstellung ausführen. Hier führen Sie einen Azure-CLI-Befehl aus, um ein Bash-Skript von GitHub herunterladen, und führen Sie es auf Ihrem virtuellen Computer. Das Skript konfiguriert Nginx.

## <a name="configure-nginx"></a>Konfigurieren von Nginx

Hier verwenden Sie die benutzerdefinierte Skripterweiterung, um Nginx auf Ihrem virtuellen Computer über Cloud Shell die Remotekonfiguration. Sie müssen auch die Firewall für eingehenden Netzwerkzugriff auf Port 80 (HTTP) konfigurieren.

1. In Cloud Shell, führen Sie diesen `az vm extension set` Befehl zum Herunterladen und Ausführen eines Bash-Skripts, die Nginx installiert und konfiguriert eine einfache Startseite.

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myLinuxVM \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/20fca2517fa5913150abab66b51b0d88aa3077d8/configure-nginx.sh"]}' \
      --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
    ```

    Der Vorgang dauert einige Minuten in Anspruch.

    In der Zwischenzeit können Sie [untersuchen Sie das Bash-Skript](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/20fca2517fa5913150abab66b51b0d88aa3077d8/configure-nginx.sh?azure-portal=true) aus einer separaten Registerkarte des Browsers bei Bedarf. Das Skript wird der Nginx installiert und konfiguriert auf der Startseite, um eine Begrüßungsnachricht an zusammen mit den Computernamen des virtuellen Computers "MyLinuxVM" anzuzeigen.

1. Führen Sie diesen `az vm open-port` Befehl zum Öffnen von Port 80 (HTTP) über die Firewall.

    ```azurecli
    az vm open-port \
      --name myLinuxVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Nun, da Nginx eingerichtet ist, wir stellen Sie sicher, dass er ausgeführt wird.

1. Führen Sie diesen `az vm list-ip-addresses` Befehl zum Auflisten der öffentlichen IP-Adresse Ihres virtuellen Computers behandelt.

    ```azurecli
    az vm list-ip-addresses \
      --name myLinuxVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > Dieser Befehl ist ziemlich komplex, vor allem `--query` Argument. Aber Sie werden ein Profi in diesem auf, wie Sie etwas tiefer gehen und erkunden Sie Azure.

    Daraufhin wird ein Ihres virtuellen Computers öffentliche IP-Adresse. Hier sehen Sie ein Beispiel.

    ```console
    137.135.110.210
    ```

1. Navigieren Sie in einer neuen Browserregisterkarte auf die IP-Adresse Ihres virtuellen Computers. Sie finden Sie unter Ihrem Begrüßungsnachricht und der VM-Namen.

    ![](../media/nginx-browser.png)

::: zone-end

## <a name="summary"></a>Zusammenfassung

Ihr virtueller Computer ausgeführt wird, und dienen jetzt Einrichten von Webseiten, aber was bedeutet, die für Sie?

Beachten Sie, dass alle Weg mit den Grundlagen und fast alle gute Innovation, die in der Cloud, die von anderen Unternehmen Groß und klein, geboren beginnt mit einem ähnlichen Setup, gestartet. Der Weiterentwicklung Ihrer Idee, beginnt er eine positive Auswirkung auf Ihr Unternehmen und Ihre Benutzer.