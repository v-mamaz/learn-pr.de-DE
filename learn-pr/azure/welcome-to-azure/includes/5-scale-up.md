Ihr Webserver ist betriebsbereit und wird ausgeführt, aber Sie erkennen, dass Sie mehr Computeleistung benötigen, um die Erfahrung für Ihre Benutzer noch attraktiver zu machen. Wie können Sie bewirken, dass Ihr virtueller Computer schneller ausgeführt wird?

In Ihrem Datencenter können Sie Ihren Webserver auf leistungsfähigere Hardware verlagern, um Leistungsprobleme zu lösen. Das Problem ist, dass Sie Ihr neues System kaufen, in Racks einbauen und betreiben müssen. Mit Azure ist die Antwort viel einfacher.

Erfahren Sie mehr über das Skalieren, bevor Sie Ihren virtuellen Computer auf eine leistungsfähigere Größe zentral hochskalieren.

## <a name="what-is-scale"></a>Was bedeutet „Skalierung“?

_Skalierung_ bezieht sich auf das Hinzufügen von Netzwerkbandbreite, Arbeitsspeicher, Speicher oder Computeleistung, um eine bessere Leistung zu erzielen.  

Möglicherweise haben Sie die Begriffe _zentrales Hochskalieren_ und _horizontales Hochskalieren_ schon einmal gehört.

Zentrales Hochskalieren oder vertikales Skalieren bedeutet, dass der Arbeitsspeicher, der Speicher oder die Computeleistung auf einem vorhandenen virtuellen Computer erhöht wird. Sie können einem Web- oder Datenbankserver z.B. zusätzlichen Arbeitsspeicher hinzufügen, um die Ausführung zu beschleunigen.

Horizontales Hochskalieren oder horizontales Skalieren bedeutet, dass zusätzliche virtuelle Computer Ihre Anwendung unterstützen. So können Sie beispielsweise viele virtuelle Computer erstellen, die auf genau die gleiche Weise konfiguriert sind, und einen Lastenausgleich verwenden, um die Arbeit auf sie zu verteilen.

> [!TIP]
> Die Cloud ist elastisch. Sie können Ihre Bereitstellung _zentral herunter-_ oder _horizontal herunterskalieren_, wenn Sie nur vorübergehend zentral hoch- oder horizontal hochskalieren müssen. Durch zentrales oder horizontales Herunterskalieren können Sie Kosten einsparen.<br><br>Ihre Cloudausgaben optimieren Sie mit **Azure Advisor** und **Azure Cost Management**. Mit diesen beiden Diensten können Sie einen unnötigen Verbrauch identifizieren und anschließend eine Skalierung auf die tatsächlich verwendete Kapazität vornehmen.

## <a name="scale-up-your-vm"></a>Zentrales Hochskalieren des virtuellen Computers

Erinnern Sie sich daran, dass Sie die Größe **Standard_DS2_v2** bei der Erstellung Ihres virtuellen Computers angegeben haben. Ihr virtueller Computer verfügt zurzeit über zwei virtuelle CPUs und 7 GB Arbeitsspeicher.

Wechseln Sie zur nächsten Größe **Standard_DS3_v2**. Ihr virtueller Computer verfügt dann über vier virtuelle CPUs und 14 GB Arbeitsspeicher.

::: zone pivot="windows-cloud"

1. Führen Sie `az vm resize` in Cloud Shell aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch. Ihr virtueller Computer wird während des Vorgangs neu gestartet.

1. Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.
    ```output
    Standard_DS3_v2
    ```

::: zone-end

::: zone pivot="linux-cloud"

1. Führen Sie `az vm resize` in Cloud Shell aus, um die Größe des virtuellen Computers auf **Standard_DS3_v2** zu erhöhen.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    Der Aktualisierungsvorgang nimmt etwa eine Minute in Anspruch. Ihr virtueller Computer wird während des Vorgangs neu gestartet.

1. Führen Sie `az vm show` aus, um sicherzustellen, dass der virtuelle Computer mit der neuen Größe ausgeführt wird.

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    Die neue VM-Größe (**Standard_DS3_v2**) wird angezeigt.
    ```output
    Standard_DS3_v2
    ```

::: zone-end

## <a name="summary"></a>Zusammenfassung

Gut gemacht! Mit nur einem Befehl ist Ihr virtueller Computer jetzt doppelt so leistungsfähig.

Zentrales und horizontales Hochskalieren sind zwei Möglichkeiten zur Leistungsverbesserung. Hier haben Sie Ihren virtuellen Computer zentral hochskaliert, um seine Computeleistung zu erhöhen.