Die zu erstellende Anwendung ist eine plattformübergreifende mobile App, die mit einer Azure-Funktion kommuniziert, um Ihren Standort zu teilen. In dieser Einheit erstellen Sie mit Visual Studio die leere mobile App und installieren ein NuGet-Paket mit einer API zum Abrufen des Benutzerstandorts.

## <a name="create-the-xamarinforms-project"></a>Erstellen des Xamarin.Forms-Projekts

1. Wählen Sie in Visual Studio *Datei > Neu > Projekt* aus.

1. Wählen Sie in der Struktur links *Visual C# > Plattformübergreifend* aus, und klicken Sie dann im Arbeitsbereich in der Mitte auf *Mobile App (Xamarin.Forms)*.

1. Geben Sie der Projektmappe den Namen „ImHere“.

1. Wählen Sie einen geeigneten Speicherort für die Projektmappe.

    > Wenn Sie dieses Modul lokal unter Windows ausführen und eine Entwicklung für Android planen, sollte der Pfad so kurz wie möglich gehalten werden. Für das Android SDK gelten Längenbeschränkungen, deshalb sollte ein möglichst kurzer Stammpfad gewählt werden.

1. Klicken Sie auf **OK**.

    ![Dialogfeld „Neue Projektmappe“](../media/2-new-solution-dialog.png)

1. Wählen Sie im Dialogfeld **Neue plattformübergreifende App** die Vorlage *Leere App* aus.

1. Für dieses Modul erstellen Sie eine UWP-App. Deaktivieren Sie deshalb iOS und Android, und lassen Sie UWP aktiviert.

    > Wenn Sie eine lokale Ausführung planen, können Sie Android aktiviert lassen, weil das Android SDK als Teil der Workload *Mobile-Entwicklung mit .NET* in Visual Studio installiert wird. Wenn Sie auch für iOS entwickeln möchten, ist eine Kopplung mit einem macOS-Build-Agent erforderlich. Weitere Informationen hierzu finden Sie in der [Xamarin iOS-Dokumentation](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/).

1. Wählen Sie für *Codefreigabestrategie* die Option **.NET Standard** aus.

1. Klicken Sie auf **OK**.

    ![Dialogfeld zum Konfigurieren der neuen Projektmappe](../media/2-configure-solution-dialog.png)

Visual Studio erstellt zwei Projekte für Sie: eine UWP-App namens `ImHere.UWP` und eine .NET Standard-Bibliothek `ImHere`. Xamarin.Forms-Apps setzen umfassen zwei Bestandteile – mindestens ein plattformspezifisches App-Projekt und (mindestens) eine .NET Standard-Bibliothek. Die plattformspezifischen App-Projekte enthalten den plattformspezifischen Code, der zum Ausführen einer App auf der jeweiligen Plattform benötigt wird. Diese Projekte starten anschließend eine Xamarin.Forms-App, die in einer plattformübergreifenden .NET Standard-Bibliothek definiert ist. Sie entwickeln Ihre App in plattformübergreifendem Code, und zur Laufzeit werden alle erstellten Benutzerschnittstellen in die relevanten plattformspezifischen Benutzeroberflächenkomponenten übersetzt.

## <a name="adding-xamarinessentials"></a>Hinzufügen von „Xamarin.Essentials“

Die UWP-, Android- und iOS-Plattformen bieten zahlreiche ähnliche Funktionen, die das Betriebssystem und die Hardware nutzen. Trotz dieser Ähnlichkeiten sind die APIs sehr unterschiedlich. Zur Verwendung dieser APIs aus plattformübergreifendem Code muss plattformspezifischer Code in Ihren App-Projekten geschrieben werden, den Sie für Ihre .NET Standard-Bibliotheken verfügbar machen. [Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/) ist ein NuGet-Paket, das eine plattformübergreifende Abstraktion einiger dieser APIs bietet – einschließlich der Geolocation-APIs, die Sie in Ihrer App zum Abrufen des Benutzerstandorts verwenden.

1. Klicken Sie im Projektmappen-Explorer von Visual Studio mit der rechten Maustaste auf die `ImHere`-Lösung, und wählen Sie *NuGet-Pakete für Projektmappe verwalten* aus.

1. Wählen Sie die Registerkarte **Durchsuchen** aus, und suchen Sie nach „Xamarin.Essentials“. Dieses Paket ist zurzeit als Vorabrelease-NuGet-Paket verfügbar, aktivieren Sie deshalb die Option *Vorabversion einbeziehen*.

1. Wählen Sie das NuGet-Paket **Xamarin.Essentials** aus.

1. Aktivieren Sie in der Projektliste auf der rechten Seite sämtliche Ihrer Projekte.

1. Klicken Sie auf die Schaltfläche **Installieren**, um das NuGet-Paket zu installieren. Sie müssen die Lizenz akzeptieren, um den Vorgang fortzusetzen.

    ![Hinzufügen des NuGet-Pakets „Xamarin.Essentials“ zu allen Projekten in der Projektmappe](../media/2-add-essentials-nuget.png)

    > Wenn Sie dieses Modul lokal ausführen und Android als Zielplattform verwenden möchten, müssen Sie einige zusätzliche Einrichtungsschritte ausführen. Weitere Informationen finden Sie in der [Dokumentation für die ersten Schritte mit Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/get-started?context=xamarin%2Fios&tabs=windows%2Candroid).

## <a name="building-and-running-the-app"></a>Erstellen und Ausführen der App

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das `ImHere.UWP`-Projekt, und wählen Sie *Als Startprojekt festlegen* aus.

1. Legen Sie die Buildkonfiguration auf **Debuggen**, die Plattform auf **x86** und das Gerät für die Ausführung auf **Lokaler Computer** fest.

    ![Festlegen der x86-Debugkonfiguration zur Ausführung auf dem lokalen Gerät](../media/2-debug-configuration.png)

1. Beginnen Sie mit dem Debuggen der App.

    ![App bei der Ausführung](../media/2-debuging-app.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine neue plattformübergreifende mobile Xamarin.Forms-App erstellt und das NuGet-Paket „Xamarin.Essentials“ hinzugefügt. Als Nächstes lernen Sie, wie Sie die Benutzeroberfläche und Logik der mobilen App entwickeln.