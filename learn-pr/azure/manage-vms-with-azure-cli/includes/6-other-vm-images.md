Wir haben `Debian` für das Image verwendet, um den virtuellen Computer zu erstellen. Azure bietet verschiedene VM-Standardimages, mit denen Sie einen virtuellen Computer erstellen können. 

Mit dem Befehl „`az vm image list --output table`“ können Sie eine Liste der verfügbaren Images abrufen. Dieser Befehl gibt die am häufigsten verwendeten Images aus, die zu einer in die Azure CLI integrierten Offlineliste gehören. Im Azure Marketplace sind jedoch _Hunderte_ von Imageoptionen verfügbar. 

> [!TIP]
> Sie können eine vollständige Liste abrufen, indem Sie dem Befehl das `--all`-Flag hinzufügen. Da die Liste der Images im Marketplace sehr umfangreich ist, ist es hilfreich, die Liste mit den Optionen „`--publisher`“ oder „`–-offer`“ zu filtern.

Einige Images sind nur in bestimmten Regionen verfügbar. Fügen Sie das `--location [location]`-Flag zum Befehl hinzu, um die Ergebnisse auf diejenigen einzugrenzen, die in der Region verfügbar sind, in der Sie den virtuellen Computer erstellen möchten. Geben Sie z.B. in Azure Cloud Shell Folgendes ein, um eine Liste der in der Region „`eastus`“ verfügbaren Images abzurufen.

```azurecli
az vm image list --location eastus --output table
```

> [!NOTE]
> Dies sind die Standardimages, die von Azure bereitgestellt werden. Denken Sie daran, dass Sie auch [eigene benutzerdefinierte Images erstellen und hochladen](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) können, um virtuelle Computer basierend auf eindeutigen Konfigurationen oder weniger häufigen Versionen oder Distributionen eines Betriebssystems zu erstellen.