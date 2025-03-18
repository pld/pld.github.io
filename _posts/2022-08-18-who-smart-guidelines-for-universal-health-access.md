---
layout: post
title: WHO Smart Guidelines for Universal Health Access
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

Half of the world’s population is <a href="https://www.who.int/news/item/13-12-2017-world-bank-and-who-half-the-world-lacks-access-to-essential-health-services-100-million-still-pushed-into-extreme-poverty-because-of-health-expenses">unable to obtain essential health services</a> or the typical healthcare services offered in large facilities. The rise of community health workers and community health service programs have been transformative, but they are at the limits of their ability to improve outcomes. <!--more-->In our work in underdeveloped nations around the world, we have heard community health workers report being overburdened and saddled with increasing responsibilities.

Recent developments show a realization that providing health services to 4 billion underserved people will require transitioning to digital tools, including smartphones, for data collection and service delivery tracking. As the smartphone’s availability and capability has increased, it has become a critical tool for delivering healthcare, especially to those at the limits of existing health system service networks. Both healthcare practitioners visiting homes and based in facilities use healthcare apps to register, monitor, and deliver services to patients. These apps and the smartphones they run on function as off-line capable EMRs with use-case specific features for the particular health services they are delivering.

Most of the smartphone apps used in global healthcare store information in ad-hoc proprietary formats, and implement healthcare workflows that are not codified at the software level. This lack of standards limits and significantly increases the cost and technical sophistication needed to share resources — be they data, software, or processes and procedures — between independent or collaborating projects using healthcare apps, which hurts the long term viability of digital health tools. (Programs like Digital Square’s Global Goods were created to solve this exact problem). In addition, part of what holds organizations back from deploying apps based on standards like FHIR is the lack of mature tooling to run FHIR on smartphones. We worked with WHO and Google to create a set of innovations to solve these obstacles.

<img src="/assets/images/2022-08-18/fhircore-smart-guidelines.png" alt="FHIR and DAKs" width="600px" />

The WHO Smart Guidelines are a framework for computable healthcare guidelines that use FHIR to define the recommended algorithms for health protocols, such as antenatal care. To bring these guidelines to healthcare projects we have been collaborating with Google on the foundational layer needed for FHIR compatible healthcare apps, called the <a href="https://github.com/google/android-fhir/">Android FHIR SDK</a>, which implements the FHIR API on Android smartphones.

Called OpenSRP FHIR Core, the innovation leverages the WHO SMART Guidelines, in combination with the Android FHIR SDK, to create the first configurable platform on Android that keeps all data, as well as all meaningful rendering and business logic, in the FHIR format and uses this for storage, queries, and execution.

In Liberia, where FHIR Core is being piloted, <a href="https://www.unicef.org/liberia/child-maternal-and-newborn-health">11,000 children under 5 die every year</a>. Globally the WHO estimates that there are <a href="https://www.who.int/news-room/fact-sheets/detail/levels-and-trends-in-child-under-5-mortality-in-2020">5 million children under 5</a> who died of <a href="https://www.who.int/news-room/fact-sheets/detail/children-reducing-mortality">preventable and treatable causes</a>. The pilot targets reproductive, maternal, newborn, and child health, and aims to eliminate avoidable child deaths through better tracking or health information and timely targeting of treatments.

Our hope and goal is to reduce the number of Liberian children under 5 deaths, and through this learn lessons to apply to our work with partners in other countries and international health organizations to reduce the number of global children under 5 deaths. Ultimately, reaching the underserved populations will require many pieces to fit together. With FHIR and the WHO SMART Guidelines, our goal is to make it easier to coordinate a cooperative and unified effort.