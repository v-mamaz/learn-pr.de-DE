An diesem Punkt ist die mobile App eine einfache „Hallo Welt“-App. In dieser Einheiten fügen Sie die Benutzeroberfläche und die grundlegende Anwendungslogik hinzu.

Die Benutzeroberfläche der App besteht aus Folgendem:

- Ein Steuerelement für Texteingaben, um Telefonnummern einzugeben.
- Eine Schaltfläche, um Ihren Standort mithilfe einer Azure-Funktion an diese Nummern zu senden.
- Eine Bezeichnung, die eine Meldung an den Benutzer des aktuellen Status sendet, z.B., dass der Standort gesendet wurde und dass der Standort erfolgreich gesendet wird.

Xamarin.Forms unterstützt ein Entwurfsmuster, das als „Model-View-ViewModel“ (MVVM) bezeichnet wird. Weitere Informationen zu MVVM finden Sie in der [Xamarin-Dokumentation zu MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm). Das Wesentliche bei MVVM ist jedoch, dass jede Seite (Ansicht) über ein ViewModel verfügt, das Eigenschaften und Verhaltensweisen verfügbar macht.

ViewModel-Eigenschaften sind nach Name an die Komponenten der Benutzeroberfläche „gebunden“, und diese Bindung synchronisiert Daten zwischen der Ansicht und dem ViewModel. Eine `string`-Eigenschaft in einem ViewModel namens `Name` kann beispielsweise an die `Text`-Eigenschaft eines Steuerelements für die Texteingabe auf der Benutzeroberfläche gebunden werden. Das Steuerelement für die Texteingabe zeigt den Wert in der `Name`-Eigenschaft an. Wenn der Benutzer den Text auf der Benutzeroberfläche ändert, wird die `Name`-Eigenschaft aktualisiert. Wenn der Wert der `Name`-Eigenschaft im ViewModel geändert wird, wird ein Ereignis ausgelöst, damit die Benutzeroberfläche aktualisiert wird.

Das ViewModel-Verhalten wird als Befehlseigenschaften verfügbar macht. Ein Befehl ist ein Objekt, der eine Aktion umfasst, die ausgeführt wird, wenn der Befehl aufgerufen wird. Diese Befehle sind nach Namen an Steuerelemente wie Schaltflächen gebunden, und das Drücken einer Schaltfläche ruft den Befehl auf.

## <a name="create-a-base-viewmodel"></a>Erstellen eines grundlegenden ViewModels

Alle ViewModels implementieren die `INotifyPropertyChanged`-Schnittstelle. Diese Schnittstelle verfügt über ein einzelnes Ereignis, `PropertyChanged`, das verwendet wird, um die Benutzeroberfläche über Updates zu benachrichtigen. Dieses Ereignis verfügt über Ereignisargumente, die den Namen der Eigenschaft, die geändert wurde, enthalten. Es ist üblich, eine ViewModel-Basisklasse zu erstellen, die diese Schnittstelle implementiert und einige Hilfsmethoden bereitstellt.

1. Erstellen Sie eine neue Klasse im `ImHere`.NET Standard-Projekt namens `BaseViewModel`, indem Sie mit der rechten Maustaste auf das Projekt und anschließend auf *Hinzufügen > Klasse* klicken. Nennen Sie die neue Klasse „BaseViewModel“, und klicken Sie auf **Hinzufügen**.

1. Legen Sie die Klasse auf `public` fest, und führen Sie eine Ableitung von `INotifyPropertyChanged` durch. Sie müssen eine using-Anweisung für `System.ComponentModel` hinzufügen.

1. Implementieren Sie die `INotifyPropertyChanged`-Schnittstelle, indem Sie das `PropertyChanged`-Ereignis hinzufügen:

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

