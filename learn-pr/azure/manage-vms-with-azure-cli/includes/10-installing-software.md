Der letzte Schritt soll nun versuchen Sie es auf dem virtuellen Computer ist auf einen Webserver zu installieren. Eine der einfachsten Pakete zu installieren ist `nginx`.

1. Suchen Sie die öffentliche IP-Adresse des virtuellen Linux-Computer. Denken Sie daran, Sie können die `vm list-ip-addresses` Befehls zu suchen.

2. Öffnen Sie als Nächstes eine `ssh` Verbindung mit dem Computer, wie bei der testen. Denken Sie daran, Sie müssen den Administratornamen zu übergeben ("**Aldis**").

3. Führen Sie in der dargestellten Shell den folgenden Befehl zum Installieren der `nginx` Webserver.

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. Verwenden Sie in der Cloud Shell `curl` die Standardseite von Ihrem Linux-Web-Server zu lesen. Alternativ können Sie eine neue Browserregisterkarte zu öffnen, und navigieren Sie zu die öffentliche IP-Adresse.

```azurecli
curl 168.61.54.62
```

Es schlägt fehl, da es sich bei virtuellen Linux-Computer auf Port 80 verfügbar macht (`http`) über die integrierte Firewall. Glücklicherweise wurde der Azure-Befehlszeilenschnittstelle einen Befehl für diese: `vm open-port`. 

5. Geben Sie Folgendes in die Cloud Shell, öffnen Sie Port 80:

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

Letztendlich sollten Sie `curl` erneut aus. Dieses Mal sollte Rückgabe von Daten – sehen Sie die Seite in einem Browser auch.



