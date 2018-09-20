Das Letzte, was wir in unserer VM ausprobieren möchten, ist die Installation eines Webservers. Eines der am einfachsten zu installierenden Pakete ist `nginx`.

## <a name="install-nginx-web-server"></a>Installieren eines NGINX-Webservers

1. Bestimmen Sie die öffentliche IP-Adresse Ihres virtuellen Linux-Computers. Denken Sie daran, dass Sie den Befehl `vm list-ip-addresses` verwenden können, um ihn nachzuschlagen.

1. Öffnen Sie als Nächstes wie beim Test eine `ssh`-Verbindung mit dem Computer. Sie müssen hierbei den Administratornamen übergeben („**aldis**“).

1. Führen Sie in der dargestellten Shell den folgenden Befehl zum Installieren des Webservers `nginx` aus.

```bash
sudo apt-get -y update && sudo apt-get -y install nginx
```

1. Beenden Sie die Secure Shell.

```bash
exit
```

## <a name="retrieve-our-default-page"></a>Abrufen unserer Standardseite

1. Verwenden Sie in Azure Cloud Shell `curl`, um die Standardseite von Ihrem Linux-Webserver einzulesen. Alternativ können Sie eine neue Browserregisterkarte öffnen und zur öffentlichen IP-Adresse navigieren.

```azurecli
curl 40.83.165.85
```

Er wird fehlschlagen, weil der virtuelle Linux-Computer den Port 80 (`http`) durch die integrierte Firewall nicht verfügbar macht. Glücklicherweise bietet die Azure CLI einen Befehl hierfür: `vm open-port`. 

1. Geben Sie Folgendes in Cloud Shell ein, um Port 80 zu öffnen:

```azurecli
az vm open-port --port 80 --resource-group <rgn>[Sandbox resource group name]</rgn> --name SampleVM
```

Es dauert einen Moment, die Netzwerkregel hinzuzufügen und den Port über die Firewall zu öffnen. Versuchen Sie `curl` erneut. Dieses Mal sollten Daten zurückgegeben werden. Sie können die Seite auch in einem Browser anzeigen.

```output
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx on Debian!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx on Debian!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working on Debian. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a></p>

<p>
      Please use the <tt>reportbug</tt> tool to report bugs in the
      nginx package with Debian. However, check <a
      href="http://bugs.debian.org/cgi-bin/pkgreport.cgi?ordering=normal;archive=0;src=nginx;repeatmerged=0">existing
      bug reports</a> before reporting a new bug.
</p>

<p><em>Thank you for using debian and nginx.</em></p>


</body>
</html>
```
