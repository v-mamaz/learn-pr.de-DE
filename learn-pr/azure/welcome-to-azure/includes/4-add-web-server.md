Nachdem Ihr virtueller Computer nun betriebsbereit ist und ausgeführt wird, kann er Aufgaben übernehmen. Hier installieren Sie einen Webserver und stellen eine einfache Webseite bereit, die den Hostnamen des virtuellen Computers angezeigt.

Zum Konfigurieren eines virtuellen Computers sind mehrere Optionen verfügbar. Sie können eine direkte Verbindung herstellen und Ihr System interaktiv konfigurieren. Auf Windows-Systemen können Sie z.B. eine Remotedesktopsitzung erstellen, um mit der Benutzeroberfläche des Windows-Remotecomputers eine Verbindung herzustellen, als ob Sie davor säßen. Bei Linux-Systemen können Sie eine SSH-Verbindung erstellen, um sicher mit Ihrem Linux-Remotesystem über das Terminal zu arbeiten.

Manuelle Konfiguration ist ein guter Anfang, aber wenn Sie Systeme hinzufügen, können Sie Ihre Bereitstellungen auch automatisieren. Automatisierung beinhaltet die Ausführung wiederholbarer Prozesse (z.B. Programme und Skripts), die Arbeiten für Sie erledigen.

::: zone pivot="windows-cloud"

Hier konfigurieren Sie IIS remote aus Ihrer Cloud Shell-Sitzung mithilfe eines Features von Windows-basierten virtuellen Azure-Computern, das als benutzerdefinierte Skripterweiterung bezeichnet wird.

::: zone-end

::: zone pivot="linux-cloud"

Hier konfigurieren Sie Nginx remote aus Ihrer Cloud Shell-Sitzung mithilfe eines Features von Linux-basierten virtuellen Azure-Computern, das als benutzerdefinierte Skripterweiterung bezeichnet wird.

::: zone-end

::: zone pivot="windows-cloud"

## <a name="what-is-iis"></a>Was ist IIS?

Internetinformationsdienste (Internet Information Services, IIS) ist ein Webserver, der unter Windows ausgeführt wird. Sie können IIS verwenden, um Standardwebinhalte (HTML, CSS und JavaScript) bereitzustellen oder ASP.NET und andere Arten von Webanwendungen auszuführen. IIS ist im Lieferumfang von Windows Server enthalten, muss jedoch aktiviert werden, damit Webseiten bereitgestellt werden können.

## <a name="whats-the-custom-script-extension"></a>Was ist die benutzerdefinierte Skripterweiterung?

Die benutzerdefinierte Skripterweiterung ist eine einfache Möglichkeit zum Herunterladen und Ausführen von Skripts auf Ihren virtuellen Azure-Computern. Sie ist nur eine von vielen Möglichkeiten zum Konfigurieren Ihres virtuellen Computers, sobald dieser betriebsbereit ist und ausgeführt wird.

Sie können Ihre Skripts im Azure-Speicher oder in einem öffentlichen Speicherort wie z.B. GitHub speichern. Sie können Skripts manuell oder als Teil einer automatisierten Bereitstellung ausführen. Hier führen Sie einen Azure CLI-Befehl zum Herunterladen eines PowerShell-Skripts von GitHub aus und führen dieses dann auf Ihrem virtuellen Computer aus. Das Skript konfiguriert IIS.

## <a name="configure-iis"></a>Konfigurieren von IIS

Hier verwenden Sie die benutzerdefinierte Skripterweiterung, um IIS remote auf Ihrem virtuellen Computer über Cloud Shell zu konfigurieren. Sie konfigurieren außerdem die Firewall für eingehenden Netzwerkzugriff an Port 80 (HTTP).

1. Führen Sie den Befehl `az vm extension set` in Cloud Shell zum Herunterladen und Ausführen eines PowerShell-Skripts aus, das IIS installiert und eine einfache Startseite konfiguriert.

    ```azurecli
    az vm extension set \
      --resource-group myResourceGroup \
      --vm-name myWindowsVM \
      --name CustomScriptExtension \
      --publisher Microsoft.Compute \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1"]}' \
      --protected-settings '{"commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"}'
    ```

    Dieser Vorgang nimmt einige Minuten in Anspruch.

    Wenn Sie möchten, können Sie in der Zwischenzeit [das PowerShell-Skript untersuchen](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1?azure-portal=true) (auf einer separaten Browserregisterkarte). Das Skript installiert IIS und konfiguriert die Startseite für die Anzeige einer Begrüßungsnachricht zusammen mit dem Computernamen des virtuellen Computers „myWindowsVM“.

1. Führen Sie den Befehl `az vm open-port` zum Öffnen von Port 80 (HTTP) über die Firewall aus.

    ```azurecli
    az vm open-port \
      --name myWindowsVM \
      --resource-group myResourceGroup \
      --port 80
    ```

## <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Da IIS nun eingerichtet ist, können wir die Ausführung überprüfen.

