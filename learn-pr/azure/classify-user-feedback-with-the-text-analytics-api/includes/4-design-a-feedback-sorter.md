<span data-ttu-id="4e82f-101">Wenden wir unser Wissen zur Textanalyse auf eine praktische Lösung an.</span><span class="sxs-lookup"><span data-stu-id="4e82f-101">Let's put our knowledge of Text Analytics to work in a practical solution.</span></span> <span data-ttu-id="4e82f-102">Unsere Lösung bezieht sich auf die Standpunktanalyse von Textdokumenten.</span><span class="sxs-lookup"><span data-stu-id="4e82f-102">Our solution will focus on Sentiment Analysis  of text documents.</span></span> <span data-ttu-id="4e82f-103">Sehen wir uns den Kontext an, indem wir das Problem umreißen, das in Angriff genommen werden soll.</span><span class="sxs-lookup"><span data-stu-id="4e82f-103">Let's set the context by describing the problem we want to tackle.</span></span> 

## <a name="manage-customer-feedback-more-efficiently"></a><span data-ttu-id="4e82f-104">Effizienteres Verwalten von Kundenfeedback</span><span class="sxs-lookup"><span data-stu-id="4e82f-104">Manage customer feedback more efficiently</span></span>

<span data-ttu-id="4e82f-105">Nehmen wir einmal an, das Produkt Ihres Unternehmens ist in den sozialen Medien in aller Munde.</span><span class="sxs-lookup"><span data-stu-id="4e82f-105">Social media is active with talk of your company's product.</span></span> <span data-ttu-id="4e82f-106">Auch Ihr Feedback-E-Mail-Alias wird von Kunden oft genutzt, um ihre Meinung zu Ihrem Produkt mitzuteilen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-106">Your feedback email alias is also active with customers eager to share their opinion of your product.</span></span>

<span data-ttu-id="4e82f-107">Wie bei jedem jungen Startup ist das Feedback Ihrer Kunden das A und O für Sie.</span><span class="sxs-lookup"><span data-stu-id="4e82f-107">As is the case with any new startup, you live by the mantra of listening to your customers.</span></span> <span data-ttu-id="4e82f-108">Doch der Erfolg Ihres Produkts stellt Sie auch vor Herausforderungen, um Ihr Versprechen zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-108">However, the success of your product has made keeping this promise easier said than done.</span></span> <span data-ttu-id="4e82f-109">Dies ist zwar ein Luxusproblem, jedoch nichtsdestotrotz ein Problem, das es zu lösen gilt.</span><span class="sxs-lookup"><span data-stu-id="4e82f-109">It's a good problem but a problem all the same.</span></span> 

<span data-ttu-id="4e82f-110">Denn das Team kann die Menge an Feedback einfach nicht mehr verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="4e82f-110">The team can't keep up with the volume of feedback anymore.</span></span> <span data-ttu-id="4e82f-111">Es benötigt Hilfe beim Sortieren des Feedbacks, um Probleme möglichst effizient verwalten zu können.</span><span class="sxs-lookup"><span data-stu-id="4e82f-111">They need help sorting the feedback so that issues can be managed as efficiently as possible.</span></span> <span data-ttu-id="4e82f-112">Als leitender Entwickler in der Organisation wurden Sie gebeten, eine geeignet Lösung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-112">As the lead developer in the organization, you have been asked to build a solution.</span></span> 

<span data-ttu-id="4e82f-113">Sehen wir uns einige allgemeine Voraussetzungen an:</span><span class="sxs-lookup"><span data-stu-id="4e82f-113">Let's look at some high-level requirements:</span></span>