1. Das allgemeine Muster für ViewModel-Eigenschaften besteht darin, eine öffentliche Eigenschaft (public) mit einem privaten Unterstützungsfeld (private) zu enthalten. Im Eigenschaftensetter wird das Unterstützungsfeld mit dem neuen Wert verglichen. Wenn der neue Wert sich von dem des Unterstützungsfelds unterscheidet, wird dieses aktualisiert, und das `PropertyChanged`-Ereignis wird ausgelöst. Diese Logik kann in einer Methode auf einfache Weise berücksichtigt werden. Fügen Sie deshalb die `Set`-Methode hinzu. Sie müssen eine using-Anweisung für den `System.Runtime.CompilerServices`-Namespace hinzufügen.

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    Diese Methode akzeptiert einen Verweis auf das Unterstützungsfeld, den neuen Wert und den Eigenschaftennamen. Wenn das Feld nicht geändert wurde, wird die Methode zurückgegeben. Andernfalls wird das Feld aktualisiert und das `PropertyChanged`-Ereignis wird ausgelöst. Der `propertyName`-Parameter der `Set`-Methode ist ein Standardparameter, der mit dem `CallerMemberName`-Attribut markiert ist. Wenn diese Methoden über einen Eigenschaftensetter aufgerufen wird, wird dieser Parameter üblicherweise als Standardwert beibehalten. Der Compiler legt den Parameterwert dann automatisch auf den Namen der aufrufenden Eigenschaft fest.

Im Folgenden finden Sie den vollständigen Code für diese Klasse.

```cs
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace ImHere
{
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
        {
            if (Equals(field, value)) return;
            field = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

## <a name="create-a-viewmodel-for-the-page"></a>Erstellen eines ViewModels für die Seite

Das `MainPage`-Objekt enthält ein Steuerelement für die Texteingabe, in das Telefonnummern eingegeben werden können, und eine Bezeichnung, um eine Meldung anzuzeigen. Diese Steuerelemente werden an die Eigenschaften in einem ViewModel gebunden.

1. Erstellen Sie eine Klasse namens `MainViewModel` im .NET Standard-Projekt `ImHere`.

1. Legen Sie diese Klasse auf „public“ fest, und führen Sie eine Ableitung von `BaseViewModel` durch.

1. Fügen Sie zwei `string`-Eigenschaften (`PhoneNumbers` und `Message`) hinzu, die jeweils ein Unterstützungsfeld enthalten. Verwenden Sie im Eigenschaftensetter die Methode `Set` der Basisklasse, um den Wert zu aktualisieren und das `PropertyChanged`-Ereignis auszulösen.

   ```cs
    string message = "";
    public string Message
    {
        get => message;
        set => Set(ref message, value);
    }

    string phoneNumbers = "";
    public string PhoneNumbers
    {
        get => phoneNumbers;
        set => Set(ref phoneNumbers, value);
    }
   ```

1. Fügen Sie eine schreibgeschützte Befehlseigenschaft namens `SendLocationCommand` hinzu. Dieser Befehl weist den Typ `ICommand` des `System.Windows.Input`-Namespace auf.

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

1. Fügen Sie der Klasse einen Konstruktor hinzu, und initialisieren Sie in diesem Konstruktor den `SendLocationCommand`-Befehl als neuen Befehl (`Command`) aus dem `Xamarin.Forms`-Namespace. Der Konstruktor für diesen Befehl (`Action`) akzeptiert eine Aktion, die ausgeführt werden soll, wenn der Befehl aufgerufen wird. Erstellen Sie deshalb eine `async`-Methode namens `SendLocation`, und übergeben Sie eine Lambda-Funktion (`await`), die auf diesen Aufruf des Konstruktors wartet. Der Körper der `SendLocation`-Methode wird in späteren Einheiten in diesem Modul implementiert. Sie müssen eine using-Anweisung für den `System.Threading.Tasks`-Namespace hinzufügen, die einen Task (`Task`) zurückgeben kann.

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

Im Folgenden finden Sie den Code für diese Klasse.

```cs
using System.Threading.Tasks;
using System.Windows.Input;
using Xamarin.Forms;

namespace ImHere
{
    public class MainViewModel : BaseViewModel
    {
        string message = "";
        public string Message
        {
            get => message;
            set => Set(ref message, value);
        }

        string phoneNumbers = "";
        public string PhoneNumbers
        {
            get => phoneNumbers;
            set => Set(ref phoneNumbers, value);
        }

