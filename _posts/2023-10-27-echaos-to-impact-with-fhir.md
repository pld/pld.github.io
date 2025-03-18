---
layout: post
title: From e-Chaos to sustainable health impact with FHIR
categories:
- General
tags: []
author_id: 2
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

<em>Digital health works exactly as it was designed and that’s the problem</em>

In a recent <a href="https://jogh.org/2022/jogh-12-04090">article</a> in the Journal of Global Health, Karamagi et al. describe digital health as in a state of <i>e-Chaos</i>. They demand digital health projects “stop further duplication, [and instead] encourage interventions that holistically strengthen the health systems.” Despite remarkable progress in digital health, we believe the industry faces significant obstacles to greater impact if we continue with business as usual — and instead propose a holistic solution built around the FHIR standard.
<h2>What’s broken with digital health?</h2>
In digital health’s long history of projects, technical and implementation choices have been pragmatic, guided by (1) available technology, (2) implementation-specific requirements such as “must work offline”, and (3) per-project funding. While some projects have successfully solved important problems and created measurable impact, nice-to-have goals such as interoperability and reusable content were unfulfilled and health challenges remained unsolved at a health systems level.

Several of our projects worked like this: a group focusing on improving childhood immunizations through community health workers wants a mobile app. However, in practice, immunizations were discovered to be covered by several other touchpoints such as health facilities and campaigns from special interest NGOs, with each group using their own software. Unsurprisingly, we would be asked to send and receive data from these other systems and these requests would be treated as “integration features” — just another requirement added during the development process. Sound familiar?

This common scenario means maintaining interoperability requires each new system to integrate with every existing system, leading to an exponential increase in effort and cost, which makes large-scale interoperability infeasible. To combat this, the digital health community has coalesced around two solutions: <i>hubs</i> and <i>monoliths</i>.
<h2><i>Hubs</i> and <i>Monoliths</i>: a little better than building integration features</h2>
<i>Integration hubs</i> are platforms meant to connect different systems. Tools such as OpenHIM address this specifically for health, while data integration tools like Airbyte, Beam, NiFi, and OpenFN are for generic use cases. Instead of integrating one program’s solution to another’s, they both integrate with the hub, which is an improvement but comes with its own challenges. Each program-to-hub integration still requires additional integration work, and for other solutions to benefit, they must also integrate to the same hub. Hubs also face a “cold start problem.” If no other program has connected to the integration hub, why bother connecting this program. Since future benefits are unknown and there is no immediate payoff, this is usually the first type of scope to be cut.

<i>Monolithic interoperability</i> is the approach of using a single platform (often with a proprietary data and workflow format) for every app and system component. This works for single projects in isolation, however because of the myriad of features required to scale – from supply chain to civil registration – you cannot build a health system on a single application. Even still, having two programs run the same platform does not ensure they are integrated, leading again to siloed and overlapping systems. Figure 1 below shows the siloed health system architectures that we end up with today using direct integration, the hub, or the monolith approach.

<img src="/assets/images/2023-10-27/silos.png" alt="" width="600" />
<p><i>Figure 1: each column represents a different digital health program. Traditional digital health architecture is siloed and requires custom adapters that are often never built.</i></p>

<h2>FHIR = better than hubs and monoliths</h2>
Hub and monolith architectures have led to digital health solutions that are not designed to address health challenges from a <i>health systems</i> standpoint, which makes sense since they were designed to solve problems from a project-perspective. What is missing is not to add an integration feature, an integration hub, or a monolithic solution, but to have integration between facility and the community apps be unavoidable, out-of-the-box, and by default without additional effort or cost. Sounds impossible?

Thankfully the global health standards community has already done a lot of the work. To break down the silos and move forward we need to use platforms and tools that build around a common architecture where integration is not something to be added but a given — built into the system itself. The FHIR standard provides that architecture.

HL7 FHIR, the globally recognized health data and workflow standard, provides the opportunity to create a new generation of digital health systems that overcome traditional interoperability challenges. FHIR can represent both the app's logic and underlying data model. With recently added mobile support, through Google’s <a href="https://developers.google.com/open-health-stack">Open Health Stack</a>, FHIR provides a fundamentally new type of architecture built around a common shared data model that puts interoperability at its core.

