In diesem Modul haben Sie mehr über die Entscheidungen erfahren, die Sie vor der Erstellung eines virtuellen Computers treffen müssen. Zu diesen Entscheidungen zählen Aspekte wie die Größe des virtuellen Computers, die Typen der verwendeten Datenträger, das ausgewählte Betriebssystemimage und die Typen der erstellten Ressourcen.

Darüber hinaus haben Sie die Optionen zum Erstellen und Verwalten virtueller Computer in Azure kennengelernt. Sie haben gesehen, wie einfach virtuelle Computer über das Portal erstellt und verwaltet werden können, und wann Resource Manager-Vorlagen, PowerShell, die Azure CLI und das Azure Client SDK verwendet werden müssen.

Abschließend haben Sie sich die verfügbaren Erweiterungen und Dienste angesehen, mit denen Ihre virtuellen Computer leichter verwaltet werden können.

## <a name="clean-up-your-resources"></a>Bereinigen von Ressourcen

Beachten Sie, dass für virtuelle Computer weiterhin eine monatliche Gebühr anfällt, solange Sie Hardware reserviert haben (selbst dann, wenn das Betriebssystem heruntergefahren ist) und Speicherplatz für Datenträger verwendet wird. Sie können den virtuellen Computer im Portal ausschalten, um die Abrechnung für Computedienste zu beenden. Für den Speicher fallen jedoch weiterhin Kosten an. Wenn Sie Ressourcen zu Testzwecken erstellen, können Sie diese ohne großen Aufwand entfernen, indem Sie die **Ressourcengruppe** löschen, zu der diese gehören.

> [!TIP]
> Stellen Sie für eine problemlose Verwaltung sicher, dass sich alle Ihre Testressourcen in derselben Ressourcengruppe befinden.

Wenn Sie eine Ressourcengruppe löschen möchten, suchen Sie diese über den Bereich **Ressourcengruppen** (klicken Sie dazu in der Randleiste auf **Ressourcengruppen**). Klicken Sie anschließend neben der Ressourcengruppe auf das Menü mit den Auslassungspunkten (`...`), und wählen Sie, wie hier dargestellt, aus dem Popupmenü die Option **Ressourcengruppe löschen** aus.

![Löschen einer Ressourcengruppe](../media-draft/7-delete-rgs.png)