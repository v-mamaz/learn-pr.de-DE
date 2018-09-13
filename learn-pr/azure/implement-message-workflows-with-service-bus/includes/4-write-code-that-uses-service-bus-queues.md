Für verteilte Anwendungen werden Warteschlangen, z.B. Service Bus-Warteschlangen, als temporäre Speicherorte für Nachrichten verwendet, die auf ihre Zustellung für eine Zielkomponente warten. Zum Senden und Empfangen von Nachrichten über eine Warteschlange müssen Sie auf den Quell- und Zielkomponenten Code schreiben.

Sehen Sie sich die Anwendung „Contoso Slices“ an. Der Kunde gibt die Bestellung über eine Website oder mobile App auf. Da Websites und mobile Apps auf Kundengeräten ausgeführt werden, gibt es praktisch keine Beschränkung der Anzahl gleichzeitig eingehender Bestellungen. Indem die Bestellungen der mobilen App und der Website in eine Warteschlange eingereiht werden, können wir für die Back-End-Komponente (eine Web-App) ermöglichen, dass Bestellungen aus dieser Warteschlange mit der eigenen Geschwindigkeit verarbeitet werden.

Die Anwendung Contoso Slices verfügt über mehrere Schritte zum Verarbeiten einer neuen Bestellung. Da aber alle Schritte davon abhängig sind, dass zuerst die Zahlung autorisiert werden muss, entscheiden wir uns für die Verwendung einer Warteschlange. Die erste Aufgabe unserer empfangenden Komponente ist die Verarbeitung der Zahlung.

In der mobilen App und auf der Website muss Contoso Code schreiben, mit dem der Warteschlange eine Nachricht hinzugefügt wird. In der Back-End-Web-App wird Code geschrieben, mit dem Nachrichten aus der Warteschlange ausgewählt werden.

Hier lernen Sie, wie Sie diesen Code schreiben.

## <a name="the-microsoftazureservicebus-nuget-package"></a>NuGet-Paket „Microsoft.Azure.ServiceBus“

Microsoft stellt eine Bibliothek mit .NET-Klassen bereit, um das Schreiben des Codes zu vereinfachen, mit dem Nachrichten über Service Bus gesendet und empfangen werden. Sie können sie mit allen .NET Framework-Sprachen nutzen, um mit einer Warteschlange, einem Thema oder einem Relay von Service Bus zu interagieren. Diese Bibliothek können Sie in Ihre Anwendung einbinden, indem Sie das NuGet-Paket **Microsoft.Azure.ServiceBus** hinzufügen.

Die wichtigste Klasse in dieser Bibliothek für Warteschlangen ist die `QueueClient`-Klasse. Zunächst müssen Sie diese Klasse jeweils in der sendenden und empfangenden Komponente instanziieren.

## <a name="connection-strings-and-keys"></a>Verbindungszeichenfolgen und Schlüssel

Sowohl für Quellkomponenten als auch für Zielkomponenten sind zwei Informationen erforderlich, um eine Verbindung mit einer Warteschlange in einem Service Bus-Namespace herzustellen:

- Speicherort des Service Bus-Namespace, auch als **Endpunkt** bekannt. Der Speicherort wird als vollqualifizierter Domänenname in der Domäne **servicebus.windows.net** angegeben. Beispiel: **pizzaService.servicebus.windows.net**.
- Ein Zugriffsschlüssel. Service Bus beschränkt den Zugriff auf Warteschlangen, Themen und Relays, indem das Angeben eines Zugriffsschlüssels gefordert wird.

Beide Informationen werden in Form einer Verbindungszeichenfolge für das `QueueClient`-Objekt bereitgestellt. Sie können die richtige Verbindungszeichenfolge für Ihren Namespace im Azure-Portal abrufen.

## <a name="calling-methods-asynchronously"></a>Asynchrones Aufrufen von Methoden

Die Warteschlange in Azure kann sich von den sendenden und empfangenden Komponenten Tausende Kilometer weit entfernt befinden. Auch wenn die physische Entfernung nicht groß ist, können langsame Verbindungen und Bandbreitenkonflikte zu Verzögerungen führen, wenn eine Komponente eine Methode in der Warteschlange aufruft. Aus diesem Grund werden über die Service Bus-Clientbibliothek `async`-Methoden für die Interaktion mit den Warteschlangen bereitgestellt. Wir verwenden diese Methoden, um das Blockieren eines Threads zu vermeiden, während auf den Abschluss von Aufrufen gewartet wird.

Verwenden Sie beim Senden einer Nachricht an eine Warteschlange beispielsweise die `QueueClient.SendAsync()`-Methode mit dem Schlüsselwort `await`.

## <a name="write-code-that-sends-to-queues"></a>Schreiben von Code für das Senden an Warteschlangen 

Für alle Sende- oder Empfangskomponenten sollten Sie die folgenden `using`-Anweisungen allen Codedateien hinzufügen, mit denen eine Service Bus-Warteschlange aufgerufen wird:

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

Erstellen Sie als Nächstes ein neues `QueueClient`-Objekt, und übergeben Sie dafür die Verbindungszeichenfolge und den Namen der Warteschlange:

```C#
queueClient = new QueueClient(TextAppConnectionString, "PrivateMessageQueue");
```

Sie können eine Nachricht an die Warteschlange senden, indem Sie die `QueueClient.SendAsync()`-Methode aufrufen und die Nachricht in Form einer Zeichenfolge mit UTF-8-Codierung übergeben:

```C#
string message = "Sure would like a large pepperoni!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await queueClient.SendAsync(encodedMessage);
```

## <a name="receive-messages-from-queue"></a>Empfangen von Nachrichten einer Warteschlange

Sie müssen zuerst einen Nachrichtenhandler registrieren, um Nachrichten empfangen zu können. Dies ist die Methode in Ihrem Code, die aufgerufen wird, wenn eine Nachricht in der Warteschlange verfügbar ist.

```C#
queueClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

Führen Sie Ihre Verarbeitungsschritte aus. Rufen Sie dann im Nachrichtenhandler die `QueueClient.CompleteAsync()`-Methode auf, um die Nachricht aus der Warteschlange zu entfernen:

```C#
await queueClient.CompleteAsync(message.SystemProperties.LockToken);
```
    