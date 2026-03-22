---
title: Cyber Attacks and NIST Framework
draft: true
tags:
  - cybersecurity
---
In this blog we'll solely focus on the cyber attacks and How [[NIST framework]] implementation protects us from the database attacks. 

## Cyber Attacks

Before digging into the topic, we will go over the typical threat mediums, When a malicious person or group is trying to attack a database, they might come through one of the following mediums.

1. Physical Medium
2. Software Medium
3. Human Medium

### Physical Medium

In this an Attacker gain the access of the physical hardware hosting the database for example, the storage devices or a piece of hardware. We might think that, this attack won't happen, yet a study revealed that 42% of purchased second hand hard disks or storage devices contains personal data and that might get stolen for malicious purposes.

According to [IBM's Cost of a Data Breach Report (2023)](https://na.ingrammicro.com/Ingram/media/North-America-US/EN-US/I/ibm/docs/Cost-of-a-Data-Breach-Report-2023.PDF), “*Physical security compromise*” is listed among the initial attack vectors. It accounts for about **6%** of breaches. The same report also includes “*lost or stolen devices*” under “Accidental data loss or lost or stolen devices,” but that is a separate category. 

### Software Medium

In our digital world, most cyber attacks were done through the form of software. This can be malicious software or a piece of code with malicious payload gets injected into the targeted device and provide unauthorized access to the bad actor, for example virus, a malware. And a software vulnerability also incur potential threat that a cyber attacker can exploit with a bug. And the final one is human error, a misconfigured software could leave security holes for the malicious actor to exploit. 

From the same [IBM's Cost of a Data Breach Report (2023)](https://na.ingrammicro.com/Ingram/media/North-America-US/EN-US/I/ibm/docs/Cost-of-a-Data-Breach-Report-2023.PDF), **Cloud misconfiguration** is an initial attack vector in about 11% of breaches. - **Known, unpatched vulnerabilities** are responsible for **just over 5%** of breaches as initial vectors. Third-party software vulnerabilities (software supply-chain compromises) are mentioned in earlier reports (e.g., 2022) at ~13%. The number of software vulnerabilities keeps rising, so much attacks might become even more popular among malicious actors.

It is important to understand that these misconfigurations and vulnerabilities might affect the DBMS directly but also any software component that holds the sensitive data.

### Human Medium

Human factor is increasingly being targeted or exploited via more refined social engineering, phishing, impersonation, deepfakes; also attackers increasingly combine human-based vectors with technical vulnerabilities. So even if technical controls are strong, gaps in culture or training often remains exploitable.

IBM’s reports consistently show phishing (*Phishing is a form of social engineering aiming at tricking its victims into revealing sensitive information for use later in a cyberattack*) as the leading method for initial access. The 41% number underscores that attackers still rely heavily on tricking people (via email or links) rather than only exploiting technical vulnerabilities. 

### Cyber Attack Types

1. Phishing - Human
2. Vishing - Human
3. Exploit Public Facing Application - Software
4. Hardware addition - Hardware
5. Supply chain compromise - Software & Hardware
6. Man in the middle - Software
7. Brute Force - Human (usually due to poor training and processes) 
8. Denial of Service - Software

## NIST framework to secure your databases

In [its cybersecurity framework](https://www.nist.gov/cyberframework/online-learning/five-functions), NIST defines 5 pillars or functions to cover all the activities and measures around securing your digital assets,

1. Identify 
2. Protect 
3. Detect
4. Respond 
5. Recover

We will use these pillars in the NIST framework to classify the typical controls we need to implement to secure your data stores.

### Identity

The Identify Function assists in developing an organizational understanding to managing cybersecurity risk to systems, people, assets, data, and capabilities. Understanding the business context, the resources that support critical functions, and the related cybersecurity risks enables an organization to focus and prioritize its efforts, consistent with its risk management strategy and business needs. 

To secure it we must have the understanding of its content, where it stored, which systems can use it and what is the application regulations and standards are. To do this we need to consider these, 

- **Create and maintain an Asset Inventory** - Creating and maintaining an **inventory of your assets** means keeping a complete, up-to-date list of all the devices, systems, applications, and data that belong to your organization.
- **CMDB and Auto-Discovery** - [[CMDB]] goes beyond just a list; it shows **how assets interact**. It stores information about your IT assets and their relationships. **Auto-discovery** tools make this process scalable by automatically scanning your environment to, detect new or changed assets in real time, identify configuration changes, sync updates into the CMDB. This automation ensures your inventory stays current.
- **Data Classification** - Classify your databases according to the type of stored data. This is important to understand the regulations that apply to your data, and to isolate your data into different security perimeters.


Example for Data Classification

| **Category**                                  | **Examples**                                        | **Protection Needed**                                      |
| --------------------------------------------- | --------------------------------------------------- | ---------------------------------------------------------- |
| Personally Identifiable Information (PII) | Names, emails, phone numbers, national IDs          | Encrypt at rest and in transit, access control, monitoring |
| Financial Data                            | Credit card info, account numbers, transaction logs | Tokenization, strong encryption, network segmentation      |
| Health Data (PHI)                         | Medical records, insurance details                  | Access control, audit trails, data minimization            |
| Internal / Confidential                   | Company documents, internal reports                 | Access control, DLP (Data Loss Prevention)                 |
| Public Data                               | Marketing material, website content                 | Basic integrity controls                                   |
Once you classify your data, you can segment your databases into different security perimeters or zones, such as:
- **Restricted zone:**  heavy monitoring, strict access control, network isolation.
- **Controlled zone:**  limited access.
- **Open zone:** standard controls.
This helps prevent **lateral movement** — even if attackers breach one database, they can’t easily reach the most sensitive ones.

### Protect

The Protect Function outlines appropriate safeguards to ensure delivery of critical infrastructure services. The Protect Function supports the ability to limit or contain the impact of a potential cybersecurity event.