|<span data-ttu-id="4e82f-114">Anforderung</span><span class="sxs-lookup"><span data-stu-id="4e82f-114">Requirement</span></span>  | <span data-ttu-id="4e82f-115">Details</span><span class="sxs-lookup"><span data-stu-id="4e82f-115">Details</span></span>  |
|---------|---------|
|<span data-ttu-id="4e82f-116">Das Feedback muss kategorisiert werden, damit das Team entsprechend darauf reagieren kann.</span><span class="sxs-lookup"><span data-stu-id="4e82f-116">Categorize feedback so we can react to it.</span></span>     |   <span data-ttu-id="4e82f-117">Nicht alle Feedbackmitteilungen sind gleich.</span><span class="sxs-lookup"><span data-stu-id="4e82f-117">Not all feedback is equal.</span></span> <span data-ttu-id="4e82f-118">Bei einigen handelt es sich um lobende Bekundungen,</span><span class="sxs-lookup"><span data-stu-id="4e82f-118">Some is glowing testimony.</span></span> <span data-ttu-id="4e82f-119">während in anderen Feedbackmitteilungen harsche Kritik von unzufriedenen Kunden geübt wird.</span><span class="sxs-lookup"><span data-stu-id="4e82f-119">Other feedback is scathing criticism from a frustrated customer.</span></span>  <span data-ttu-id="4e82f-120">Und in manchen Fällen ist es womöglich unklar, was der Kunde eigentlich möchte.</span><span class="sxs-lookup"><span data-stu-id="4e82f-120">Perhaps you can't tell what the customer wants in other cases.</span></span> <br/><br/><span data-ttu-id="4e82f-121">Wenigstens ein Hinweis auf den Standpunkt oder den Ton des Feedbacks würde Ihnen schon bei der Kategorisierung helfen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-121">At a minimum, having an indication of the sentiment, or tone, of feedback would help us categorize it.</span></span>     |
|<span data-ttu-id="4e82f-122">Die Lösung sollte sich je nach Bedarf zentral hoch- oder herunterskalieren lassen können.</span><span class="sxs-lookup"><span data-stu-id="4e82f-122">The solution should scale up or down to meet demand.</span></span>    |   <span data-ttu-id="4e82f-123">Denken Sie an unser Szenario: Wir sind ein Startup.</span><span class="sxs-lookup"><span data-stu-id="4e82f-123">We're a startup.</span></span> <span data-ttu-id="4e82f-124">Fixkosten lassen sich nur schwer rechtfertigen und wir haben kein genaues Muster im Feedbackdatenverkehr feststellen können.</span><span class="sxs-lookup"><span data-stu-id="4e82f-124">Fixed costs are difficult to justify and we haven't figured out  the exact pattern of feedback traffic.</span></span> <span data-ttu-id="4e82f-125">Wir benötigen also eine Lösung, die Aktivitätsbursts verarbeiten kann, anfallende Kosten in Ruhezeiten jedoch so gering wie möglich hält.</span><span class="sxs-lookup"><span data-stu-id="4e82f-125">We'll need a solution that can tackle bursts of activity, but cost as little as possible during quiet times.</span></span> <br/><br/> <span data-ttu-id="4e82f-126">In diesem Fall empfiehlt sich eine serverlose Architektur, die basierend auf einem Verbrauchstarif abgerechnet wird.</span><span class="sxs-lookup"><span data-stu-id="4e82f-126">A serverless architecture billed on a consumption plan is a good candidate in this case.</span></span>     |
| <span data-ttu-id="4e82f-127">Eine MVP-Lösung (Minimal Viable Product) muss erstellt werden, die jedoch bei Bedarf anpassbar ist.</span><span class="sxs-lookup"><span data-stu-id="4e82f-127">Produce a Minimal Viable Product (MVP), but make the solution adaptable.</span></span>    | <span data-ttu-id="4e82f-128">Heutzutage sollte Feedback kategorisiert werden, damit wir unsere begrenzten Ressourcen für das Feedback einsetzen können, das eine hohe Priorität hat.</span><span class="sxs-lookup"><span data-stu-id="4e82f-128">Today we want to categorize feedback so we can apply our limited resources to the feedback that matters.</span></span> <span data-ttu-id="4e82f-129">Ist ein Kunde frustriert, sollten wir umgehend darüber Bescheid wissen und mit diesem in Dialog treten.</span><span class="sxs-lookup"><span data-stu-id="4e82f-129">If a customer is frustrated, we want to know immediately and start chatting to them.</span></span>  <span data-ttu-id="4e82f-130">Diese Lösung wird in Zukunft um weitere Features erweitert.</span><span class="sxs-lookup"><span data-stu-id="4e82f-130">In the future, we'll enhance this solution to do more.</span></span> <span data-ttu-id="4e82f-131">Ein neues Feature könnte beispielsweise sein, Schlüsselbegriffe in einem Feedback zu überprüfen, um Probleme zu erkennen, bevor sie ein kritisches Ausmaß bei unseren Kunden annehmen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-131">One idea for a new feature is to examine key phrases in feedback to detect pain points before they reach critical mass with our customers.</span></span>   <span data-ttu-id="4e82f-132">Darüber hinaus könnten Antworten an Kunden automatisiert werden, die entweder positiv oder neutral sind.</span><span class="sxs-lookup"><span data-stu-id="4e82f-132">Another idea is to automate responses back to customers who are either positive or neutral.</span></span> <span data-ttu-id="4e82f-133">Denn auch wenn Kunden nur lobende Worte für uns haben, möchten wir sie wissen lassen, dass ihr Feedback weiterhin beachtet wird.</span><span class="sxs-lookup"><span data-stu-id="4e82f-133">Even though they love us, we want them to know we are still listening to their feedback.</span></span> <br/><br/><span data-ttu-id="4e82f-134">Für dieses Szenario eignet sich eine Lösung mit einer Plug & Play-Architektur.</span><span class="sxs-lookup"><span data-stu-id="4e82f-134">A solution that offers a plug-and-play architecture is a good fit here.</span></span> <span data-ttu-id="4e82f-135">Beispielsweise könnten wir Warteschlangen nach dem Fließbandprinzip einsetzen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-135">We could, for example, use queues as a form of factory line.</span></span> <span data-ttu-id="4e82f-136">Sie führen also eine Aufgabe durch, und platzieren das Ergebnis in eine Warteschlange, die der anschließend zuständige Teil des Systems übernimmt und weiterverarbeitet.</span><span class="sxs-lookup"><span data-stu-id="4e82f-136">You perform one task, then place the result into a queue for the next part of the system to pick it up and process.</span></span>   |
|<span data-ttu-id="4e82f-137">Es muss schnell eine Lösung bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="4e82f-137">Deliver quickly.</span></span>     |   <span data-ttu-id="4e82f-138">Ein altbekanntes Gesetz.</span><span class="sxs-lookup"><span data-stu-id="4e82f-138">We've all heard this one before!</span></span> <span data-ttu-id="4e82f-139">Denken Sie daran, dass es hier um eine MVP-Lösung geht und diese schnell an unserem Szenario getestet werden soll.</span><span class="sxs-lookup"><span data-stu-id="4e82f-139">Remember, this solution is an MVP and we want to test it with our scenario quickly.</span></span> <span data-ttu-id="4e82f-140">Um eine schnelle und qualitativ angemessene Lösung bereitzustellen, müssen wir den Umfang des zu schreibenden Codes einschränken.</span><span class="sxs-lookup"><span data-stu-id="4e82f-140">To deliver at speed and with quality will mean writing less code.</span></span> <br/><br/> <span data-ttu-id="4e82f-141">Der Vorteil der Textanalyse-API besteht darin, dass ein Modell nicht für die Erkennung des Standpunkts trainiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="4e82f-141">Taking advantage of the Text Analytics API means we don't have to train a model to detect sentiment.</span></span>  <span data-ttu-id="4e82f-142">Mithilfe von Azure Functions und deklarativen Bindungen an Warteschlangen wird die Menge an Code, der geschrieben werden muss, reduziert.</span><span class="sxs-lookup"><span data-stu-id="4e82f-142">Using Azure Functions and binding to queues declaratively reduces the amount of code we have to write.</span></span>  <span data-ttu-id="4e82f-143">Eine serverlose Lösung bedeutet zudem, dass die Serververwaltung wegfällt.</span><span class="sxs-lookup"><span data-stu-id="4e82f-143">A serverless solution also means we don't have to worry about server management.</span></span>   |

