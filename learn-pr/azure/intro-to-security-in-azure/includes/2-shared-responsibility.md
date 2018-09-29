<span data-ttu-id="a9d11-101">Mit dem Wandel der Computingumgebungen von vom Kunden gesteuerten Datencentern hin zu Clouddatencentern verschiebt sich auch die Verantwortung für die Sicherheit.</span><span class="sxs-lookup"><span data-stu-id="a9d11-101">As computing environments move from customer-controlled data centers to cloud data centers, the responsibility of security also shifts.</span></span> <span data-ttu-id="a9d11-102">Sicherheit ist nun ein gemeinsames Anliegen von Cloudanbietern und Kunden.</span><span class="sxs-lookup"><span data-stu-id="a9d11-102">Security is now a concern shared both by cloud providers and customers.</span></span> <span data-ttu-id="a9d11-103">Für jede Anwendung und Lösung ist es wichtig zu verstehen, was Ihre Verantwortung ist und was in der Verantwortung von Azure liegt.</span><span class="sxs-lookup"><span data-stu-id="a9d11-103">For every application and solution, it's important to understand what's your responsibility and what's Azure's responsibility.</span></span>

#### <a name="understand-security-threats"></a><span data-ttu-id="a9d11-104">Verstehen der Sicherheitsrisiken</span><span class="sxs-lookup"><span data-stu-id="a9d11-104">Understand security threats</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWkotg]

#### <a name="azure-security-you-versus-the-cloud"></a><span data-ttu-id="a9d11-105">Azure-Sicherheit: Ihre Verantwortung im Vergleich zur Verantwortung der Cloud</span><span class="sxs-lookup"><span data-stu-id="a9d11-105">Azure security: you versus the cloud</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvj]

## <a name="share-security-responsibility-with-azure"></a><span data-ttu-id="a9d11-106">Gemeinsame Verantwortung für die Sicherheit mit Azure</span><span class="sxs-lookup"><span data-stu-id="a9d11-106">Share security responsibility with Azure</span></span>

<span data-ttu-id="a9d11-107">Die erste vorgenommene Verschiebung erfolgt von lokalen Datencentern zu Infrastructure-as-a-Service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="a9d11-107">The first shift you’ll make is from on-premises data centers to infrastructure as a service (IaaS).</span></span> <span data-ttu-id="a9d11-108">Mit IaaS nutzen Sie den Dienst der niedrigsten Ebene und fordern von Azure die Erstellung von virtuellen Computern (VMs) und virtuellen Netzwerken an.</span><span class="sxs-lookup"><span data-stu-id="a9d11-108">With IaaS, you are leveraging the lowest-level service and asking Azure to create virtual machines (VMs) and virtual networks.</span></span> <span data-ttu-id="a9d11-109">Auf dieser Ebene sind Sie weiterhin dafür verantwortlich, Ihre Betriebssysteme und Software zu patchen und zu schützen sowie Ihr Netzwerk so zu konfigurieren, dass es sicher ist.</span><span class="sxs-lookup"><span data-stu-id="a9d11-109">At this level, it's still your responsibility to patch and secure your operating systems and software, as well as configure your network to be secure.</span></span> <span data-ttu-id="a9d11-110">Bei Contoso Shipping nutzen Sie IaaS, wenn Sie damit beginnen, anstelle der lokalen physischen Server die virtuellen Azure-Computer zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a9d11-110">At Contoso Shipping, you are taking advantage of IaaS when you start using Azure VMs instead of your on-premises physical servers.</span></span> <span data-ttu-id="a9d11-111">Zusätzlich zu den betriebsbezogenen Vorteilen kommen Sie in den Genuss des sicherheitsbezogenen Vorteils, dass Sie sich nicht mehr um den Schutz der physischen Komponenten des Netzwerks kümmern müssen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-111">In addition to the operational advantages, you receive the security advantage of having outsourced concern over protecting the physical parts of the network.</span></span>

