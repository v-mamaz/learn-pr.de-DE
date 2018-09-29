Azure Container Registry ist ein verwalteter Docker-Registrierungsdienst, der auf Version 2.0 der Open Source-Docker-Registrierung basiert. Azure Container Registry-Instanzen sind privat und werden in Azure gehostet. Mit ihnen können Sie Images für alle Arten von Containerbereitstellungen erstellen, speichern und verwalten.

Containerimages können unter Verwendung von Container Registry mithilfe von Push/Pull übertragen werden. Hierfür kommt die Docker CLI oder Azure CLI zum Einsatz. Durch die Azure-Portal-Integration können Sie sich die Containerimages in Ihrer Containerregistrierung ansehen und sie so überprüfen. In verteilten Umgebungen kann das Georeplikationsfeature von Container Registry dazu verwendet werden, Containerimages für die lokalisierte Verteilung in mehreren Azure-Rechenzentren bereitzustellen.

Neben dem Speichern von Containerimages können mit Azure Container Registry Tasks auch Containerimages in Azure erstellt werden. ACR Tasks greift auf eine Standard-Dockerfile zurück, um ein Containerimage in Azure Container Registry zu erstellen und zu speichern. Lokale Docker-Tools sind dabei nicht notwendig. Mit ACR Tasks können Sie Buildvorgänge bei Bedarf ausführen oder aber für Containerimages vollständig mithilfe von DevOps-Prozessen und -Tools automatisieren.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul

- Bereitstellen einer Azure-Containerregistrierung
- Erstellen eines Containerimage mithilfe von Azure Container Registry Tasks
- Bereitstellen des Containers in einer Azure-Containerinstanz
- Replizieren des Containerimage für mehrere Azure-Rechenzentren

## <a name="prerequisites"></a>Voraussetzungen  

- Keine