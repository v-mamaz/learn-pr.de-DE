Ihre Webserver ausgeführt wird, und wird ausgeführt, aber Sie nutzen, benötigen Sie mehr rechenleistung, um die Erfahrung für Ihre Benutzer hervorragend ist. Wie können Sie Ihren virtuellen Computer schneller ausgeführt?

In Ihrem Rechenzentrum können Sie Ihrem Webserver zu leistungsstärkerer Hardware zum Lösen von Leistungsproblemen verschieben. Das Problem ist, dass Sie kaufen, ein rack und schalten Sie das neue System müssen. Mit Azure ist die Antwort viel einfacher.

Jetzt müssen Sie Ihren virtuellen Computer auf eine leistungsfähigere Größe hochskalieren. Bevor Sie Ihre VM Größe ändern, müssen Sie ihn schließen oder Zuordnung aufheben.

Zuerst definieren wir, welche Skalierung bedeutet und was geschieht, wenn Sie die Zuordnung Ihres virtuellen Computers aufheben.

## <a name="what-is-scale"></a>Was ist die Skalierung?

_Skalierung_ bezieht sich auf das Hinzufügen von Netzwerkbandbreite, Arbeitsspeicher, Speicher oder rechenleistung, um eine bessere Leistung zu erzielen.  

Sie haben die Begriffe gehört _zentral hochskalieren_ und _horizontal hochskalieren_.

Zentral hochzuskalieren oder vertikale Skalierung, bedeutet, dass den Arbeitsspeicher, Speicher, erhöhen oder zu computeleistung auf einem vorhandenen virtuellen Computer. Sie können eine Web- oder Datenbank-Server, um Ausführung zu beschleunigen, z. B. zusätzlichen Arbeitsspeicher hinzufügen.

> [!TIP]
> Sie können auch _Herunterskalieren_ Ihr System, wenn Sie nur vorübergehend zentral hochskalieren.

Horizontales hochskalieren oder horizontale Skalierung, bedeutet, dass zusätzliche virtuelle Computer auf Ihre Anwendung zu unterstützen. Z. B. können Sie viele virtuelle Computer so konfiguriert, auf genau die gleiche Weise erstellen und verwenden einen Load Balancer, um die Arbeit auf sie verteilen.

## <a name="what-is-deallocation"></a>Was ist die Aufhebung der Zuordnung?

Aufhebung der Zuordnung ist der Prozess, der Ihr virtueller Computer heruntergefahren und die computeressourcen frei.

Wenn Sie Ihren PC am Arbeitsplatz oder zu Hause Herunterfahren, wird das Betriebssystem schließt alle Programme und benachrichtigt, die Power Management Hardware Strom ausschalten.

Aufheben der Zuordnung eines virtuellen Computers entspricht. Nachdem Ihr virtueller Computer heruntergefahren wird, gibt Azure die Hardware verwendet, um die Leistungsfähigkeit frei. Ihre Datenträger für Daten und Speicher bleiben intakt. Wenn Sie Ihren virtuellen Computer starten, sichern, wird Sie weitermachen, wo Sie aufgehört, wie mit Ihrem PC.

Aufhebung der Zuordnung, sind Sie nicht für die Compute und Netzwerk-Ressourcen in Rechnung gestellt, die dem virtuellen Computer verwendet. Sie bezahlen für alle zugeordneten Datenträger im Speicher befindet, aber die Gesamtkosten für die ist wesentlich geringer, als es der Fall wäre, wenn die VM ausgeführt wurden.

Hier müssen Sie Ihren virtuellen Computer kurz Zuordnung aufheben, damit Sie die Größe anpassen können. Aber Sie können auch heben Sie die Zuordnung Ihrer virtuellen Computer für einen längeren Zeitraum, um Kosten zu sparen. Angenommen, Sie haben eine Bank von virtuellen Computern, die Sie während der Arbeitszeiten zu Testzwecken verwenden. Sie können Ihre virtuellen Computer automatisch auf Nächte und Wochenenden freigegeben werden, planen. Wenn Sie spät bleiben müssen, können Sie diese manuell neu starten.

## <a name="scale-up-your-vm"></a>Zentrales hochskalieren Ihres virtuellen Computers

Denken Sie daran, dass Sie die Größe angegeben **"standard_ds2_v2"** bei der Erstellung Ihres virtuellen Computers. Ihr virtueller Computer verfügt derzeit zwei virtuellen CPUs und 7 GB Arbeitsspeicher.

Lassen Sie uns auf die Größe, erhöhen Sie die **Standard_DS3_v2**. Ihr virtueller Computer müssen vier virtuelle CPUs und 14 GB Arbeitsspeicher.

::: zone pivot="windows-cloud"

1. Führen Sie in Cloud Shell, `az vm deallocate` freizugeben oder zu beenden, Ihren virtuellen Computer.

    ```azurecli
    az vm deallocate \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM
    ```
    Der Vorgang dauert ein paar Minuten in Anspruch.
1. Führen Sie `az vm resize` Erhöhen der Größe des virtuellen Computers **Standard_DS3_v2**.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM \
      --size Standard_DS3_v2
    ```
    Der Aktualisierungsvorgang dauert etwa eine Minute.
1. Führen Sie `az vm start` Ihrer virtuellen Computer neu starten.

    ```azurecli
    az vm start \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM
    ```
    Der Vorgang dauert ungefähr eine Minute.
1. Führen Sie `az vm show` um sicherzustellen, dass die neue Größe ausgeführt wird.

    ```azurecli
    az vm show \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    Sie finden Sie unter der neuen VM-Größe, **Standard_DS3_v2**.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

::: zone pivot="linux-cloud"

1. Führen Sie in Cloud Shell, `az vm deallocate` freizugeben oder zu beenden, Ihren virtuellen Computer.

    ```azurecli
    az vm deallocate \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM
    ```
    Der Vorgang dauert ein paar Minuten in Anspruch.
1. Führen Sie `az vm resize` Erhöhen der Größe des virtuellen Computers **Standard_DS3_v2**.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM \
      --size Standard_DS3_v2
    ```
    Der Aktualisierungsvorgang dauert etwa eine Minute.
1. Führen Sie `az vm start` Ihrer virtuellen Computer neu starten.

    ```azurecli
    az vm start \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM
    ```
    Der Vorgang dauert ungefähr eine Minute.
1. Führen Sie `az vm show` um sicherzustellen, dass die neue Größe ausgeführt wird.

    ```azurecli
    az vm show \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    Sie finden Sie unter der neuen VM-Größe, **Standard_DS3_v2**.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

> [!NOTE]
> Standardmäßig weist Azure eine neue öffentliche IP-Adresse Ihres virtuellen Computers beim Beenden und starten Sie ihn neu. Dies ist in Ordnung zu Lernzwecken. In der Praxis können Sie eine öffentliche IP-Adresse, die bleibt mit Ihrem virtuellen Computer reservieren, selbst wenn Ihr virtueller Computer neu gestartet wird.

## <a name="summary"></a>Zusammenfassung

Gute Arbeit! Mit nur wenigen Befehlen ist der virtuellen Computer jetzt doppelt so leistungsfähig.

Hochskalieren und horizontales Skalieren werden zwei Möglichkeiten, um die Leistung zu erhöhen. Hier hochskaliert Sie Ihrer VM, die rechenleistung zu erhöhen.

Sie heben die Zuordnung eines virtuellen Computers auf, bevor Sie die Größe anpassen können. Sie können auch Ihre virtuellen Computer Zuordnung aufheben, wenn sie nicht verwendet, um Kosten zu sparen sind.