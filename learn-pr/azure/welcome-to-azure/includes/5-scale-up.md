Ihr Webserver ist betriebsbereit und wird ausgeführt, aber Sie erkennen, dass Sie mehr Computeleistung benötigen, um die Erfahrung für Ihre Benutzer noch attraktiver zu machen. Wie können Sie bewirken, dass Ihr virtueller Computer schneller ausgeführt wird?

In Ihrem Datencenter können Sie Ihren Webserver auf leistungsfähigere Hardware verlagern, um Leistungsprobleme zu lösen. Das Problem ist, dass Sie Ihr neues System kaufen, in Racks einbauen und betreiben müssen. Mit Azure ist die Antwort viel einfacher.

Sie müssen Ihren virtuellen Computer nur auf eine leistungsfähigere Größe zentral hochskalieren. Bevor Sie die Größe Ihres virtuellen Computers ändern, müssen Sie ihn herunterfahren oder seine Zuordnung aufheben.

Definieren wir zunächst, was „Skalierung“ bedeutet und was geschieht, wenn Sie die Zuordnung Ihres virtuellen Computers aufheben.

## <a name="what-is-scale"></a>Was bedeutet „Skalierung“?

_Skalierung_ bezieht sich auf das Hinzufügen von Netzwerkbandbreite, Arbeitsspeicher, Speicher oder Computeleistung, um eine bessere Leistung zu erzielen.  

Möglicherweise haben Sie die Begriffe _zentrales Hochskalieren_ und _horizontales Hochskalieren_ schon einmal gehört.

Zentrales Hochskalieren oder vertikales Skalieren bedeutet, dass der Arbeitsspeicher, der Speicher oder die Computeleistung auf einem vorhandenen virtuellen Computer erhöht wird. Sie können einem Web- oder Datenbankserver z.B. zusätzlichen Arbeitsspeicher hinzufügen, um die Ausführung zu beschleunigen.

> [!TIP]
> Sie können Ihr System auch _zentral herunterskalieren_, wenn Sie es nur vorübergehend zentral hochskalieren mussten.

Horizontales Hochskalieren oder horizontales Skalieren bedeutet, dass zusätzliche virtuelle Computer Ihre Anwendung unterstützen. So können Sie beispielsweise viele virtuelle Computer erstellen, die auf genau die gleiche Weise konfiguriert sind, und Lastenausgleich verwenden, um die Arbeit auf sie zu verteilen.

## <a name="what-is-deallocation"></a>Was bedeutet „Aufhebung der Zuordnung“?

Die Aufhebung der Zuordnung ist der Vorgang, bei dem Ihr virtueller Computer heruntergefahren wird und seine Computeressourcen freigibt.

Wenn Sie Ihren PC am Arbeitsplatz oder zu Hause herunterfahren, schließt das Betriebssystem alle Programme und weist dann die Energieverwaltungshardware an, den Computer auszuschalten.

Das Aufheben der Zuordnung eines virtuellen Computers ist ähnlich. Nachdem Ihr virtueller Computer heruntergefahren wurde, gibt Azure die Hardware erneut frei, die für ihn verwendet wurde. Ihre Datenträger und Ihr Speicher bleiben intakt. Wenn Sie Ihren virtuellen Computer erneut starten, setzen Sie dort an, wo Sie aufgehört haben, genau wie bei Ihrem PC.

Wenn die Zuordnung aufgehoben ist, zahlen Sie nicht für die Compute- und Netzwerkressourcen, die der virtuelle Computer verwendet. Sie zahlen zwar weiterhin für alle zugehörigen Datenträger, die sich im Speicher befinden, aber die Gesamtkosten sind wesentlich geringer als für einen ausgeführten virtuellen Computer.

Hier heben Sie die Zuordnung Ihres virtuellen Computers kurz auf, damit Sie seine Größe ändern können. Sie können die Zuordnung Ihrer virtuellen Computer aber auch über einen längeren Zeitraum hinweg aufheben, um Kosten zu sparen. Angenommen, Sie nutzen eine Reihe von virtuellen Computern während der Arbeitszeiten zu Testzwecken. Sie können planen, dass die Zuordnung Ihrer virtuellen Computer Nachts und an den Wochenenden aufgehoben wird. Wenn Sie Überstunden machen müssen, können Sie diese virtuellen Computer manuell erneut starten.

## <a name="scale-up-your-vm"></a>Zentrales Hochskalieren des virtuellen Computers

Erinnern Sie sich daran, dass Sie die Größe **Standard_DS2_v2** bei der Erstellung Ihres virtuellen Computers angegeben haben. Ihr virtueller Computer verfügt zurzeit über zwei virtuelle CPUs und 7 GB Arbeitsspeicher.

Wechseln Sie zur nächsten Größe **Standard_DS3_v2**. Ihr virtueller Computer verfügt dann über vier virtuelle CPUs und 14 GB Arbeitsspeicher.

::: zone pivot="windows-cloud"

1. Führen Sie `az vm deallocate` in Cloud Shell aus, um die Zuordnung Ihres virtuellen Computers aufzuheben oder ihn zu beenden.

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    Dieser Vorgang nimmt einige Minuten in Anspruch.
1. Führen Sie `az vm resize` aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --size Standard_DS3_v2
    ```
    Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch.
1. Führen Sie `az vm start` aus, um Ihren virtuellen Computer neu zu starten.

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    Der Vorgang nimmt etwa eine Minute in Anspruch.
1. Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

::: zone pivot="linux-cloud"

1. Führen Sie `az vm deallocate` in Cloud Shell aus, um die Zuordnung Ihres virtuellen Computers aufzuheben oder ihn zu beenden.

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    Dieser Vorgang nimmt einige Minuten in Anspruch.
1. Führen Sie `az vm resize` aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --size Standard_DS3_v2
    ```
    Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch.
1. Führen Sie `az vm start` aus, um Ihren virtuellen Computer neu zu starten.

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    Der Vorgang nimmt etwa eine Minute in Anspruch.
1. Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

> [!NOTE]
> Standardmäßig weist Azure Ihrem virtuellen Computer beim Beenden und Neustarten eine neue öffentliche IP-Adresse zu. Dies ist zu Lernzwecken vertretbar. In der Praxis können Sie eine öffentliche IP-Adresse reservieren, die Ihrem virtuellen Computer selbst dann zugeordnet bleibt, wenn Ihr virtueller Computer neu gestartet wird.

## <a name="summary"></a>Zusammenfassung

Gut gemacht! Mit nur wenigen Befehlen ist Ihr virtueller Computer jetzt doppelt so leistungsfähig.

Zentrales und horizontales Hochskalieren stellen zwei Möglichkeiten dar, die Leistung zu steigern. Hier haben Sie Ihren virtuellen Computer zentral hochskaliert, um seine Computeleistung zu erhöhen.

Sie heben die Zuordnung eines virtuellen Computers auf, bevor Sie seine Größe ändern können. Sie können die Zuordnung Ihrer virtuellen Computer auch aufheben, wenn sie nicht verwendet werden, um Kosten zu sparen.