<span data-ttu-id="a9d11-112">Mit der Umstellung auf Platform-as-a-Service (PaaS) wird ein Großteil der Sicherheitsrisiken outgesourct.</span><span class="sxs-lookup"><span data-stu-id="a9d11-112">Moving to platform as a service (PaaS) outsources a lot of security concerns.</span></span> <span data-ttu-id="a9d11-113">Auf dieser Ebene kümmert sich Azure um das Betriebssystem und die meisten grundlegenden Softwarekomponenten, z.B. Datenbankverwaltungssysteme.</span><span class="sxs-lookup"><span data-stu-id="a9d11-113">At this level, Azure is taking care of the operating system and of most foundational software like database management systems.</span></span> <span data-ttu-id="a9d11-114">Alle Updates mit den aktuellen Sicherheitspatches werden durchgeführt und können für die Zugriffssteuerung in Azure Active Directory integriert werden.</span><span class="sxs-lookup"><span data-stu-id="a9d11-114">Everything is updated with the latest security patches and can be integrated with Azure Active Directory for access controls.</span></span> <span data-ttu-id="a9d11-115">Bei PaaS ergeben sich außerdem viele betriebsbezogene Vorteile.</span><span class="sxs-lookup"><span data-stu-id="a9d11-115">PaaS also comes with a lot of operational advantages.</span></span> <span data-ttu-id="a9d11-116">Anstatt für Ihre Umgebungen gesamte Infrastrukturen und Subnetze manuell zu erstellen, können Sie im Azure-Portal „Point-and-Click“ verwenden oder automatisierte Skripts ausführen, um komplexe geschützte Systeme hoch- und herunterzufahren und wie gewünscht zu skalieren.</span><span class="sxs-lookup"><span data-stu-id="a9d11-116">Rather than building whole infrastructures and subnets for your environments by hand, you can "point and click" within the Azure portal or run automated scripts to bring complex, secured systems up and down, and scale them as needed.</span></span> <span data-ttu-id="a9d11-117">Contoso Shipping verwendet Azure Event Hubs für die Erfassung von Telemetriedaten von Drohnen und LKWs (sowie eine Web-App mit einem Azure Cosmos DB-Back-End mit den mobilen Apps des Unternehmens), die alle Beispiele für PaaS sind.</span><span class="sxs-lookup"><span data-stu-id="a9d11-117">Contoso Shipping uses Azure Event Hubs for ingesting telemetry data from drones and trucks &mdash; as well as a web app with an Azure Cosmos DB back end with their mobile apps &mdash; which are all examples of PaaS.</span></span>

<span data-ttu-id="a9d11-118">Bei Software-as-a-Service (SaaS) wird nahezu alles outgesourct.</span><span class="sxs-lookup"><span data-stu-id="a9d11-118">With software as a service (SaaS), you outsource almost everything.</span></span> <span data-ttu-id="a9d11-119">Bei SaaS handelt es sich um Software, die mit einer Internetinfrastruktur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="a9d11-119">SaaS is software that runs with an internet infrastructure.</span></span> <span data-ttu-id="a9d11-120">Der Code wird vom Anbieter gesteuert, jedoch für die Verwendung durch den Kunden konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="a9d11-120">The code is controlled by the vendor but configured to be used by the customer.</span></span> <span data-ttu-id="a9d11-121">Wie so viele Unternehmen verwendet auch Contoso Shipping Office 365. Dies ist ein gutes Beispiel für SaaS.</span><span class="sxs-lookup"><span data-stu-id="a9d11-121">Like so many companies, Contoso Shipping uses Office 365, which is a great example of SaaS!</span></span>

![shared_responsibility.png](../media/shared_responsibilities.png)

## <a name="a-layered-approach-to-security"></a><span data-ttu-id="a9d11-123">Mehrstufiger Sicherheitsansatz</span><span class="sxs-lookup"><span data-stu-id="a9d11-123">A layered approach to security</span></span>