1. Führen Sie den Befehl `az vm list-ip-addresses` zum Auflisten der öffentlichen IP-Adresse Ihres virtuellen Computers aus.

    ```azurecli
    az vm list-ip-addresses \
      --name myWindowsVM \
      --resource-group myResourceGroup \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > Dieser Befehl ist recht komplex, insbesondere das Argument `--query`. Aber Sie werden schon bald ein Profi sein, wenn Sie sich einarbeiten und Azure erkunden.

    Die öffentliche IP-Adresse Ihres virtuellen Computers wird angezeigt. Hier sehen Sie ein Beispiel.

    ```console
    104.211.9.245
    ```

1. Navigieren Sie auf einer neuen Browserregisterkarte zur IP-Adresse Ihres virtuellen Computers. Eine Begrüßungsnachricht und der Name Ihres virtuellen Computers werden angezeigt.

    ![](../media/iis-browser.png)

::: zone-end

::: zone pivot="linux-cloud"

## <a name="what-is-nginx"></a>Was ist Nginx?

Nginx (ausgesprochen „Engine-x“) ist ein beliebter, kostenloser Open-Source-Webserver, der unter Unix, Linux, macOS und Windows ausgeführt werden kann. Hier verwenden Sie Nginx, um eine einfache Webseite bereitzustellen.

## <a name="whats-the-custom-script-extension"></a>Was ist die benutzerdefinierte Skripterweiterung?

Die benutzerdefinierte Skripterweiterung ist eine einfache Möglichkeit zum Herunterladen und Ausführen von Skripts auf Ihren virtuellen Azure-Computern. Sie ist nur eine von vielen Möglichkeiten zum Konfigurieren Ihres virtuellen Computers, sobald dieser betriebsbereit ist und ausgeführt wird.

Sie können Ihre Skripts im Azure-Speicher oder in einem öffentlichen Speicherort wie z.B. GitHub speichern. Sie können Skripts manuell oder als Teil einer automatisierten Bereitstellung ausführen. Hier führen Sie einen Azure CLI-Befehl zum Herunterladen eines Bash-Skripts von GitHub aus und führen dieses dann auf Ihrem virtuellen Computer aus. Das Skript konfiguriert Nginx.

## <a name="configure-nginx"></a>Konfigurieren von Nginx

Hier verwenden Sie die benutzerdefinierte Skripterweiterung, um Nginx remote auf Ihrem virtuellen Computer über Cloud Shell zu konfigurieren. Sie konfigurieren außerdem die Firewall für eingehenden Netzwerkzugriff an Port 80 (HTTP).

1. Führen Sie den Befehl `az vm extension set` in Cloud Shell zum Herunterladen und Ausführen eines Bash-Skripts aus, das Nginx installiert und eine einfache Startseite konfiguriert.

    ```azurecli
    az vm extension set \
      --resource-group myResourceGroup \
      --vm-name myLinuxVM \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/20fca2517fa5913150abab66b51b0d88aa3077d8/configure-nginx.sh"]}' \
      --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
    ```

    Dieser Vorgang nimmt einige Minuten in Anspruch.

    Wenn Sie möchten, können Sie in der Zwischenzeit [das Bash-Skript untersuchen](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/20fca2517fa5913150abab66b51b0d88aa3077d8/configure-nginx.sh?azure-portal=true) (auf einer separaten Browserregisterkarte). Das Skript installiert Nginx und konfiguriert die Startseite für die Anzeige einer Begrüßungsnachricht zusammen mit dem Computernamen des virtuellen Computers „myLinuxVM“.

1. Führen Sie den Befehl `az vm open-port` zum Öffnen von Port 80 (HTTP) über die Firewall aus.

    ```azurecli
    az vm open-port \
      --name myLinuxVM \
      --resource-group myResourceGroup \
      --port 80
    ```

## <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Da Nginx nun eingerichtet ist, können wir die Ausführung überprüfen.

1. Führen Sie den Befehl `az vm list-ip-addresses` zum Auflisten der öffentlichen IP-Adresse Ihres virtuellen Computers aus.

    ```azurecli
    az vm list-ip-addresses \
      --name myLinuxVM \
      --resource-group myResourceGroup \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > Dieser Befehl ist recht komplex, insbesondere das Argument `--query`. Aber Sie werden schon bald ein Profi sein, wenn Sie sich einarbeiten und Azure erkunden.

    Die öffentliche IP-Adresse Ihres virtuellen Computers wird angezeigt. Hier sehen Sie ein Beispiel.

    ```console
    137.135.110.210
    ```

1. Navigieren Sie auf einer neuen Browserregisterkarte zur IP-Adresse Ihres virtuellen Computers. Eine Begrüßungsnachricht und der Name Ihres virtuellen Computers werden angezeigt.

    ![](../media/nginx-browser.png)

::: zone-end

## <a name="summary"></a>Zusammenfassung

Ihr virtueller Computer wird ausgeführt und kann nun Webseiten bereitstellen. Aber was bedeutet das für Sie?

Denken Sie daran, jede Reise beginnt mit den Grundlagen, und fast jede große Innovation, die in der Cloud geboren wurde (von großen und kleinen Unternehmen), begann mit einem ähnlichen Setup wie bei Ihnen. Wenn sich Ihre Idee weiterentwickelt, beginnt sie sich positiv auf Ihr Unternehmen und Ihre Benutzer auszuwirken.