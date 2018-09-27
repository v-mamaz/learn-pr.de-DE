Wir haben `Debian` für das Image verwendet, um den virtuellen Computer zu erstellen. Azure bietet verschiedene VM-Standardimages, mit denen Sie einen virtuellen Computer erstellen können. 

## <a name="listing-images"></a>Auflisten von Images

Mit dem folgenden Befehl können Sie eine Liste der verfügbaren Images virtueller Computer abrufen. 

```azurecli
az vm image list --output table
```

Dieser Befehl gibt die am häufigsten verwendeten Images aus, die zu einer in die Azure CLI integrierten Offlineliste gehören. Im Azure Marketplace sind jedoch _Hunderte_ von Imageoptionen verfügbar. 

## <a name="getting-all-images"></a>Abrufen aller Images

Sie können eine vollständige Liste abrufen, indem Sie dem Befehl das `--all`-Flag hinzufügen. Da die Liste der Images im Marketplace sehr umfangreich ist, ist es hilfreich, die Liste mit den Optionen „`--publisher`“, „`--sku`“ oder „`–-offer`“ zu filtern.

Verwenden Sie beispielsweise den folgenden Befehl, um _alle_ verfügbaren Wordpress-Images anzuzeigen:

```azurecli
az vm image list --sku Wordpress --output table --all
```

Oder diesen Befehl, um alle von Microsoft bereitgestellten Images anzuzeigen:

```azurecli
az vm image list --publisher Microsoft --output table --all
```

## <a name="location-specific-images"></a>Standortspezifische Images

Einige Images sind nur in bestimmten Regionen verfügbar. Fügen Sie das `--location [location]`-Flag zum Befehl hinzu, um die Ergebnisse auf diejenigen einzugrenzen, die in der Region verfügbar sind, in der Sie den virtuellen Computer erstellen möchten. Geben Sie z.B. in Azure Cloud Shell Folgendes ein, um eine Liste der in der Region `eastus` verfügbaren Images abzurufen.

```azurecli
az vm image list --location eastus --output table
```

Versuchen Sie, einige der Images an den anderen verfügbaren Azure-Sandboxstandorten zu überprüfen:

[!include[](../../../includes/azure-sandbox-regions-note.md)]

> [!TIP]
> Dies sind die Standardimages, die von Azure bereitgestellt werden. Denken Sie daran, dass Sie auch [eigene benutzerdefinierte Images erstellen und hochladen](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) können, um virtuelle Computer basierend auf eindeutigen Konfigurationen oder weniger häufigen Versionen oder Distributionen eines Betriebssystems zu erstellen.

Ihr Befehlsfenster ist jetzt wahrscheinlich voll. Sie können `clear` eingeben, um den Bildschirm zu löschen, wenn Sie möchten.