Als bewährte Methode ermöglicht die Platzierung einer Containerregistrierung in jeder Region, in der Images ausgeführt werden, netzwerknahe Vorgänge, die schnelle und zuverlässige Übertragungen auf Imageebene gestatten. Mit der Georeplikation kann eine Azure-Containerregistrierung als zentrale Registrierung verwendet werden, die mehreren Regionen regionale Multimasterregistrierungen zur Verfügung stellt.

Eine Registrierung mit Georeplikation bietet folgende Vorteile:

* einzelner Registrierungs-/Image-/Tagname in mehreren Regionen verwendbar
* netzwerknaher Registrierungszugriff über regionale Bereitstellungen
* keine zusätzlichen Ausgangsgebühren, da Images aus einer lokalen, replizierten Registrierung in derselben Region wie Ihr Containerhost mithilfe von Pull übertragen werden
* zentrale Verwaltung einer Registrierung für mehrere Regionen

## <a name="replicate-image-to-multiple-locations"></a>Replizieren eines Images für mehrere Standorte

Verwenden Sie den `az acr replication create`-Befehl, um Ihre Containerimages für eine andere Region zu replizieren. In diesem Beispiel wird eine Replikation für die Region `japaneast` erstellt. Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.

```azurecli
az acr replication create --registry <acrName> --location japaneast
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```console
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myACR0007/replications/japaneast",
  "location": "japaneast",
  "name": "japaneast",
  "provisioningState": "Succeeded",
  "resourceGroup": "myresourcegroup",
  "status": {
    "displayStatus": "Syncing",
    "message": null,
    "timestamp": "2018-08-15T20:22:09.275792+00:00"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries/replications"
}
```

Verwenden Sie den Befehl `az acr replication list`, um sich eine Liste mit allen Replikaten des Containerimages anzeigen zu lassen. Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.

```azurecli
az acr replication list --registry <acrName> --output table
```

Die Ausgabe sollte in etwa wie folgt aussehen:

```console
NAME       LOCATION    PROVISIONING STATE    STATUS
---------  ----------  --------------------  --------
japaneast  japaneast   Succeeded             Ready
eastus     eastus      Succeeded             Ready
```

Obwohl das Azure-Portal in dieser Übung nicht genutzt wurde, bietet es sich an, dessen Benutzeroberfläche aufzurufen.

Wenn Sie im Azure-Portal `Replications` für eine Azure-Containerregistrierung auswählen, wird eine Karte mit den aktuellen Replikationen angezeigt. Containerimages können für zusätzliche Regionen repliziert werden, indem letztere auf der Karte ausgewählt werden.

![Replikationskarte für Container im Azure-Portal](../media/replication-map.png)

## <a name="clean-up"></a>Bereinigen

Dies ist die letzte Einheit des Azure Container Registry-Lernmoduls. Sie können nun die erstellten Ressourcen bereinigen, indem Sie die Ressourcengruppe löschen. Verwenden Sie hierzu den `az group delete`-Befehl.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a>Zusammenfassung

In diesem Modul haben Sie ein Containerimage für mehrere Azure-Regionen mithilfe der Azure CLI repliziert.