<img src="/assets/images/2023-10-27/interop-layers.png" alt="" width="600" />
<i>Figure 2: a standards-based digital health architecture combines reusable building blocks based on a common standard.</i></p>
Interventions can create reusable FHIR content to describe the healthcare workers, healthcare workflows, and their connections, and contribute to an evolving ecosystem of innovation that does not depend on the specific organization or tools used in the implementation. Any platform that understands FHIR can load that intervention and its generated data, integrate it with other FHIR data or systems, and execute it.
<h2>FHIR gives us coordination by default</h2>
While hubs and monoliths have led to “unintentional and extreme duplication of digital tools which implies a lack of a coordinated approach and weak partnerships” (Karamgi et al.), FHIR avoids this by making <i>standards-based interoperability</i> a prerequisite.

Consider a ministry of health working with partner organizations to implement a program for the prevention of mother to child HIV transmission. One organization may have an app for maternal health, such as antenatal care visits, while a second organization has their own app for HIV management. To limit the risk of mother to child transmission these apps need to work together. Let's take a look at how to integrate this data under the 3 solutions we’ve discussed:
<ol>
 	<li aria-level="1">With the hub approach, an integration hub is set up that both programs have to be aware of and have access to; then these programs must create or implement connections to that hub. The programs must also agree on a common language for the information they want to share.</li>
 	<li aria-level="1">In the monolith approach, the programs use the same proprietary platform, and then they must either integrate the data of one program completely with the other or write an integration that continuously synchronizes data between the two systems. To have a useful integration they will still need to ensure that both systems represent information in the same way.</li>
 	<li aria-level="1">With a standards-based approach, where both programs store their data in FHIR, the different programs are alternative ways to view and manage the same underlying shared health records. There’s one FHIR server set up and both programs can query and push data into it.</li>
</ol>
<img src="/assets/images/2023-10-27/multi-app.png" alt="" width="600" />
<i>Figure 3: a facility app used by a nurse, and a community app used by a community health worker, are alternative ways to view, manage, and contribute to the same set of shared health records.</i></p>
One way to think of a FHIR health systems architecture is as a set of interlocking tiles that connect <i>because</i> of, not <i>in spite</i> of, their structure. Like Lego pieces, they are built to be interoperable with each other. Programs and countries that are adopting FHIR-native platforms can add on new modules over time, and be confident that their data integrates with other FHIR tools.
<h2>Packaging FHIR for sustainable impact</h2>
By transitioning to digital health architectures built around standard based systems that can store a shared health record for each client that interacts with the healthcare system, programs and countries open the door to standard packages of reusable content. For example, the <a href="https://github.com/WorldHealthOrganization/smart-immunizations">SMART Immunization Guidelines</a> created by the WHO, or the <a href="https://ona.io/home/who-anc-smart-guidelines-in-indonesia/">Antenatal Care SMART Guidelines</a> implemented in OpenSRP, are computable – or “machine readable” — healthcare guidelines that can be run on any application that can interpret and execute FHIR, as depicted below in Figure 4.

<img src="/assets/images/2023-10-27/digitalization-pathway.png" alt="" width="600" />
<i>Figure 4: the SMART Guidelines provide a standards-based common language for building reusable healthcare workflows that can be combined like Lego pieces.</i></p>
Organizations running digital health programs, and the countries implementing them contribute to the growing set of computable health packages, all defined in the same FHIR-based format. These packages are plug-and-play. If a program is running a FHIR-based electronic immunization register in their primary healthcare facilities, when they want to expand it to community outreach they don’t need to transfer any data, they simply point their FHIR-native community app at the same shared health records they are using in their primary healthcare facilities.

There are many challenges leading to the current “e-Chaos” holding back digital health interventions. However, with FHIR, the SMART Guidelines, and community-driven global goods, we have all the tools, concepts, and architectures we need to reduce that chaos. The critical next step in this journey is to move beyond digitizing health <i>apps</i> to digitizing the health <i>systems</i> that those apps exist within.