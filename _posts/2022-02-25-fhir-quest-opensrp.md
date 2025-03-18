---
layout: post
title: FHIR-native case management with Quest and OpenSRP
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

HL7 FHIR provides a standardized and popular way for digital health systems to represent health data and  associated processes. We are excited to introduce Quest, an open source app that lets you use FHIR to define forms and capture data to take advantage of the growing Android FHIR and WHO SMART guidelines ecosystem.

<img src="/assets/images/2022-02-25/quest_ecosystem.png" alt="Quest ecosystem" width="600px">

As digital health platforms embrace FHIR, the barriers to interoperability will decrease, making it possible to interact with patient data across different health systems to inform clinical decisions and coordinate care. Adoption of FHIR also enables semantic interoperability, i.e. the ability to exchange and understand data with unambiguous, shared meaning across systems. This standardization and aggregation of data is needed for health systems to generate and operationalize ML/AI driven insights.

Key to FHIR’s ability to collect standardized data is the use of digital forms, rendered using the [FHIR Questionnaire resource](https://www.hl7.org/fhir/questionnaire.html). Questionnaires support complex clinical logic and the ability to map data elements to medical terminology codes like ICD11. We can map the data captured in FHIR Questionnaires directly to other FHIR resources (such as Patients, Observations, etc) making them ideal for creating FHIR native health applications.

While the FHIR implementation guide for [Structured Data Capture](https://build.fhir.org/ig/HL7/sdc/) (SDC) is a well defined specification, digital tools that accessibly capture FHIR data natively are still largely non-existent. To address this we created Quest (short for Questionnaire), a digital health app-runner built upon the [Android FHIR SDK](https://github.com/google/android-fhir). Quest makes it possible for non-technical users to develop and implement FHIR native data collection and case management apps.

Using Quest a person with no programming experience can design and deploy a simple data collection or case management app using FHIR Questionnaires they have authored. In developing Quest, we have initially focused on (1) enabling FHIR native on and off-line data collection on mobile devices, and (2) adding support for equivalent data capture capabilities via web forms. To promote data security, Quest will support the administration of data collection via authenticated users and secure, encrypted stores on FHIR compatible clouds and servers, such as [Google’s Cloud Healthcare API](https://cloud.google.com/healthcare-api/docs/concepts/fhir) and [HAPI FHIR](https://hapifhir.io/). These data stores support programmatic export and API based access to collected FHIR data, simplifying integration with external analysis and monitoring platforms.

We are excited for these tools to lower the barrier to adopting FHIR native apps. We have been aggressively working with a great team of technical and implementing partners who are bringing the benefits of FHIR to healthcare and other projects around the globe. We welcome you to join Ona and our partners in contributing and discussing the implementation strategy on the [FHIR Core code repository](https://github.com/opensrp/fhircore), including iterating on early drafts of the [Quest documentation](https://github.com/opensrp/fhircore/tree/main/android/quest).