<span data-ttu-id="4e82f-144">Unsere vorgeschlagenen Lösungen für die einzelnen Anforderungen in der obigen Tabelle bieten einen Einblick in den Denkprozess, um passende Lösungen für die jeweiligen Anforderungen zu finden.</span><span class="sxs-lookup"><span data-stu-id="4e82f-144">Our proposed solution for each requirement in the preceding table offers a glimpse into how to map requirements to solutions.</span></span>  <span data-ttu-id="4e82f-145">Sehen wir uns nun an, wie eine Lösung auf Basis von Azure aussehen könnte.</span><span class="sxs-lookup"><span data-stu-id="4e82f-145">Let's now see  what a solution might look like based on Azure.</span></span>

## <a name="a-solution-based-on-azure-functions-azure-queue-storage-and-text-analytics-api"></a><span data-ttu-id="4e82f-146">Eine Lösung auf Grundlage von Azure Functions, Azure Queue Storage und der Textanalyse-API</span><span class="sxs-lookup"><span data-stu-id="4e82f-146">A solution based on Azure Functions, Azure Queue Storage, and Text Analytics API</span></span>

<span data-ttu-id="4e82f-147">Die folgende Abbildung zeigt einen Entwurfsvorschlag für eine Lösung.</span><span class="sxs-lookup"><span data-stu-id="4e82f-147">The following diagram is a design proposal for a solution.</span></span> <span data-ttu-id="4e82f-148">Darin werden drei Kernkomponenten von Azure verwendet: Azure Queue Storage, Azure Functions und Microsoft Cognitive Services in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e82f-148">It uses three core components of Azure - Azure Queue Storage, Azure Functions, and Microsoft Cognitive Services on Azure.</span></span>