<span data-ttu-id="a9d11-124">Die *tiefgehende Verteidigung* ist eine Strategie, bei der mithilfe zahlreicher Mechanismen das Ausmaß eines Angriffs gedämpft wird, der darauf abzielt, unberechtigten Zugriff auf Informationen zu erlangen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-124">*Defense in depth* is a strategy that employs a series of mechanisms to slow the advance of an attack aimed at acquiring unauthorized access to information.</span></span> <span data-ttu-id="a9d11-125">Jede Ebene bietet Schutz, sodass bei einer Sicherheitsverletzung auf einer Ebene die nachfolgende Ebene eine weitere Bedrohung verhindert.</span><span class="sxs-lookup"><span data-stu-id="a9d11-125">Each layer provides protection so that if one layer is breached, a subsequent layer is already in place to prevent further exposure.</span></span> <span data-ttu-id="a9d11-126">Microsoft verfolgt einen mehrstufigen Sicherheitsansatz – sowohl in den physischen Datencentern als auch für Azure-Dienste.</span><span class="sxs-lookup"><span data-stu-id="a9d11-126">Microsoft applies a layered approach to security, both in physical data centers and across Azure services.</span></span> <span data-ttu-id="a9d11-127">Im Rahmen der tiefgehenden Verteidigung sollen Informationen geschützt und ihr Diebstahl durch Personen verhindert werden, die keine Zugriffsberechtigung besitzen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-127">The objective of defense in depth is to protect and prevent information from being stolen by individuals who are not authorized to access it.</span></span>

<span data-ttu-id="a9d11-128">Sie können sich die tiefgehende Verteidigung wie einen Satz mit konzentrischen Ringen vorstellen, wobei die Daten im Zentrum geschützt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-128">Defense in depth can be visualized as a set of concentric rings, with the data to be secured at the center.</span></span> <span data-ttu-id="a9d11-129">Jeder Ring stellt eine zusätzliche Sicherheitsebene für die Daten dar.</span><span class="sxs-lookup"><span data-stu-id="a9d11-129">Each ring adds an additional layer of security around the data.</span></span> <span data-ttu-id="a9d11-130">Dieser Ansatz macht die Abhängigkeit von einer einzelnen Schutzebene überflüssig, verlangsamt einen Angriff und bietet Alarmtelemetrie, auf die automatisch oder manuell reagiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="a9d11-130">This approach removes reliance on any single layer of protection and acts to slow down an attack and provide alert telemetry that can be acted upon, either automatically or manually.</span></span> <span data-ttu-id="a9d11-131">Sehen wir uns jede Ebene genauer an.</span><span class="sxs-lookup"><span data-stu-id="a9d11-131">Let's take a look at each of the layers.</span></span>

![Mehrschichtige Sicherheit](../media/defense_in_depth_layers_small.PNG)

:::row:::
  :::column:::
    <span data-ttu-id="a9d11-133">![Bild, das Daten darstellt](../media/2-data.png)</span><span class="sxs-lookup"><span data-stu-id="a9d11-133">![Image representing data](../media/2-data.png)</span></span>
  :::column-end:::
    <span data-ttu-id="a9d11-134">:::column span="3"::: **Daten**</span><span class="sxs-lookup"><span data-stu-id="a9d11-134">:::column span="3"::: **Data**</span></span>

<span data-ttu-id="a9d11-135">In der Regel zielen Angriffe auf folgende Daten ab:</span><span class="sxs-lookup"><span data-stu-id="a9d11-135">In almost all cases, attackers are after data:</span></span>

- <span data-ttu-id="a9d11-136">Daten, die in einer Datenbank gespeichert sind</span><span class="sxs-lookup"><span data-stu-id="a9d11-136">Data stored in a database</span></span>
- <span data-ttu-id="a9d11-137">Daten, die auf einem Datenträger einer VM gespeichert sind</span><span class="sxs-lookup"><span data-stu-id="a9d11-137">Data stored on disk inside virtual machines</span></span>
- <span data-ttu-id="a9d11-138">Daten, die in einer SaaS-Anwendung wie Office 365 gespeichert sind</span><span class="sxs-lookup"><span data-stu-id="a9d11-138">Data stored on a SaaS application such as Office 365</span></span>
- <span data-ttu-id="a9d11-139">Daten, die im Cloudspeicher gespeichert sind</span><span class="sxs-lookup"><span data-stu-id="a9d11-139">Data stored in cloud storage</span></span>

