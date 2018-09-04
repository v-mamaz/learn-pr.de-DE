Das Letzte, was wir in unserer VM ausprobieren möchten, ist die Installation eines Webservers. Eines der am einfachsten zu installierenden Pakete ist `nginx`.

1. Bestimmen Sie die öffentliche IP-Adresse Ihres virtuellen Linux-Computers. Denken Sie daran, dass Sie den Befehl `vm list-ip-addresses` verwenden können, um ihn nachzuschlagen.

1. Öffnen Sie als Nächstes wie beim Test eine `ssh`-Verbindung mit dem Computer. Sie müssen hierbei den Administratornamen übergeben („**aldis**“).

1. Führen Sie in der dargestellten Shell den folgenden Befehl zum Installieren des Webservers `nginx` aus.

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

1. Verwenden Sie in Azure Cloud Shell `curl`, um die Standardseite von Ihrem Linux-Webserver einzulesen. Alternativ können Sie eine neue Browserregisterkarte öffnen und zur öffentlichen IP-Adresse navigieren.

```azurecli
curl 168.61.54.62
```

Er wird fehlschlagen, weil der virtuelle Linux-Computer den Port 80 (`http`) durch die integrierte Firewall nicht verfügbar macht. Glücklicherweise bietet die Azure CLI einen Befehl hierfür: `vm open-port`. 

1. Geben Sie Folgendes in Cloud Shell ein, um Port 80 zu öffnen:

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

Wiederholen Sie schließlich `curl`. Dieses Mal sollten Daten zurückgegeben werden. Sie können die Seite auch in einem Browser anzeigen.
