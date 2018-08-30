<span data-ttu-id="400c4-101">An diesem Punkt ist die mobile App eine einfache „Hallo Welt“-App.</span><span class="sxs-lookup"><span data-stu-id="400c4-101">At this point, the mobile app is a simple "Hello World" app.</span></span> <span data-ttu-id="400c4-102">In dieser Einheiten fügen Sie die Benutzeroberfläche und die grundlegende Anwendungslogik hinzu.</span><span class="sxs-lookup"><span data-stu-id="400c4-102">In this unit, you add the UI and some basic application logic.</span></span>

<span data-ttu-id="400c4-103">Die Benutzeroberfläche der App besteht aus Folgendem:</span><span class="sxs-lookup"><span data-stu-id="400c4-103">The UI for the app will consist of:</span></span>

* <span data-ttu-id="400c4-104">Ein Steuerelement für Texteingaben, um Telefonnummern einzugeben.</span><span class="sxs-lookup"><span data-stu-id="400c4-104">A text-entry control to enter some phone numbers.</span></span>
* <span data-ttu-id="400c4-105">Eine Schaltfläche, um Ihren Standort mithilfe einer Azure-Funktion an diese Nummern zu senden.</span><span class="sxs-lookup"><span data-stu-id="400c4-105">A button to send your location to those numbers using an Azure function.</span></span>
* <span data-ttu-id="400c4-106">Eine Bezeichnung, die eine Meldung an den Benutzer des aktuellen Status sendet, z.B., dass der Standort gesendet wurde und dass der Standort erfolgreich gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="400c4-106">A label that will show a message to the user of the current status, such as the location being sent and location sent successfully.</span></span>

<span data-ttu-id="400c4-107">Xamarin.Forms unterstützt ein Entwurfsmuster, das als „Model-View-ViewModel“ (MVVM) bezeichnet wird.</span><span class="sxs-lookup"><span data-stu-id="400c4-107">Xamarin.Forms supports a design pattern called Model-View-ViewModel (MVVM).</span></span> <span data-ttu-id="400c4-108">Weitere Informationen zu MVVM finden Sie in der [Xamarin-Dokumentation zu MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm). Das Wesentliche bei MVVM ist jedoch, dass jede Seite (Ansicht) über ein ViewModel verfügt, das Eigenschaften und Verhaltensweisen verfügbar macht.</span><span class="sxs-lookup"><span data-stu-id="400c4-108">You can read more about MVVM in the [Xamarin MVVM docs](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), but the essence of it is, each page (View) has a ViewModel that exposes properties and behavior.</span></span>

<span data-ttu-id="400c4-109">ViewModel-Eigenschaften sind nach Name an die Komponenten der Benutzeroberfläche „gebunden“, und diese Bindung synchronisiert Daten zwischen der Ansicht und dem ViewModel.</span><span class="sxs-lookup"><span data-stu-id="400c4-109">ViewModel properties are 'bound' to components on the UI by name, and this binding synchronizes data between the View and ViewModel.</span></span> <span data-ttu-id="400c4-110">Eine `string`-Eigenschaft in einem ViewModel namens `Name` kann beispielsweise an die `Text`-Eigenschaft eines Steuerelements für die Texteingabe auf der Benutzeroberfläche gebunden werden.</span><span class="sxs-lookup"><span data-stu-id="400c4-110">For example, a `string` property on a ViewModel called `Name` could be bound to the `Text` property of a text-entry control on the UI.</span></span> <span data-ttu-id="400c4-111">Das Steuerelement für die Texteingabe zeigt den Wert in der `Name`-Eigenschaft an. Wenn der Benutzer den Text auf der Benutzeroberfläche ändert, wird die `Name`-Eigenschaft aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="400c4-111">The text-entry control shows the value in the `Name` property and, when the user changes the text in the UI, the `Name` property is updated.</span></span> <span data-ttu-id="400c4-112">Wenn der Wert der `Name`-Eigenschaft im ViewModel geändert wird, wird ein Ereignis ausgelöst, damit die Benutzeroberfläche aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="400c4-112">If the value of the `Name` property is changed in the ViewModel, an event is raised to tell the UI to update.</span></span>