<span data-ttu-id="a9d11-140">Es liegt in der Verantwortung derjenigen, die den Zugriff auf Daten steuern und Daten speichern, sicherzustellen, dass die Daten ordnungsgemäß geschützt sind.</span><span class="sxs-lookup"><span data-stu-id="a9d11-140">It's the responsibility of those storing and controlling access to data to ensure that it's properly secured.</span></span> <span data-ttu-id="a9d11-141">Häufig schreiben gesetzliche Vorgaben die Steuerung und die Prozesse vor, die zur Gewährleistung von Vertraulichkeit, Integrität und Verfügbarkeit von Daten erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="a9d11-141">Often, there are regulatory requirements that dictate the controls and processes that must be in place to ensure the confidentiality, integrity, and availability of the data.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="a9d11-142">![Bild einer Datei im Netzwerk](../media/2-application.png)</span><span class="sxs-lookup"><span data-stu-id="a9d11-142">![Image of a file on the network](../media/2-application.png)</span></span>
  :::column-end:::
    <span data-ttu-id="a9d11-143">:::column span="3"::: **Anwendung**</span><span class="sxs-lookup"><span data-stu-id="a9d11-143">:::column span="3"::: **Application**</span></span>

- <span data-ttu-id="a9d11-144">Stellen Sie sicher, dass Anwendungen sicher vor und frei von Sicherheitsrisiken sind.</span><span class="sxs-lookup"><span data-stu-id="a9d11-144">Ensure applications are secure and free of vulnerabilities.</span></span>
- <span data-ttu-id="a9d11-145">Speichern Sie vertrauliche Anwendungsgeheimnisse auf einem sicheren Speichermedium.</span><span class="sxs-lookup"><span data-stu-id="a9d11-145">Store sensitive application secrets in a secure storage medium.</span></span>
- <span data-ttu-id="a9d11-146">Erklären Sie Sicherheit zu einer Entwurfsanforderung für alle Anwendungsentwicklungen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-146">Make security a design requirement for all application development.</span></span>

<span data-ttu-id="a9d11-147">Integrieren Sie Sicherheit in den Anwendungsentwicklungszyklus, um die Anzahl der im Code eingeführten Sicherheitsrisiken zu verringern.</span><span class="sxs-lookup"><span data-stu-id="a9d11-147">Integrating security into the application development life cycle will help reduce the number of vulnerabilities introduced in code.</span></span> <span data-ttu-id="a9d11-148">Bestärken Sie alle Entwicklungsteams darin, dafür zu sorgen, dass ihre Anwendungen standardmäßig sicher sind, und dass Sicherheitsanforderungen nicht verhandelbar sind.</span><span class="sxs-lookup"><span data-stu-id="a9d11-148">We encourage all development teams to ensure their applications are secure by default, and that they're making security requirements non-negotiable.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="a9d11-149">![Ein Terminal, das Compute darstellt](../media/2-compute.png)</span><span class="sxs-lookup"><span data-stu-id="a9d11-149">![A terminal representing compute](../media/2-compute.png)</span></span>
  :::column-end:::
    <span data-ttu-id="a9d11-150">:::column span="3"::: **Compute**</span><span class="sxs-lookup"><span data-stu-id="a9d11-150">:::column span="3"::: **Compute**</span></span>

- <span data-ttu-id="a9d11-151">Schützen Sie den Zugriff auf virtuelle Computer.</span><span class="sxs-lookup"><span data-stu-id="a9d11-151">Secure access to virtual machines.</span></span>
- <span data-ttu-id="a9d11-152">Implementieren Sie Endpoint Protection, und halten Sie alle Systeme immer auf dem neuesten Stand.</span><span class="sxs-lookup"><span data-stu-id="a9d11-152">Implement endpoint protection and keep systems patched and current.</span></span>

<span data-ttu-id="a9d11-153">Durch Malware, nicht gepatchte und nicht ordnungsgemäß geschützte Systeme ist Ihre Umgebung offen für Angriffe.</span><span class="sxs-lookup"><span data-stu-id="a9d11-153">Malware, unpatched systems, and improperly secured systems open your environment to attacks.</span></span> <span data-ttu-id="a9d11-154">Der Fokus dieser Ebene liegt darin, dafür zu sorgen, dass Ihre Computeressourcen sicher und die notwendigen Kontrollen eingerichtet sind, um Sicherheitsprobleme zu minimieren.</span><span class="sxs-lookup"><span data-stu-id="a9d11-154">The focus in this layer is on making sure your compute resources are secure, and that you have the proper controls in place to minimize security issues.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="a9d11-155">![Drei verbundene Systeme, die ein Netzwerk darstellen](../media/2-networking.png)</span><span class="sxs-lookup"><span data-stu-id="a9d11-155">![Three connected systems representing networking](../media/2-networking.png)</span></span>
  :::column-end:::
    <span data-ttu-id="a9d11-156">:::column span="3"::: **Netzwerk**</span><span class="sxs-lookup"><span data-stu-id="a9d11-156">:::column span="3"::: **Networking**</span></span>