![Konzeptionelle Darstellung einer Architektur zum Sortieren von Feedback](../media-draft/proposed-solution.PNG)

<span data-ttu-id="4e82f-150">Die obige Abbildung zeigt, wie Textdokumente mit Benutzerfeedback in eine Warteschlange mit dem Namen *new-feedback-q* platziert.</span><span class="sxs-lookup"><span data-stu-id="4e82f-150">The idea is that text documents containing user feedback are placed into a queue that we've named *new-feedback-q* in the preceding diagram.</span></span> <span data-ttu-id="4e82f-151">Der Eingang eines Textdokuments in der Warteschlange löst eine Azure-Funktion aus bzw. startet diese.</span><span class="sxs-lookup"><span data-stu-id="4e82f-151">The arrival of a text document into the queue triggers, or starts, an Azure Function.</span></span> <span data-ttu-id="4e82f-152">Die Funktion liest die neuen Dokumente aus der Eingabewarteschlange und sendet diese zur Analyse an die Textanalyse-API.</span><span class="sxs-lookup"><span data-stu-id="4e82f-152">The function reads the new documents from the input queue and sends them for analysis to the Text Analytics API.</span></span> <span data-ttu-id="4e82f-153">Basierend auf den Ergebnissen, die die API zurückgibt, wird das Dokument zur weiteren Verarbeitung in eine Ausgabewarteschlange platziert.</span><span class="sxs-lookup"><span data-stu-id="4e82f-153">Based on the results that the API returns, the document is placed into an output queue for further processing.</span></span>

<span data-ttu-id="4e82f-154">Das für die einzelnen Dokumente berechnete Ergebnis ergibt einen Standpunktwert.</span><span class="sxs-lookup"><span data-stu-id="4e82f-154">The result we get back for each document is a sentiment score.</span></span> <span data-ttu-id="4e82f-155">In den Ausgabewarteschlangen wird Feedback gespeichert, und zwar sortiert nach positivem, neutralem und negativem Feedback.</span><span class="sxs-lookup"><span data-stu-id="4e82f-155">The output queues are used to store feedback sorted into positive, neutral, and negative.</span></span> <span data-ttu-id="4e82f-156">Die Warteschlange für negatives Feedback ist dabei hoffentlich stets leer.</span><span class="sxs-lookup"><span data-stu-id="4e82f-156">Hopefully the negative queue will always be empty!</span></span> <span data-ttu-id="4e82f-157">Sobald wir jedes eingehende Feedback basierend auf dem Standpunkt der jeweiligen Ausgabewarteschlange zugeordnet haben, können Sie beispielsweise Logik hinzufügen, um entsprechende Maßnahmen für die Nachrichten in den Warteschlangen vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-157">:-)   Once we've bucketed each incoming piece of feedback into an output queue based on sentiment, you can imagine adding logic to take action on the messages in each queue.</span></span> 