        public MainViewModel()
        {
            SendLocationCommand = new Command(async () => await SendLocation());
        }

        public ICommand SendLocationCommand { get; }

        async Task SendLocation()
        {
        }
    }
}
```

## <a name="create-the-user-interface"></a>Erstellen der Benutzeroberfläche

Xamarin.Forms-Benutzeroberflächen können mithilfe von XAML erstellt werden.

1. Öffnen Sie die `MainPage.xaml`-Datei über das `ImHere`-Projekt. Die Seite wird im XAML-Editor geöffnet.

    Hinweis: Das `ImHere.UWP`-Projekt enthält ebenfalls eine Datei namens `MainPage.xaml`. Versichern Sie sich, dass Sie die Datei in der .NET Standard-Bibliothek bearbeiten.

1. Bevor Sie Steuerelemente in einem ViewModel an Eigenschaften binden können, müssen Sie eine Instanz von ViewModel als Bindungskontext der Seite festlegen. Fügen Sie folgenden XAML-Code innerhalb der `ContentPage` auf oberster Ebene hinzu.

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

1. Löschen Sie die Inhalte von `StackLayout`, und fügen Sie Auffüllungen hinzu, damit die Benutzeroberfläche besser aussieht.

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

1. Fügen Sie ein `Editor`-Steuerelement hinzu, das der Benutzer dafür verwenden kann, Telefonnummern zu `StackLayout` hinzuzufügen. Diese werden mit einer Bezeichnung `Label` versehen, die beschreibt, wofür das Steuerelement vorgesehen ist. Die untergeordneten Steuerelemente des Stapels von `StackLayout` werden horizontal oder vertikal in der Reihenfolge angeordnet, in der sie hinzugefügt werden. Wenn `Label` also zuerst hinzugefügt wird, wird es über `Editor` platziert. Bei `Editor`-Steuerelementen handelt es sich um mehrzeilige Steuerelemente für Eingaben, über die der Benutzer mehrere Telefonnummern (eine pro Zeile) eingeben kann.

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    Die `Text`-Eigenschaft von `Editor` ist an die `PhoneNumbers`-Eigenschaft von `MainViewModel` gebunden. Die Syntax für die Bindung soll den Eigenschaftenwert auf `"{Binding <property name>}"` festlegen. Durch die geschweiften Klammern wird der XAML-Compiler darüber informiert, dass dieser Wert ein Sonderfall ist und nicht wie eine einfache Zeichenfolge behandelt werden soll `string`.

1. Fügen Sie eine Schaltfläche hinzu, `Button`zum den Standort des Benutzers unter `Editor` zu senden.

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    Die `Command`-Eigenschaft wird an den `SendLocationCommand`-Befehl von ViewModel gebunden. Wenn auf die Schaltfläche getippt wird, wird der Befehl ausgeführt.

1. Fügen Sie eine Bezeichnung `Label` hinzu, um die Statusmeldung unter der Schaltfläche `Button` anzuzeigen.

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

Im Folgenden finden Sie den vollständigen Code für diese Seite.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ImHere"
             x:Class="ImHere.MainPage">
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
        <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                Command="{Binding SendLocationCommand}" />
        <Label Text="{Binding Message}"
               HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    </StackLayout>
</ContentPage>
```

Führen Sie die App aus, um die neue Benutzeroberfläche anzuzeigen. Wenn Sie die Bindung an diesem Punkt überprüfen möchten, können Sie dies tun, indem Sie Breakpoints zu den Eigenschaften oder der `SendLocation`-Methode hinzuzufügen.

![Die Benutzeroberfläche der neuen App](../media-drafts/3-new-ui.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, die Benutzeroberfläche für die App mithilfe von XAML zu erstellen. Außerdem haben Sie ein ViewModel erstellt, um die Anwendungslogik zu verarbeiten. Sie haben ebenfalls gelernt, wie das ViewModel an die Benutzeroberfläche gebunden wird. In der nächsten Einheit fügen Sie die Suche nach dem Standort zum ViewModel hinzu.