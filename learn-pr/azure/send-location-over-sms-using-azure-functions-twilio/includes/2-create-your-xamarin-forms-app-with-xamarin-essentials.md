Die zu erstellende Anwendung ist eine plattformübergreifende mobile App, die mit einer Azure-Funktion kommuniziert, um Ihren Standort zu teilen. In dieser Einheit erstellen Sie mit Visual Studio die leere mobile App und installieren ein NuGet-Paket mit einer API zum Abrufen des Benutzerstandorts.

## <a name="create-the-xamarinforms-project"></a>Erstellen des Xamarin.Forms-Projekts

1. Wählen Sie in Visual Studio *Datei > Neu > Projekt* aus.

1. Wählen Sie in der Struktur links *Visual C# > Plattformübergreifend* aus, und klicken Sie dann im Arbeitsbereich in der Mitte auf *Mobile App (Xamarin.Forms)*.

1. Geben Sie der Projektmappe den Namen „ImHere“.

1. Wählen Sie einen geeigneten Speicherort für die Projektmappe aus.

1. Klicken Sie auf **OK**.

    ![Dialogfeld „Neue Projektmappe“](../media/2-new-solution-dialog.png)

1. Wählen Sie im Dialogfeld **Neue plattformübergreifende App** die Vorlage *Leere App* aus.

1. Für dieses Modul erstellen Sie eine UWP-App. Deaktivieren Sie deshalb iOS und Android, und lassen Sie UWP aktiviert.

1. Wählen Sie für *Codefreigabestrategie* die Option **.NET Standard** aus.

1. Klicken Sie auf **OK**.

    ![Dialogfeld zum Konfigurieren der neuen Projektmappe](../media/2-configure-solution-dialog.png)

Visual Studio erstellt zwei Projekte für Sie: eine UWP-App namens `ImHere.UWP` und eine .NET Standard-Bibliothek `ImHere`. Xamarin.Forms-Apps umfassen zwei Bestandteile – mindestens ein plattformspezifisches App-Projekt und (mindestens) eine .NET Standard-Bibliothek. Die plattformspezifischen App-Projekte enthalten den plattformspezifischen Code, der zum Ausführen einer App auf der jeweiligen Plattform benötigt wird. Diese Projekte starten anschließend eine Xamarin.Forms-App, die in einer plattformübergreifenden .NET Standard-Bibliothek definiert ist. Sie entwickeln Ihre App in plattformübergreifendem Code, und zur Laufzeit werden alle erstellten Benutzeroberflächen in die relevanten plattformspezifischen Benutzeroberflächenkomponenten übersetzt.

## <a name="adding-xamarinessentials"></a>Hinzufügen von „Xamarin.Essentials“

Die UWP-, Android- und iOS-Plattformen bieten zahlreiche ähnliche Funktionen, die das Betriebssystem und die Hardware nutzen. Trotz dieser Ähnlichkeiten sind die APIs sehr unterschiedlich. Zur Verwendung dieser APIs aus plattformübergreifendem Code muss plattformspezifischer Code in Ihren App-Projekten geschrieben werden, den Sie für Ihre .NET Standard-Bibliotheken verfügbar machen. [Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true) ist ein NuGet-Paket, das eine plattformübergreifende Abstraktion über eine Reihe dieser APIs bietet, sodass Sie keinen plattformspezifischen Code schreiben müssen. Dazu gehören auch die Geolocation-APIs, die Sie in Ihrer App verwenden werden, um den Standort des Benutzers zu ermitteln.

1. Klicken Sie im Projektmappen-Explorer von Visual Studio mit der rechten Maustaste auf die Projektmappe `ImHere` (die oberste Projektmappe, nicht das .NET Standard-Projekt `ImHere`), und wählen Sie *NuGet-Pakete für Projektmappe verwalten...* aus.

1. Klicken Sie auf die Registerkarte **Durchsuchen**, und suchen Sie nach „Xamarin.Essentials“. Dieses Paket ist zurzeit als Vorabversion-NuGet-Paket verfügbar. Aktivieren Sie deshalb das Kontrollkästchen neben *Include prelease* (Vorabversion einbeziehen).

    > [!TIP]
    > Wenn Sie das Xamarin.Essentials-NuGet-Paket nicht sehen, überprüfen Sie nochmals, ob *Include prelease* aktiviert ist. 

1. Wählen Sie das NuGet-Paket **Xamarin.Essentials** aus.

1. Aktivieren Sie in der Projektliste auf der rechten Seite sämtliche Ihrer Projekte.

1. Klicken Sie auf die Schaltfläche **Installieren**, um das NuGet-Paket zu installieren. Sie müssen die Lizenz akzeptieren, um den Vorgang fortzusetzen.

    ![Hinzufügen des NuGet-Pakets „Xamarin.Essentials“ zu allen Projekten in der Projektmappe](../media/2-add-essentials-nuget.png)

## <a name="building-and-running-the-app"></a>Erstellen und Ausführen der App

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das `ImHere.UWP`-Projekt, und wählen Sie *Als Startprojekt festlegen* aus.

1. Legen Sie die Buildkonfiguration auf **Debuggen**, die Plattform auf **x86** und das Gerät für die Ausführung auf **Lokaler Computer** fest.

    ![Festlegen der x86-Debugkonfiguration zur Ausführung auf dem lokalen Gerät](../media/2-debug-configuration.png)

1. Beginnen Sie mit dem Debuggen der App.

    ![App bei der Ausführung](../media/2-debuging-app.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine neue plattformübergreifende mobile Xamarin.Forms-App erstellt und das NuGet-Paket „Xamarin.Essentials“ hinzugefügt. Als Nächstes lernen Sie, wie Sie die Benutzeroberfläche und Logik der mobilen App entwickeln.