<span data-ttu-id="400c4-113">Das ViewModel-Verhalten wird als Befehlseigenschaften verfügbar macht. Ein Befehl ist ein Objekt, der eine Aktion umfasst, die ausgeführt wird, wenn der Befehl aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="400c4-113">ViewModel behavior is exposed as command properties, a command being an object that wraps an action that is executed when the command is invoked.</span></span> <span data-ttu-id="400c4-114">Diese Befehle sind nach Namen an Steuerelemente wie Schaltflächen gebunden, und das Drücken einer Schaltfläche ruft den Befehl auf.</span><span class="sxs-lookup"><span data-stu-id="400c4-114">These commands are bound by name to controls like buttons, and tapping a button will invoke the command.</span></span>

## <a name="create-a-base-viewmodel"></a><span data-ttu-id="400c4-115">Erstellen eines grundlegenden ViewModels</span><span class="sxs-lookup"><span data-stu-id="400c4-115">Create a base ViewModel</span></span>

<span data-ttu-id="400c4-116">Alle ViewModels implementieren die `INotifyPropertyChanged`-Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="400c4-116">ViewModels all implement the `INotifyPropertyChanged` interface.</span></span> <span data-ttu-id="400c4-117">Diese Schnittstelle verfügt über ein einzelnes Ereignis, `PropertyChanged`, das verwendet wird, um die Benutzeroberfläche über Updates zu benachrichtigen.</span><span class="sxs-lookup"><span data-stu-id="400c4-117">This interface has a single event, `PropertyChanged`, which is used to notify the UI of any updates.</span></span> <span data-ttu-id="400c4-118">Dieses Ereignis verfügt über Ereignisargumente, die den Namen der Eigenschaft, die geändert wurde, enthalten.</span><span class="sxs-lookup"><span data-stu-id="400c4-118">This event has event args that contain the name of the property that has changed.</span></span> <span data-ttu-id="400c4-119">Es ist üblich, eine ViewModel-Basisklasse zu erstellen, die diese Schnittstelle implementiert und einige Hilfsmethoden bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="400c4-119">It's common practice to create a base ViewModel class implementing this interface and providing some helper methods.</span></span>

1. <span data-ttu-id="400c4-120">Erstellen Sie eine neue Klasse im `ImHere`.NET Standard-Projekt namens `BaseViewModel`, indem Sie mit der rechten Maustaste auf das Projekt und anschließend auf *Hinzufügen > Klasse* klicken. Nennen Sie die neue Klasse „BaseViewModel“, und klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="400c4-120">Create a new class in the `ImHere` .NET standard project called `BaseViewModel` by right-clicking on the project, and then selecting *Add->Class...*. Name the new class "BaseViewModel" and click **Add**.</span></span>

2. <span data-ttu-id="400c4-121">Legen Sie die Klasse auf `public` fest, und führen Sie eine Ableitung von `INotifyPropertyChanged` durch.</span><span class="sxs-lookup"><span data-stu-id="400c4-121">Make the class `public` and derive from `INotifyPropertyChanged`.</span></span> <span data-ttu-id="400c4-122">Sie müssen eine using-Anweisung für `System.ComponentModel` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="400c4-122">You'll need to add a using directive for `System.ComponentModel`.</span></span>

