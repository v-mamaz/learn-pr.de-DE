Ihr Unternehmen stellt Computeworkloads in verschiedenen Regionen bereit, damit Sie lokale Präsenz für Ihren verteilten Kundenstamm zeigen. 

Das Ziel ist, eine Containerregistrierung in jeder Region zu platzieren, in der Images ausgeführt werden. Durch diese Strategie werden netzwerknahe Vorgänge und dadurch schnelle, zuverlässige Übertragungen auf Imageebene gewährleistet. 

Mit der Georeplikation kann eine Azure-Containerregistrierung als zentrale Registrierung verwendet werden, die mehreren Regionen regionale Multimasterregistrierungen zur Verfügung stellt.

Eine Registrierung mit Georeplikation bietet folgende Vorteile:

- einzelner Registrierungs-/Image-/Tagname in mehreren Regionen verwendbar
- Netzwerknaher Registrierungszugriff in regionalen Bereitstellungen
- Keine zusätzlichen Ausgangsgebühren, da Images aus einer lokalen, replizierten Registrierung in der gleichen Region wie Ihr Containerhost abgerufen werden
- Zentrale Verwaltung einer Registrierung für mehrere Regionen

## <a name="replicate-an-image-to-multiple-locations"></a>Replizieren eines Images für mehrere Standorte

Sie verwenden den Azure CLI-Befehl `az acr replication create`, um Ihre Containerimages aus einer Region in eine andere zu replizieren. In diesem Beispiel wird eine Replikation für die Region `japaneast` erstellt. Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.

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

Der letzte Schritt. Sie können alle erstellten Replikate von Containerimages abrufen. Verwenden Sie den Befehl `az acr replication list` zum Abrufen dieser Liste. Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.

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

Bedenken Sie, dass Sie für das Auflisten der Imagereplikate nicht nur Azure CLI verwenden können. Wenn Sie im Azure-Portal `Replications` für eine Azure-Containerregistrierung auswählen, wird eine Karte mit den aktuellen Replikationen angezeigt. Containerimages können in zusätzliche Regionen repliziert werden, indem die Regionen auf der Karte ausgewählt werden.

![Replikationskarte für Container im Azure-Portal](../media/replication-map.png)

## <a name="clean-up-your-resources"></a>Bereinigen von Ressourcen
<!---TODO: Do we need to include cleanup for the free education tier?--->

Sie können nun die erstellten Ressourcen bereinigen, indem Sie die Ressourcengruppe löschen. Verwenden Sie hierzu den Befehl `az group delete`.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a>Zusammenfassung

Sie haben nun mit der Azure CLI erfolgreich ein Containerimage in mehreren Azure-Rechenzentren repliziert. 