- <span data-ttu-id="a9d11-157">Schränken Sie die Kommunikation zwischen Ressourcen ein.</span><span class="sxs-lookup"><span data-stu-id="a9d11-157">Limit communication between resources.</span></span>
- <span data-ttu-id="a9d11-158">Verweigern Sie Aktionen standardmäßig.</span><span class="sxs-lookup"><span data-stu-id="a9d11-158">Deny by default.</span></span>
- <span data-ttu-id="a9d11-159">Schränken Sie eingehenden und ggf. ausgehenden Zugriff auf das Internet ein.</span><span class="sxs-lookup"><span data-stu-id="a9d11-159">Restrict inbound internet access and limit outbound, where appropriate.</span></span>
- <span data-ttu-id="a9d11-160">Implementieren Sie eine sichere Verbindung mit lokalen Netzwerken.</span><span class="sxs-lookup"><span data-stu-id="a9d11-160">Implement secure connectivity to on-premises networks.</span></span>

<span data-ttu-id="a9d11-161">Der Schwerpunkt dieser Ebene liegt darauf, die Netzwerkkonnektivität für alle Ressourcen einzuschränken, um nur das zu ermöglichen, was erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="a9d11-161">At this layer, the focus is on limiting the network connectivity across all your resources to allow only what is required.</span></span> <span data-ttu-id="a9d11-162">Durch die Einschränkung dieser Kommunikation verringern Sie das Lateral Movement-Risiko in Ihrem Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="a9d11-162">By limiting this communication, you reduce the risk of lateral movement throughout your network.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="a9d11-163">![Eine physikalische Barriere, die den Netzwerkumkreis darstellt](../media/2-perimeter.png)</span><span class="sxs-lookup"><span data-stu-id="a9d11-163">![A physical barrier representing the network perimeter](../media/2-perimeter.png)</span></span>
  :::column-end:::
    <span data-ttu-id="a9d11-164">:::column span="3"::: **Umkreis**</span><span class="sxs-lookup"><span data-stu-id="a9d11-164">:::column span="3"::: **Perimeter**</span></span>

- <span data-ttu-id="a9d11-165">Aktivieren Sie einen Schutz vor verteilten Denial-of-Service-Angriffen (DDoS), um umfangreiche Angriffe zu filtern, bevor es zu einem Denial-of-Service bei Endbenutzern kommt.</span><span class="sxs-lookup"><span data-stu-id="a9d11-165">Use distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for end users.</span></span>
- <span data-ttu-id="a9d11-166">Verwenden Sie Umkreisfirewalls, um böswillige Angriffe auf Ihr Netzwerk zu erkennen und zu melden.</span><span class="sxs-lookup"><span data-stu-id="a9d11-166">Use perimeter firewalls to identify and alert on malicious attacks against your network.</span></span>

<span data-ttu-id="a9d11-167">Beim Netzwerkumkreis geht es um den Schutz vor Angriffen auf das Netzwerk und somit auf Ihre Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-167">At the network perimeter, it's about protecting from network-based attacks against your resources.</span></span> <span data-ttu-id="a9d11-168">Die Identifizierung dieser Angriffe, die Beseitigung ihrer Auswirkungen und die Warnung, wenn sie auftreten, sind wichtige Möglichkeiten, um Ihr Netzwerk sicher zu halten.</span><span class="sxs-lookup"><span data-stu-id="a9d11-168">Identifying these attacks, eliminating their impact, and alerting you when they happen are important ways to keep your network secure.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="a9d11-169">![Ein Badge, der einen sicheren Zugriff darstellt](../media/2-policies-and-access.png)</span><span class="sxs-lookup"><span data-stu-id="a9d11-169">![A badge representing a secure access](../media/2-policies-and-access.png)</span></span>
  :::column-end:::
    <span data-ttu-id="a9d11-170">:::column span="3"::: **Richtlinien und Zugriff**</span><span class="sxs-lookup"><span data-stu-id="a9d11-170">:::column span="3"::: **Policies and access**</span></span>