3. <span data-ttu-id="400c4-123">Implementieren Sie die `INotifyPropertyChanged`-Schnittstelle, indem Sie das `PropertyChanged`-Ereignis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="400c4-123">Implement the `INotifyPropertyChanged` interface by adding the `PropertyChanged` event:</span></span>

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. <span data-ttu-id="400c4-124">Das allgemeine Muster für ViewModel-Eigenschaften besteht darin, eine öffentliche Eigenschaft (public) mit einem privaten Unterstützungsfeld (private) zu enthalten.</span><span class="sxs-lookup"><span data-stu-id="400c4-124">The common pattern for ViewModel properties is to have a public property with a private backing field.</span></span> <span data-ttu-id="400c4-125">Im Eigenschaftensetter wird das Unterstützungsfeld mit dem neuen Wert verglichen.</span><span class="sxs-lookup"><span data-stu-id="400c4-125">In the property setter, the backing field is checked against the new value.</span></span> <span data-ttu-id="400c4-126">Wenn der neue Wert sich von dem des Unterstützungsfelds unterscheidet, wird dieses aktualisiert, und das `PropertyChanged`-Ereignis wird ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="400c4-126">If the new value is different to the backing field, the backing field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="400c4-127">Diese Logik kann in einer Methode auf einfache Weise berücksichtigt werden. Fügen Sie deshalb die `Set`-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="400c4-127">This logic is easy to factor out into a method, so add the `Set` method.</span></span> <span data-ttu-id="400c4-128">Sie müssen eine using-Anweisung für den `System.Runtime.CompilerServices`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="400c4-128">You'll need to add a using directive for the `System.Runtime.CompilerServices` namespace.</span></span>

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    <span data-ttu-id="400c4-129">Diese Methode akzeptiert einen Verweis auf das Unterstützungsfeld, den neuen Wert und den Eigenschaftennamen.</span><span class="sxs-lookup"><span data-stu-id="400c4-129">This method takes a reference to the backing field, the new value, and the property name.</span></span> <span data-ttu-id="400c4-130">Wenn das Feld nicht geändert wurde, wird die Methode zurückgegeben. Andernfalls wird das Feld aktualisiert und das `PropertyChanged`-Ereignis wird ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="400c4-130">If the field hasn't changed, the method returns, otherwise, the field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="400c4-131">Der `propertyName`-Parameter der `Set`-Methode ist ein Standardparameter, der mit dem `CallerMemberName`-Attribut markiert ist.</span><span class="sxs-lookup"><span data-stu-id="400c4-131">The `propertyName` parameter on the `Set` method is a default parameter and is marked with the `CallerMemberName` attribute.</span></span> <span data-ttu-id="400c4-132">Wenn diese Methoden über einen Eigenschaftensetter aufgerufen wird, wird dieser Parameter üblicherweise als Standardwert beibehalten.</span><span class="sxs-lookup"><span data-stu-id="400c4-132">When this method is called from a property setter, this parameter is normally left as the default value.</span></span> <span data-ttu-id="400c4-133">Der Compiler legt den Parameterwert dann automatisch auf den Namen der aufrufenden Eigenschaft fest.</span><span class="sxs-lookup"><span data-stu-id="400c4-133">The compiler will then automatically set the parameter value to be the name of the calling property.</span></span>

<span data-ttu-id="400c4-134">Im Folgenden finden Sie den vollständigen Code für diese Klasse.</span><span class="sxs-lookup"><span data-stu-id="400c4-134">The full code for this class is below.</span></span>

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

## <a name="create-a-viewmodel-for-the-page"></a><span data-ttu-id="400c4-135">Erstellen eines ViewModels für die Seite</span><span class="sxs-lookup"><span data-stu-id="400c4-135">Create a ViewModel for the page</span></span>

<span data-ttu-id="400c4-136">Das `MainPage`-Objekt enthält ein Steuerelement für die Texteingabe, in das Telefonnummern eingegeben werden können, und eine Bezeichnung, um eine Meldung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="400c4-136">The `MainPage` will have a text-entry control for phone numbers and a label to display a message.</span></span> <span data-ttu-id="400c4-137">Diese Steuerelemente werden an die Eigenschaften in einem ViewModel gebunden.</span><span class="sxs-lookup"><span data-stu-id="400c4-137">These controls will be bound to properties on a ViewModel.</span></span>

