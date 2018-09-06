Da sich Ihre App nun einsatzbereit auf Ihrem lokalen Computer befindet, kann sie in Azure veröffentlicht werden. 

In dieser Übung entwerfen und erstellen Sie eine neue ASP.NET-Webanwendung und führen sie auf dem lokalen Computer aus.

## <a name="create-a-new-project"></a>Erstellen eines neuen Projekts

### <a name="visual-studio-for-windows"></a>Visual Studio für Windows

Der erste Schritt ist, Visual Studio zu starten und eine lokale ASP.NET Core-Webanwendung zu erstellen.

1. Wählen Sie auf der Startseite von Visual Studio **Datei** aus, und klicken Sie dann auf **Neu** und **Projekt...**.

1. Wählen Sie im Dialogfeld **Neues Projekt** im linken Bereich **Web** aus.

1. Klicken Sie im mittleren Bereich auf **ASP.NET Core-Webanwendung**.

1. Geben Sie am unteren Rand des Dialogfelds im Feld **Name** als Namen **Alpine Ski House** ein.

1. Wählen Sie einen **Speicherort** für die neue Projektmappe aus.

1. Klicken Sie auf die Schaltfläche **OK**, um Ihr Projekt zu erstellen.

1. Im Dialogfeld **Neue ASP.NET Core-Webanwendung** wird Ihnen eine Auswahl von Startvorlagen angezeigt. Wählen Sie für diese Übung **Webanwendung** aus, und klicken Sie dann zum Erstellen Ihres Projekts auf **OK**.

    ![Dialogfeld „Neues Projekt“](../media-draft/3-aspnet-templates.png)

    > [!NOTE]
    > Sie können auch je nach Ihren Webentwicklungsanforderungen verschiedene Startvorlagen in diesem Dialogfeld auswählen. Am oberen Rand des Dialogfelds können Sie auch die ASP.NET Core-Version auswählen. Wählen Sie ASP.NET Core 2.0 oder höher aus.

1. Sie sollten nun über Ihre neue ASP.NET Core-Webanwendungs-Projektmappe verfügen.

    ![Dialogfeld „Neues Projekt“](../media-draft/3-new-solution.png)

### <a name="visual-studio-mac"></a>Visual Studio für Mac

1. Wählen Sie auf der Startseite von Visual Studio **Datei** aus, und klicken Sie dann auf **Neu** und **Projekt...**.

1. Wählen Sie unter **.NET Core** eine **ASP.NET Core-Web-App** aus, und klicken Sie dann auf **Weiter**.

1. Geben Sie als **Projektname** **AlpineSkiHouse** ein. Damit sollte auch der Projektmappenname automatisch aufgefüllt werden.

1. Wählen Sie einen **Speicherort** auf Ihrem lokalen Computer für das Projekt aus.

1. Klicken Sie auf **Erstellen**.

## <a name="build-and-test-on-your-local-machine"></a>Erstellen und Testen auf dem lokalen Computer

Nun erstellen und testen Sie das neue Projekt auf dem lokalen Computer, um vor der Bereitstellung in Azure sicherzustellen, dass es lokal erstellt und bereitgestellt wird.

1. Drücken Sie **F5** zum Ausführen der App im Debugmodus oder **STRG + F5** zum Ausführen ohne Anfügen des Debuggers.

    ![Dialogfeld „Neues Projekt“](../media-draft/3-webapp-launch.png)

Visual Studio startet IIS Express und führt die App aus. Wenn Visual Studio ein Webprojekt erstellt, wird ein zufälliger Port für den Webserver verwendet. In der vorherigen Abbildung ist die Portnummer 44381. Wenn Sie die App ausführen, wird wahrscheinlich eine andere Portnummer angezeigt.

> [!TIP]
> Wenn Sie die App mit **STRG + F5** (Nicht-Debugmodus) starten, können Sie Codeänderungen vornehmen, die Datei speichern, den Browser aktualisieren und die Codeänderungen anzeigen. Viele Entwickler bevorzugen den Nicht-Debugmodus, um die App schnell zu starten und Änderungen anzuzeigen.

> [!IMPORTANT]
> Vielleicht ist Ihnen der Abschnitt am oberen Rand der Webseite aufgefallen, der für Ihre Datenschutz- und Cookienutzungsrichtlinien vorgesehen ist. Wählen Sie **Akzeptieren** aus, um der Nachverfolgung zuzustimmen. Diese App verfolgt keine persönlichen Informationen nach. Der vorlagengenerierte Code enthält Ressourcen zur Einhaltung der Datenschutz-Grundverordnung (DSGVO).

## <a name="summary"></a>Zusammenfassung

Der erste Schritt, Ihre ASP.NET-Website in Betrieb zu nehmen, ist das lokale Erstellen und Ausführen. Da Sie Ihre Website nun erstellt haben, können Sie sie in Azure bereitstellen.
