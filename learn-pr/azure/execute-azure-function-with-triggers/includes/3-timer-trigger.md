Es ist üblich, eine bestimmte Logik in festgelegten Intervallen auszuführen. Stellen Sie sich vor, Sie haben einen Blog und stellen fest, dass Ihre Abonnenten die neuesten Beiträge nicht lesen. Also entscheiden Sie sich dafür, ein Mal pro Woche eine E-Mail zu senden, um sie an Ihren Blog zu erinnern. Sie implementieren diese Logik mit einer Azure Funktions-App mit einem _Timertrigger_, damit Ihre Funktion wöchentlich aufgerufen wird.

## <a name="what-is-a-timer-trigger"></a>Was ist ein Timertrigger?

Ein Zeitgebertrigger ist ein Trigger, der eine Funktion in einem bestimmten Intervall ausführt. Um einen Timertrigger zu erstellen, müssen Sie zwei Informationen angeben.

1. Ein *Zeitstempel-Parametername*, d.h. ein Bezeichner für den Zugriff auf den Trigger im Code.
2. Ein *Zeitplan*, d.h. ein CRON-Ausdruck, der das Intervall für den Timer festlegt.

## <a name="what-is-a-cron-expression"></a>Was ist ein CRON-Ausdruck?

Ein *CRON-Ausdruck* ist eine Zeichenfolge aus sechs Feldern, die eine Zeitangabe darstellt.

Die Reihenfolge der sechs Felder in Azure ist die folgende: `{second} {minute} {hour} {day} {month} {day of the week}`.

Ein CRON-Ausdruck zum Erstellen eines Triggers, der alle fünf Minuten ausgeführt wird, sieht beispielsweise so aus:

```log
0 */5 * * * *
```

Diese Zeichenfolge kann auf den ersten Blick verwirrend aussehen. Wir betrachten diese Konzepte im Detail, wenn wir uns die CRON-Ausdrücke genauer ansehen.

Um einen CRON-Ausdruck zu erstellen, benötigen Sie ein grundlegendes Verständnis von Sonderzeichen.

| Sonderzeichen | Bedeutung | Beispiel |
| ------------- | ------------- | ------------- |
| *      | Wählt jeden Wert in einem Feld aus | Ein Sternchen „*“ im Feld für den Wochentag steht für *jeden* Tag. |
| ,      | Trennt Listenelemente | Ein Komma „1,3“ im Feld für den Wochentag wird bei Auflistungen verwendet. In diesem Beispiel trennt es „montags“ (Tag 1) und „mittwochs“ (Tag 3). |
| -      | Gibt einen Bereich an | Ein Bindestrich „10-12“ im Feld für die Stunden gibt einen Bereich an, der hier 10, 11 und 12 Uhr einschließt. |
| /      | Gibt ein Inkrement an | Ein Schrägstrich „*/10“ im Feld für die Minuten bedeutet in diesem Beispiel ein Inkrement von 10 Minuten. |

Nun kehren wir zum ursprünglichen CRON-Ausdruckbeispiel zurück. Versuchen wir, ihn besser zu verstehen, indem wir ihn Feld für Feld aufschlüsseln.

```log
0 */5 * * * *
```

Das **erste Feld** stellt die Sekunden dar. Es unterstützt die Werte 0 bis 59. Da das Feld eine 0 (Null) enthält, wird der erste Wert ausgewählt, der eine Sekunde beträgt.

Das **zweite Feld** steht für die Minuten. Der Wert „*/5“ enthält zwei Sonderzeichen. Das Sternchen (\*) gibt an, dass jeder Wert im Feld ausgewählt wird. Da dieses Feld die Minuten darstellt, sind die möglichen Werte 0 bis 59. Das zweite Sonderzeichen ist der Schrägstrich (/), der ein Inkrement angibt. Wenn Sie diese Zeichen kombinieren, bedeutet das, dass im Bereich 0 bis 59 jeder fünfte Wert ausgewählt wird. Das bedeutet also „alle fünf Minuten“.

Die **verbleibenden vier Felder** stellen die Stunde, den Tag, den Monat und den Wochentag dar. Ein Sternchen in einem dieser Felder bedeutet, ein beliebiger Wert wird ausgewählt. In diesem Beispiel wählen wir „jede Stunde jedes Tages jedes Monats“ aus.

Wenn Sie alle Felder zusammensetzen, bedeutet der Ausdruck „in der ersten Sekunde jeder fünften Minute jeder Stunde jedes Tages jedes Monats“.

## <a name="how-to-create-a-timer-trigger"></a>Erstellen eines Timertriggers

Sie können im Azure-Portal einen Timertrigger erstellen. Wählen Sie in Ihrer Azure-Funktions-App **Timertrigger** aus der Liste der Triggervorlagen aus. Geben Sie die Logik ein, die Sie ausführen möchten. Geben Sie einen **Zeitstempel-Parameternamen** und den **CRON-Ausdruck** an.

In diesem Modul liegt der Schwerpunkt auf die Erstellung von Triggern im Portal, aber Sie können Trigger auch programmgesteuert mit Core Tools, Visual Studio oder VS Code erstellen.

Ein Timertrigger ruft eine Azure Funktions-App nach einem einheitlichen Zeitplan auf. Um den Zeitplan für einen Timertrigger zu definieren, erstellen Sie einen CRON-Ausdruck. Dabei handelt es sich um eine Zeichenfolge, die eine Zeitangabe darstellt.