In dieser Einheit entwerfen und erstellen Sie eine neue ASP.NET-Webanwendung und führen sie auf dem lokalen Computer aus.

## <a name="create-a-project"></a>Erstellen eines Projekts

### <a name="visual-studio-for-windows"></a>Visual Studio für Windows

Im ersten Schritt wird Visual Studio gestartet und eine lokale ASP.NET Core-Webanwendung erstellt.

1. Klicken Sie auf der Startseite von Visual Studio auf **Datei** und anschließend auf **Neu** > **Projekt...**.

1. Klicken Sie im linken Bereich des Dialogfelds **Neues Projekt** auf **Web**.

1. Klicken Sie im mittleren Bereich auf **ASP.NET Core-Webanwendung**.

1. Geben Sie am unteren Rand des Dialogfelds im Feld **Name** den Namen **Alpine Ski House** ein.

1. Wählen Sie einen **Speicherort** für die neue Projektmappe aus.

1. Klicken Sie auf die Schaltfläche **OK**, um Ihr Projekt zu erstellen.

1. Im Dialogfeld **Neue ASP.NET Core-Webanwendung** wird Ihnen eine Auswahl von Startvorlagen angezeigt. Wählen Sie für diese Übung **Webanwendung** aus, und klicken Sie dann zum Erstellen Ihres Projekts auf **OK**.

    ![Dialogfeld „Neues Projekt“](../media-draft/3-aspnet-templates.png)

    > [!NOTE]
    > Sie können je nach Webentwicklungsanforderungen auch andere Startvorlagen in diesem Dialogfeld auswählen. Am oberen Rand des Dialogfelds können Sie auch die ASP.NET Core-Version auswählen. Wählen Sie mindestens ASP.NET Core 2.0 aus.

1. Sie verfügen nun über eine neue Projektmappe für eine ASP.NET Core-Webanwendung.

    ![Dialogfeld „Neues Projekt“](../media-draft/3-new-solution.png)

### <a name="visual-studio-mac"></a>Visual Studio für Mac

1. Klicken Sie auf der Startseite von Visual Studio auf **Datei** und anschließend auf **Neu** > **Projekt...**.

1. Wählen Sie unter **.NET Core** eine **ASP.NET Core-Web-App** aus, und klicken Sie dann auf **Weiter**.

1. Geben Sie unter **Projektname** die Zeichenfolge **AlpineSkiHouse** ein. Dies sollte auch den Namen der Projektmappe auffüllen.

1. Wählen Sie für das Projekt einen **Speicherort** auf Ihrem lokalen Computer aus.

1. Klicken Sie auf **Erstellen**.

## <a name="build-and-test-on-your-local-machine"></a>Erstellen und Testen auf dem lokalen Computer

Nun erstellen und testen Sie das neue Projekt auf dem lokalen Computer, um vor der Bereitstellung in Azure sicherzustellen, dass es lokal erstellt und bereitgestellt wird.

1. Drücken Sie **F5**, um die App im Debugmodus auszuführen, oder **STRG+F5**, um sie ohne Debugger auszuführen.

    ![Dialogfeld „Neues Projekt“](../media-draft/3-webapp-launch.png)

Visual Studio startet IIS Express und führt die App aus. Wenn Visual Studio ein Webprojekt erstellt, wird ein nach dem Zufallsprinzip ausgewählter Port für den Webserver verwendet. In der vorherigen Abbildung wird die Portnummer 44381 verwendet. Wenn Sie die App ausführen, wird wahrscheinlich eine andere Portnummer angezeigt.

> [!TIP]
> Wenn Sie die App mit **STRG+F5** (Modus oder Debugger) starten, können Sie Codeänderungen vornehmen, die Datei speichern, den Browser aktualisieren und die Codeänderungen anzeigen. Viele Entwickler bevorzugen den Modus ohne Debugger, um die App schnell starten und Änderungen anzeigen zu können.

> [!IMPORTANT]
> Vielleicht ist Ihnen der Abschnitt am oberen Rand der Webseite aufgefallen, der für Ihre Datenschutz- und Cookienutzungsrichtlinie vorgesehen ist. Klicken Sie auf **Akzeptieren**, um der Nachverfolgung zuzustimmen. Diese App verfolgt keine persönlichen Informationen nach. Der vorlagengenerierte Code enthält Ressourcen zur Einhaltung der Datenschutz-Grundverordnung (DSGVO).

## <a name="summary"></a>Zusammenfassung

Im ersten Einrichtungsschritt wird Ihre ASP.NET-Website erstellt und lokal ausgeführt. Nachdem Sie Ihre Website nun erstellt haben, können Sie sie in Azure bereitstellen.