- <span data-ttu-id="a9d11-171">Steuern Sie den Zugriff auf die Infrastruktur und die Änderungssteuerung.</span><span class="sxs-lookup"><span data-stu-id="a9d11-171">Control access to infrastructure and change control.</span></span>
- <span data-ttu-id="a9d11-172">Verwenden Sie SSO (Single Sign-On, einmaliges Anmelden) und Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="a9d11-172">Use single sign-on and multi-factor authentication.</span></span>
- <span data-ttu-id="a9d11-173">Überwachen Sie Ereignisse und Änderungen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-173">Audit events and changes.</span></span>

<span data-ttu-id="a9d11-174">Bei der Ebene „Richtlinien und Zugriff“ geht es darum, die Sicherheit von Identitäten zu gewährleisten, nur erforderlichen Zugriff zu gewähren und Änderungen zu protokollieren.</span><span class="sxs-lookup"><span data-stu-id="a9d11-174">The policy and access layer is all about ensuring identities are secure, access granted is only what is needed, and changes are logged.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="a9d11-175">![Eine Überwachungskamera, die physische Sicherheit darstellt](../media/2-physical-security.png)</span><span class="sxs-lookup"><span data-stu-id="a9d11-175">![A security camera representing physical security](../media/2-physical-security.png)</span></span>
  :::column-end:::
    <span data-ttu-id="a9d11-176">:::column span="3"::: **Physische Sicherheit**</span><span class="sxs-lookup"><span data-stu-id="a9d11-176">:::column span="3"::: **Physical security**</span></span>

- <span data-ttu-id="a9d11-177">Die physische Gebäudesicherheit und die Steuerung des Zugriffs auf Computerhardware im Datencenter ist die erste Verteidigungslinie.</span><span class="sxs-lookup"><span data-stu-id="a9d11-177">Physical building security and controlling access to computing hardware within the data center is the first line of defense.</span></span>

<span data-ttu-id="a9d11-178">Bei der physischen Sicherheit geht es darum, physische Schutzmaßnahmen gegen den Zugriff auf Ressourcen zu treffen.</span><span class="sxs-lookup"><span data-stu-id="a9d11-178">With physical security, the intent is to provide physical safeguards against access to assets.</span></span> <span data-ttu-id="a9d11-179">Dadurch wird sichergestellt, dass andere Ebenen nicht umgangen werden und angemessen auf Verlust oder Diebstahl reagiert wird.</span><span class="sxs-lookup"><span data-stu-id="a9d11-179">This ensures that other layers can't be bypassed, and loss or theft is handled appropriately.</span></span>
  :::column-end:::
:::row-end:::

## <a name="summary"></a><span data-ttu-id="a9d11-180">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="a9d11-180">Summary</span></span>

<span data-ttu-id="a9d11-181">Wir haben gesehen, dass Azure eine Hilfe für viele Ihrer Sicherheitsprobleme darstellt.</span><span class="sxs-lookup"><span data-stu-id="a9d11-181">We've seen here that Azure helps a lot with your security concerns.</span></span> <span data-ttu-id="a9d11-182">Die Sicherheit ist aber weiterhin eine **gemeinsame Aufgabe**, für die beide Seiten verantwortlich sind.</span><span class="sxs-lookup"><span data-stu-id="a9d11-182">But security is still a **shared responsibility**.</span></span> <span data-ttu-id="a9d11-183">Wie hoch hierbei unser Anteil an der Verantwortung ist, hängt davon ab, welches Modell wir in Bezug auf Azure verwenden.</span><span class="sxs-lookup"><span data-stu-id="a9d11-183">How much of that responsibility falls on us depends on which model we use with Azure.</span></span>

<span data-ttu-id="a9d11-184">Wir nutzen die Ringe der *tiefgehenden Verteidigung* als Richtlinie, um zu ermitteln, welche Schutzmaßnahmen für unsere Daten und Umgebungen geeignet sind.</span><span class="sxs-lookup"><span data-stu-id="a9d11-184">We use the *defense in depth* rings as a guideline for considering what protections are adequate for our data and environments.</span></span>