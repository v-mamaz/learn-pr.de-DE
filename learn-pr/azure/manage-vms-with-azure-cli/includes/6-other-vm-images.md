Wir verwendeten `Debian` für das Image zum Erstellen des virtuellen Computers. Azure verfügt über mehrere standard VM-Images, die Sie zum Erstellen eines virtuellen Computers verwenden können. 

Sie erhalten eine Liste der verfügbaren Images mithilfe der `az vm image list --output table` Befehl. Dies gibt die am häufigsten verwendeten Images, die Teil einer offline-Liste in der Azure-Befehlszeilenschnittstelle integriert sind. Es gibt jedoch _Hunderte_ des imageoptionen, die in den Azure Marketplace verfügbar sind. 

> [!TIP]
> Sie können eine vollständige Liste erhalten, durch das Hinzufügen der `--all` Flag an den Befehl. Da die Liste der Images im Marketplace sehr groß ist, ist es hilfreich, um die Liste mit Filtern die `--publisher` oder `–-offer` Optionen.

Einige Images sind nur in bestimmten Speicherorten verfügbar. Versuchen Sie es hinzufügen der `--location [location]` Flag an den Befehl um die Ergebnisse an solche zur Verfügung, in der Region zu begrenzen, die den virtuellen Computer in erstellt werden soll. Geben Sie beispielsweise Folgendes in Cloud Shell zum Abrufen einer Liste der Images verfügbar, in der `eastus` Region.

```azurecli
az vm image list --location eastus --output table
```

> [!NOTE]
> Hierbei handelt es sich um die standard-Images, die von Azure bereitgestellt werden. Denken Sie daran, die Sie auch [erstellen und eigene benutzerdefinierte Images hochladen](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-custom-images) zum Erstellen von VMs basierend auf eindeutige Konfigurationen oder weniger häufig Versionen oder Verteilen von ein Betriebssystem installiert ist.