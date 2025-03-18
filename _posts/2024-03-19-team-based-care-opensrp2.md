---
layout: post
title: Team-based care with OpenSRP 2
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

## Introduction to team-based care

Team-based care is a model of health care delivery where health professionals come together to provide comprehensive and coordinated care for a patient. Team-based care aims to improve the quality and continuity of care, increase efficiency, and reduce administrative burden by sharing health records and patient-centric workflows among health practitioners. In 2022, the Patrick J. McGovern Foundation awarded Ona with a grant to build a suite of FHIR-native digital health tools to accelerate team-based care in Indonesia. Led by the Summit Institute for Development (SID), who also received a grant from Grand Challenge Canada for team-based care, Ona has developed OpenSRP apps for midwives (BidanKu app), vaccinators (VaksinatorKu app), and community health workers (CHWs - KaderKu app)—using a standardized data model and shared database—to provide coordinated care for patients in communities and facilities across Indonesia.

## Vision behind team-based care

For over a decade, SID and Ona have been applying technology to improve health care outcomes through the digitization of patient data and health care workflows, the integration of diagnostics and laboratory information systems, and the implementation / publication of impactful research and training methodologies. One pillar of our collaboration is to build out the plug-and-play suite of platforms and integrations needed to bring patient-centered team-based care to the communities where it can most significantly reduce mortality and morbidity. Rebuilding the OpenSRP product has allowed us to flexibly deliver apps purpose-built for the health worker teams that SID works alongside in Indonesia.

Collaboration between midwife, vaccinator, and CHW is essential to ensure patients receive high quality care. Midwives play a crucial role in providing antenatal care to pregnant mothers, in part by monitoring the health of the mother and baby during pregnancy. The midwife also assists the pregnant mother in delivery and provides postnatal care to both the mother and newborn. The vaccinator is responsible for administering the correct vaccinations to people from 0 to 18 years of age, and following the guidelines defined by the Indonesian Pediatric Society and required by the Indonesian Ministry of Health. The CHW is a community-based volunteer who cares for children, pregnant women, teenagers and the elderly. They provide education and counseling on nutrition, remind people to visit the Posyandu (these are community-based integrated health posts established for a day per month), and provide complementary food for pregnant women based on their nutritional status and the village policy.

<img src="/assets/images/2024-03-19/location-hierarchy-diagram.png" alt="" width="600px"/>

*Figure 1: Midwives and vaccinators are assigned at the village level and responsible for patients in all the sub-villages. CHWs are assigned at the sub-village level and responsible for patients in a particular sub-village.*

These frontline health care workers collaborate through:

* Information sharing: Midwives, vaccinators, and CHWs share information about pregnancies, births and immunizations in assigned locations.
* *Referrals: CHWs can refer patients (e.g. those needing ANC care, PNC follow up, assistance during delivery, or seeking follow up for minor illnesses) to midwives, and those seeking immunizations to a vaccinator or  midwife.

Figure 1 shows how different healthcare workers are assigned at different levels in the administrative hierarchy, with access to different groups of patients in their respective villages or catchment areas.

Some of the challenges reported by health workers, government supervisors, and patients, when using the current health information system in Indonesia, include:

* Data quality challenges, such as data clumping, heaping, and other health record inaccuracies;
* Limited and slow access to health records, leading to delayed or unavailable data analysis;
* Non-synchronized data due to limited internet connection;
* When using paper records, risk of damage or loss of the records themselves;
* Limited or no ability to share data and communicate between systems;
* Data is for reporting only not for providing feedback to frontline workers, supervisors and community members nor for taking actions in a real time basis;
* Difficulty managing patients at scale. Health workers need to manage thousands of patients and schedule visits manually on paper, which has led to missed appointments for essential health services.

<img src="/assets/images/2024-03-19/menu-screen.jpg" alt="" width="223px"/>
<img src="/assets/images/2024-03-19/profile-screen.jpg" alt="" width="223px"/>

*Figure 2: The left panel shows the main menu in the BidanKu app, where midwives can select the particular set of clients they are interested in viewing. The right panel shows the patient view for a synthetic patient and the dropdown menu with actions to take for that synthetic patient.*

To address these challenges, SID and Ona developed three FHIR-native OpenSRP 2 apps that enable team-based care between three health care workers, later expanding to additional front line health care workers. The initial three apps are:

* BidanKu for midwives to use in primary health care centers and during Posyandu,
* VaksinatorKu for vaccinators to use during Posyandu and service delivery at primary care facilities (Puskesmas)s, and
* KaderKu for community health workers (CHWs) to use during Posyandu and in household visits.

Figure 3 shows how the three apps are used in overlapping locations that are part of the patients care journey.

<img src="/assets/images/2024-03-19/care-theaters-diagram.png" alt="" width="600px"/>

*Figure 3: Midwives, vaccinators, and CHWs operate in overlapping locations, making information sharing essential to providing efficient patient-centered care.*

## Shared data = patient centered care

The three apps — BidanKu, VaksinatorKu, and KaderKu — all synchronize their transactional health data, such as patient records, and health workflow data, with the same health data store. This ensures that the most up to date data is synced to the health data store. If a health care worker is providing services to the same patient they can view the latest information on that patient.

<img src="/assets/images/2024-03-19/app-system-design.png" alt="" width="600px"/>

*Figure 4: FHIR-native components communicate directly with the health data store, which can be used to store shared health records (SHRs) as well as patient, facility, and other registries. These systems can use various intermediaries to communicate with additional external systems, both apps and clinical electronic medical record systems (EMRs).*

The health data store can integrate with direct to client apps, through web apps, smartphone apps, or messaging platforms, like WhatsApp. For example, caregivers can fill in the details of sick child assessment forms from their phones at home, and then a midwife and CHW can access those assessments in OpenSRP 2 to view their symptoms, a preliminary diagnosis, and follow-up actions.

## OpenSRP 2 is a platform for team-based apps

Each of these apps achieves their unique user-based functionality through configurations written in standards-based FHIR files. This gives us a well defined separation between the platform (OpenSRP 2) that runs the apps and the apps themselves. This allows SID, Ona, and future collaborators to continue working together to build additional apps tailored to more health care workers and related service providers, all of whom are essential to delivering unified team-based care at the community level.

The other unique separation of responsibilities, which we have implemented through OpenSRP 2 and demonstrated in this work, is between the apps and where health information is stored. Using an off-the-shelf FHIR store for health system data allows seamless interoperability between the apps and external systems that understand FHIR. This lets the apps function as different “views” of the data, instead of silos holding health vertical or worker specific information.

<img src="/assets/images/2024-03-19/app-vs-content.png" alt="" width="600px"/>

*Figure 5: Reference workflow content, is combined with reference worker content and the latest app features to produce an app with the correct health workflow and worker content for the Indonesian context, while producing generic and reusable materials.*

For at least the past decade, team-based care has been widely discussed in digital health, but to our knowledge it has never been deployed in a global health context supported by smartphone apps. Collaborating closely with SID, an experienced institution for health program implementation, as well as with the health care workforce members delivering care has allowed us to ground the features required for any team-based care platform in reality. Building on-top of a standards-based platform has allowed us to define the features and configurations required for team-based care in a way that goes beyond the specific location, health care workers, and health care workflows we are currently targeting.

Written in collaboration with:

Yuni Dwi Setiyawati
CEO, Summit Institute for Development

Edward Sutanto
DPhil Student, Nuffield Department of Medicine, University of Oxford

Anuraj Shankar
Research fellow, Nuffield Department of Medicine, University of Oxford