<span data-ttu-id="4e82f-158">Sehen wir uns als Nächstes ein Flussdiagramm an, um zu erfahren, welche Schritte die Funktionslogik durchführen muss.</span><span class="sxs-lookup"><span data-stu-id="4e82f-158">Let's look at a flowchart next to see what the function logic needs to do.</span></span>

![Flussdiagramm zur Logik in der Azure-Funktion zum Sortieren von Textdokumenten nach Standpunkt in Ausgabewarteschlangen](../media-draft/flow.PNG)

<span data-ttu-id="4e82f-160">Unsere Logik ist wie ein Router.</span><span class="sxs-lookup"><span data-stu-id="4e82f-160">Our logic is like a router.</span></span> <span data-ttu-id="4e82f-161">Sie empfängt eine Texteingabe und leitet sie abhängig vom Standpunktwert des Texts an eine Ausgabewarteschlange weiter.</span><span class="sxs-lookup"><span data-stu-id="4e82f-161">It takes text input and routes it to an output queue based on the sentiment score of the text.</span></span> <span data-ttu-id="4e82f-162">Wir sind auf die Textanalyse-API angewiesen.</span><span class="sxs-lookup"><span data-stu-id="4e82f-162">We have a dependency on Text Analytics API.</span></span> <span data-ttu-id="4e82f-163">Zwar wirkt die Logik recht simpel, doch durch diese Funktion entfällt die Notwendigkeit für Teammitglieder, Feedback manuell zu analysieren.</span><span class="sxs-lookup"><span data-stu-id="4e82f-163">While the logic seems trivial, this function will remove the need for people on the team to analyze feedback manually.</span></span>

## <a name="steps-to-implement-our-solution"></a><span data-ttu-id="4e82f-164">Schritte zur Implementierung unserer Lösung</span><span class="sxs-lookup"><span data-stu-id="4e82f-164">Steps to implement our solution</span></span>

<span data-ttu-id="4e82f-165">Um die in dieser Einheit beschriebene Lösung zu implementieren, müssen die folgenden Schritte durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="4e82f-165">To implement the solution described in this unit, we'll need to complete the following steps.</span></span>

1. <span data-ttu-id="4e82f-166">Erstellen Sie eine Funktions-App zum Hosten der Lösung.</span><span class="sxs-lookup"><span data-stu-id="4e82f-166">Create a function app to host our solution.</span></span>

1. <span data-ttu-id="4e82f-167">Prüfen Sie den Standpunkt in eingehenden Feedbacknachrichten mittels der Textanalyse-API.</span><span class="sxs-lookup"><span data-stu-id="4e82f-167">Look for sentiment in incoming feedback messages using the Text Analytics API.</span></span> <span data-ttu-id="4e82f-168">Wir verwenden unseren Zugriffsschlüssel aus der vorherigen Übung und schreiben Code, um die Anforderungen zu senden.</span><span class="sxs-lookup"><span data-stu-id="4e82f-168">We'll use our access key from the preceding exercise and write some code to send the requests.</span></span>

1. <span data-ttu-id="4e82f-169">Veröffentlichen Sie Feedback für die verarbeitenden Warteschlangen basierend auf dem Standpunkt.</span><span class="sxs-lookup"><span data-stu-id="4e82f-169">Post feedback to processing queues based on sentiment.</span></span>


<span data-ttu-id="4e82f-170">Fahren wir nun mit der Erstellung unserer Funktion und der Funktions-App fort.</span><span class="sxs-lookup"><span data-stu-id="4e82f-170">Let's move on to creating our function and function app.</span></span> 