1. <span data-ttu-id="400c4-138">Erstellen Sie eine Klasse namens `MainViewModel` im .NET Standard-Projekt `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="400c4-138">Create a class called `MainViewModel` in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="400c4-139">Legen Sie diese Klasse auf „public“ fest, und führen Sie eine Ableitung von `BaseViewModel` durch.</span><span class="sxs-lookup"><span data-stu-id="400c4-139">Make this class public and derive from `BaseViewModel`.</span></span>

3. <span data-ttu-id="400c4-140">Fügen Sie zwei `string`-Eigenschaften (`PhoneNumbers` und `Message`) hinzu, die jeweils ein Unterstützungsfeld enthalten.</span><span class="sxs-lookup"><span data-stu-id="400c4-140">Add two `string` properties, `PhoneNumbers` and `Message`, each with a backing field.</span></span> <span data-ttu-id="400c4-141">Verwenden Sie im Eigenschaftensetter die Methode `Set` der Basisklasse, um den Wert zu aktualisieren und das `PropertyChanged`-Ereignis auszulösen.</span><span class="sxs-lookup"><span data-stu-id="400c4-141">In the property setter, use the base class `Set` method to update the value and raise the `PropertyChanged` event.</span></span>

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

4. <span data-ttu-id="400c4-142">Fügen Sie eine schreibgeschützte Befehlseigenschaft namens `SendLocationCommand` hinzu.</span><span class="sxs-lookup"><span data-stu-id="400c4-142">Add a read-only command property called `SendLocationCommand`.</span></span> <span data-ttu-id="400c4-143">Dieser Befehl weist den Typ `ICommand` des `System.Windows.Input`-Namespace auf.</span><span class="sxs-lookup"><span data-stu-id="400c4-143">This command will have a type of `ICommand` from the `System.Windows.Input` namespace.</span></span>

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. <span data-ttu-id="400c4-144">Fügen Sie der Klasse einen Konstruktor hinzu, und initialisieren Sie in diesem Konstruktor den `SendLocationCommand`-Befehl als neuen Befehl (`Command`) aus dem `Xamarin.Forms`-Namespace.</span><span class="sxs-lookup"><span data-stu-id="400c4-144">Add a constructor to the class, and in this constructor, initialize the `SendLocationCommand` as a new `Command` from the `Xamarin.Forms` namespace.</span></span> <span data-ttu-id="400c4-145">Der Konstruktor für diesen Befehl (`Action`) akzeptiert eine Aktion, die ausgeführt werden soll, wenn der Befehl aufgerufen wird. Erstellen Sie deshalb eine `async`-Methode namens `SendLocation`, und übergeben Sie eine Lambda-Funktion (`await`), die auf diesen Aufruf des Konstruktors wartet.</span><span class="sxs-lookup"><span data-stu-id="400c4-145">The constructor for this command takes an `Action` to run when the command is invoked, so create an `async` method called `SendLocation` and pass a lambda function that `await`s this call to the constructor.</span></span> <span data-ttu-id="400c4-146">Der Körper der `SendLocation`-Methode wird in späteren Einheiten in diesem Modul implementiert.</span><span class="sxs-lookup"><span data-stu-id="400c4-146">The body of the `SendLocation` method will be implemented in later units in this module.</span></span> <span data-ttu-id="400c4-147">Sie müssen eine using-Anweisung für den `System.Threading.Tasks`-Namespace hinzufügen, die einen Task (`Task`) zurückgeben kann.</span><span class="sxs-lookup"><span data-stu-id="400c4-147">You'll need to add a using directive for the `System.Threading.Tasks` namespace to be able to return a `Task`.</span></span>

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

<span data-ttu-id="400c4-148">Im Folgenden finden Sie den Code für diese Klasse.</span><span class="sxs-lookup"><span data-stu-id="400c4-148">The code for this class is shown below.</span></span>

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

## <a name="create-the-user-interface"></a><span data-ttu-id="400c4-149">Erstellen der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="400c4-149">Create the user interface</span></span>

<span data-ttu-id="400c4-150">Xamarin.Forms-Benutzeroberflächen können mithilfe von XAML erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="400c4-150">Xamarin.Forms UIs can be built using XAML.</span></span>

1. <span data-ttu-id="400c4-151">Öffnen Sie die `MainPage.xaml`-Datei über das `ImHere`-Projekt.</span><span class="sxs-lookup"><span data-stu-id="400c4-151">Open the `MainPage.xaml` file from the `ImHere` project.</span></span> <span data-ttu-id="400c4-152">Die Seite wird im XAML-Editor geöffnet.</span><span class="sxs-lookup"><span data-stu-id="400c4-152">The page will open in the XAML editor.</span></span>

    <span data-ttu-id="400c4-153">Hinweis: Das `ImHere.UWP`-Projekt enthält ebenfalls eine Datei namens `MainPage.xaml`.</span><span class="sxs-lookup"><span data-stu-id="400c4-153">NOTE - The `ImHere.UWP` project also contains a file called `MainPage.xaml`.</span></span> <span data-ttu-id="400c4-154">Versichern Sie sich, dass Sie die Datei in der .NET Standard-Bibliothek bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="400c4-154">Make sure you're editing the one in the .NET standard library.</span></span>

2. <span data-ttu-id="400c4-155">Bevor Sie Steuerelemente in einem ViewModel an Eigenschaften binden können, müssen Sie eine Instanz von ViewModel als Bindungskontext der Seite festlegen.</span><span class="sxs-lookup"><span data-stu-id="400c4-155">Before you can bind controls to properties on a ViewModel, you have to set an instance of the ViewModel as the binding context of the page.</span></span> <span data-ttu-id="400c4-156">Fügen Sie folgenden XAML-Code innerhalb der `ContentPage` auf oberster Ebene hinzu.</span><span class="sxs-lookup"><span data-stu-id="400c4-156">Add the following XAML inside the top-level `ContentPage`.</span></span>

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. <span data-ttu-id="400c4-157">Löschen Sie die Inhalte von `StackLayout`, und fügen Sie Auffüllungen hinzu, damit die Benutzeroberfläche besser aussieht.</span><span class="sxs-lookup"><span data-stu-id="400c4-157">Delete the contents of the `StackLayout` and add some padding inside it to help make the UI look better.</span></span>

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. <span data-ttu-id="400c4-158">Fügen Sie ein `Editor`-Steuerelement hinzu, das der Benutzer dafür verwenden kann, Telefonnummern zu `StackLayout` hinzuzufügen. Diese werden mit einer Bezeichnung versehen, die beschreibt, wofür das Steuerelement vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="400c4-158">Add an `Editor` control that the user can use to add phone numbers to the `StackLayout`, with a `Label` above to describe what the entry control is for.</span></span> <span data-ttu-id="400c4-159">Die untergeordneten Steuerelemente des Stapels von `StackLayout` werden horizontal oder vertikal in der Reihenfolge angeordnet, in der sie hinzugefügt werden. Wenn `Label` also zuerst hinzugefügt wird, wird es über `Editor` platziert.</span><span class="sxs-lookup"><span data-stu-id="400c4-159">`StackLayout`'s stack child controls either horizontally or vertically in the order in which the controls are added, so adding the `Label` first will put it above the `Editor`.</span></span> <span data-ttu-id="400c4-160">Bei `Editor`-Steuerelementen handelt es sich um mehrzeilige Steuerelemente für Eingaben, über die der Benutzer mehrere Telefonnummern (eine pro Zeile) eingeben kann.</span><span class="sxs-lookup"><span data-stu-id="400c4-160">`Editor` controls are multi-line entry controls, allowing the user to enter multiple phone numbers, one per line.</span></span>

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    <span data-ttu-id="400c4-161">Die `Text`-Eigenschaft von `Editor` ist an die `PhoneNumbers`-Eigenschaft von `MainViewModel` gebunden.</span><span class="sxs-lookup"><span data-stu-id="400c4-161">The `Text` property on the `Editor` is bound to the `PhoneNumbers` property on the `MainViewModel`.</span></span> <span data-ttu-id="400c4-162">Die Syntax für die Bindung soll den Eigenschaftenwert auf `"{Binding <property name>}"` festlegen.</span><span class="sxs-lookup"><span data-stu-id="400c4-162">The syntax for binding is to set the property value to `"{Binding <property name>}"`.</span></span> <span data-ttu-id="400c4-163">Durch die geschweiften Klammern wird der XAML-Compiler darüber informiert, dass dieser Wert ein Sonderfall ist und nicht wie eine einfache Zeichenfolge behandelt werden soll `string`.</span><span class="sxs-lookup"><span data-stu-id="400c4-163">The curly braces will tell the XAML compiler that this value is special and should be treated differently from a simple `string`.</span></span>

5. <span data-ttu-id="400c4-164">Fügen Sie eine Schaltfläche hinzu, `Button`zum den Standort des Benutzers unter `Editor` zu senden.</span><span class="sxs-lookup"><span data-stu-id="400c4-164">Add a `Button` to send the user's location below the `Editor`.</span></span>

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    <span data-ttu-id="400c4-165">Die `Command`-Eigenschaft wird an den `SendLocationCommand`-Befehl von ViewModel gebunden.</span><span class="sxs-lookup"><span data-stu-id="400c4-165">The `Command` property is bound to the `SendLocationCommand` command on the ViewModel.</span></span> <span data-ttu-id="400c4-166">Wenn auf die Schaltfläche getippt wird, wird der Befehl ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="400c4-166">When the button is tapped, the command will be executed.</span></span>

6. <span data-ttu-id="400c4-167">Fügen Sie eine Bezeichnung hinzu, um die Statusmeldung unter der Schaltfläche anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="400c4-167">Add a `Label` to show the status message below the `Button`.</span></span>

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

<span data-ttu-id="400c4-168">Im Folgenden finden Sie den vollständigen Code für diese Seite.</span><span class="sxs-lookup"><span data-stu-id="400c4-168">The full code for this page is below.</span></span>

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

<span data-ttu-id="400c4-169">Führen Sie die App aus, um die neue Benutzeroberfläche anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="400c4-169">Run the app to see the new UI.</span></span> <span data-ttu-id="400c4-170">Wenn Sie die Bindung an diesem Punkt überprüfen möchten, können Sie dies tun, indem Sie Breakpoints zu den Eigenschaften oder der `SendLocation`-Methode hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="400c4-170">If you want to validate the bindings at this point, you can do so by adding breakpoints to the properties or the `SendLocation` method.</span></span>

![Die Benutzeroberfläche der neuen App](../media/3-new-ui.png)

## <a name="summary"></a><span data-ttu-id="400c4-172">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="400c4-172">Summary</span></span>

<span data-ttu-id="400c4-173">In dieser Einheit haben Sie gelernt, die Benutzeroberfläche für die App mithilfe von XAML zu erstellen. Außerdem haben Sie ein ViewModel erstellt, um die Anwendungslogik zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="400c4-173">In this unit, you learned how to create the UI for the app using XAML, along with a ViewModel to handle the applications logic.</span></span> <span data-ttu-id="400c4-174">Sie haben ebenfalls gelernt, wie das ViewModel an die Benutzeroberfläche gebunden wird.</span><span class="sxs-lookup"><span data-stu-id="400c4-174">You also learned how to bind the ViewModel to the UI.</span></span> <span data-ttu-id="400c4-175">In der nächsten Einheit fügen Sie die Suche nach dem Standort zum ViewModel hinzu.</span><span class="sxs-lookup"><span data-stu-id="400c4-175">In the next unit, you add location lookup to the ViewModel.</span></span>