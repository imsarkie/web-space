---
title: How to secure your database
source: https://ubuntu.com/blog/secure-database
author:
  - "[[Mohamed Wadie Nsiri]]"
published:
created: 2025-10-06
description: Learn how to apply the NIST framework to enforce a secure database approach from identification, protection and detection stages to response and recovery.
tags:
  - clippings
draft: true
---
Your submission was sent successfully! [*Close*](https://ubuntu.com/blog/#)

Your preferences have been successfully updated. [*Close notification*](https://ubuntu.com/blog/#)

This article was last updated **2 years ago**.

---

Cybersecurity threats are increasing in volume, complexity and impact. Yet, organisations struggle to counter these growing threats. Cyber attacks often intend to steal, damage, hijack or alter value-generating data. In this article around database security, we use the [[NIST framework]] to lay out the common controls that you can implement to secure your databases. Let’s start by discussing the potential impact of unsecured databases.
## How bad can an unsecure database be?

The cost of a single data breach reached an average of $4.35 million in 2022, according to [IBM’s Cost of a Data Breach](https://www.ibm.com/reports/data-breach) report. At the same time, the number of organisations that are ready to efficiently meet today’s security risks is as low as 15%, according to [Cisco’s Cybersecurity Readiness Index](https://www.cisco.com/c/dam/m/en_us/products/security/cybersecurity-reports/cybersecurity-readiness-index/2023/cybersecurity-readiness-index-report.pdf). Given the previous numbers, it should not surprise you that the *World Economic Forum* placed cybersecurity failures as the most concerning technological risk in its [Global Risks Report for 2022](https://www3.weforum.org/docs/WEF_The_Global_Risks_Report_2022.pdf).  

Before digging into the typical controls we can implement around a database management system (i.e. DBMS), we will go over the typical threat mediums.  

## Cyber attack mediums

When a malicious person is trying to attack a database, they might leverage one of the following mediums.

### Physical medium

An attacker with physical access to the hardware hosting the target database can be tempted to steal, for example, the storage devices and try to reverse engineer the data stored in the concerned piece of hardware.  

We might be tempted to think that this type of attack is unlikely to happen. Yet, a [study conducted by Blancco in 2019](https://www.blancco.com/blancco-reveals-42-of-used-drives-sold-on-ebay-are-holding-sensitive-data/) revealed that 42% of purchased second hand drives contained personal data.  

According to [IBM’s Cost of a Data Breach](https://www.ibm.com/reports/data-breach) report, physical security compromises accounted for around 9% of the data breaches’ initial vectors.  

Let’s now move to the next medium in cyber attacks, software.  

### Software medium

In our digital world, most attacks involve a form of software. This can be malicious software that is injected into the targeted victim’s environment (e.g. a virus, a malware), a software vulnerability (i.e. a bug that can be exploited by a cyber attacker) or misconfigured software that could leave security holes for the malicious actor to exploit.  

According to [IBM’s Cost of a Data Breach](https://www.ibm.com/reports/data-breach) report, vulnerabilities in third party software and misconfigurations account for nearly 28% of the initial attack vectors. Unfortunately, the number of software vulnerabilities keeps rising, so such attacks might become even more popular among malicious actors.  

It is important to understand that an attacker might use vulnerabilities affecting the DBMS directly but also any software component that can be used by a legit user (application or human) to interact with the database either locally (e.g. the Operating System) or remotely via network calls.  

Let’s now cover the most used attack medium in cyberattacks, human factors.

### Human medium

According to [IBM’s 2023 Threat Intelligence Index](https://www.ibm.com/downloads/cas/DB4GL8YM), 41% of the reported incidents involve phishing for initial access. Phishing is a form of social engineering aiming at tricking its victims into revealing sensitive information that will be used later to conduct a cyberattack. Even more worrying, The *World Economic Forum’s* [Global Risks Report for 2022](https://www3.weforum.org/docs/WEF_The_Global_Risks_Report_2022.pdf) found that 95% of cybersecurity issues are traced to human error.  

Human errors can consist of falling into a social engineering trap or failing to define and follow proper security processes to protect the sensitive data. Let’s go over some of the most common attack types, including the ones targeting human factors.  

## Cyber attack types

The following table lists some of the common cyber attacks and techniques:  

| **Attack step\***              | **Category\***                        | **Attack**                                                 | **Description**                                                                                                           | **Main** **medium**                                  |
| ------------------------------ | ------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Initial access                 | Phishing                              | Malicious   attachment and/or link                         | Uses social engineering to trick the victim into downloading malicious agents (virus, malware…).                          | Human                                                |
| Initial access                 | Vishing                               | Fraudulent   calls, sms …                                  | Uses social engineering to trick the victim into providing sensitive information over interactive channels.               | Human                                                |
| Initial access                 | Exploit   Public Facing   Application | SQL injection                                              | Uses vulnerabilities in a public-facing application to run queries that are not legitimately authorised.                  | Software                                             |
| Initial access                 | Hardware   addition                   |                                                            | Uses illegitimate hardware to connect to the victim’s network.                                                            | Hardware                                             |
| Initial access                 | Supply chain   compromise             | DevOps tools, software repositories   and hardware   parts | Alters software or hardware dependencies to alter the behaviour of the resulting application to gain illegitimate access. | Software and Hardware                                |
| Credential access   Collection | Man in the   middle                   | Sniffing                                                   | Corrupts a network device to steal or deviate exchanged information from its intended targets.                            | Software                                             |
| Credential access              | Brute force                           | Password guessing, cracking …                              | Gets a valid credential by trying common or leaked secrets or by using an artefact of the secret (e.g. its hash).         | Human   (usually due to poor training and processes) |
| Impact                         | Denial of   Service                   | Flooding/   Exhausting                                     | Renders a targeted service inoperable by overloading it with illegitimate traffic.                                        | Software                                             |

(\*) As per [MITRE ATT&CK®](https://attack.mitre.org/)

Now that we are familiar with some of the common cyber attacks, let’s dive into the different controls you need to implement to secure your database.

## Applying the NIST framework to secure your databases

In [its cybersecurity framework](https://www.nist.gov/cyberframework/online-learning/five-functions), NIST defines 5 pillars or functions to cover all the activities and measures around securing your digital assets: Identify, Protect, Detect, Respond and Recover.

We will use these pillars in the NIST framework to classify the typical controls we need to implement to secure your data stores.

### Identify

The first step in any effort to secure your data is to know its content, where it is stored, which systems can consume it and what the applicable regulations and standards are. In order to achieve the above, you need to consider the following:

- Create and maintain an inventory of your assets. A tool with [Configuration Management DB](https://en.wikipedia.org/wiki/Configuration_management_database) and auto-discovery capabilities is highly recommended.
- Create and maintain an application dependency map to assess who is consuming your data. This can be achieved throughout your CMDB tool or using a dedicated tracing tool (e.g. [Jaeger](https://www.jaegertracing.io/)) that can help you visualise the flows between your applications. Adopting a more structured approach of expressing connections between workloads would be even better with a solution like [Canonical’s Juju](https://juju.is/). Juju is an open source orchestration engine. It has a built-in [integration](https://juju.is/docs/juju/integration) mechanism to relate workloads and track their dependencies (and not only guess them using logs or inventory data).
- Classify your databases according to the type of stored data. This is important to understand the regulations that apply to your data, and to isolate your data into different security perimeters. For instance, you may choose to classify data as:
	- Personally Identifiable Information (a.k.a. PII data)
	- Financial data (e.g. credit card data, transactions)
	- Other…

After understanding your data and its legitimate consumers, the next step would be to start implementing all the measures to proactively prevent its theft, alteration or deterioration.

### Protect

Let’s go over the typical measures you need to implement to protect your data.

#### Train your staff

As we discussed earlier, most cybersecurity issues involve a human factor. Therefore, it is important to regularly train your teams so that they understand:  

- The damage that cybersecurity attacks can cause to them and to their company.
- Typical social engineering based attacks.
- Processes they need to abide by to prevent such attacks.
- Process they need to follow when they suspect being victim to such attacks.

#### Implement database authentication

All database products come with built-in database authentication. You should opt for one that supports password-based authentication, at least, and has built-in LDAP/Kerberos integration. Our recommended approach is to use:

- LDAP integration to authenticate your human users. Most companies use a solution that supports LDAP. It is better to reuse the existing controls (e.g. password policy, account lifecycle) rather than reinventing them on the database side. We also recommend using MFA authentication for human users.
- Secret store (e.g. [AWS’ secrets manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html), [Conjur](https://www.conjur.org/)) to store the credentials of your robotic users (e.g. application users, monitoring users). Then, leverage managed identities (e.g. [Azure managed identity](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview)) or a certificate to allow the hosting machines to fetch the required credentials and expose them to the databases. It is recommended to ensure that a secret gives access to as few resources as possible. For example, using one secret to access all your databases can significantly increase the impact radius of a theft of that particular secret.

#### Implement database authorisation

Most database products are shipped with a decent role management functionality. Roles are a set of predefined permissions that are used to ease the management burden. We recommend to have the following roles:  

| **Role** | **Granted permissions** | **Typical users** |
| --- | --- | --- |
| **STATS** | Read specific statistics-related tables (e.g. v$tables in oracle, performance schema in MySQL). | Monitoring agents. |
| **READ** | Read the applicative tables’ content. | Developers working on the application populating or using the concerned tables. |
| **DML** | The Data Manipulation Language role grants the permissions to read, insert/add, update and delete the content of existing tables. | Applications using and populating the tables’ content. |
| **DDL** | The Data Definition Language role grants the permissions needed to modify the structure of the database (e.g. adding a column/table). | Automation users for managing database structure. For example, it can be assigned to versioning tools such as [Liquibase](https://github.com/liquibase/liquibase) and [Flyway](https://flywaydb.org/). |
| **REPLICA** | Set up replication for the database. | Automation users for managing replication. |
| **BACKUP** | Backup or export data. | Automation users for managing backups. |
| **DBA** | Full administration rights to the database. | Should be restricted to a very small group of people (e.g. the administrators in charge of the concerned database). |

#### Use network services to isolate your databases and segregate its consumers

Once you implement the database’s built-in authentication and authorisation mechanisms, you can start implementing more layers of defence. Let’s focus on a few best practices related to the networking layer:

- Databases must be deployed in a private subnet that is not exposed to the internet.
- Databases should be placed in different firewalled network zones (e.g. subnets) depending on the criticality and nature of their data (e.g. credit card holding databases should be placed in a dedicated zone).
- Segregate the legitimate traffic to your database based on the privileges level using, for example, different network interfaces:
	- One interface for management tasks to be used by DBAs and automation users. Access through this interface should only be accessible through specific [bastion hosts](https://en.wikipedia.org/wiki/Bastion_host).
	- One interface for database-to-database communications.
	- One interface for application and developer induced traffic.
- Restrict the hosts that can access your database using IP ranges to limit the attack surface.
- Change the default port of your databases and close all unneeded ports. The number of opened ports can be reduced by dedicating a number of hosts to your database instances and removing any unneeded database services or agents.
- In a public cloud, you need to use private links when using the cloud services (e.g. for storing your backups) to ensure that your traffic remains within the public cloud’s dedicated network.

#### Isolate your database from other colocated workloads

When colocating several workloads in the same host, sandboxing your database instances can mitigate some vulnerabilities affecting your databases at the cost of additional components (and therefore attack surfaces).

For example, you can use [LXD](https://ubuntu.com/lxd) to run and manage your databases within [LXC containers](https://en.wikipedia.org/wiki/LXC). You can also deploy your database in a [confined snap](https://snapcraft.io/docs/snap-confinement) (e.g. [PostgreSQL](https://snapcraft.io/charmed-postgresql), [MySQL](https://snapcraft.io/charmed-mysql)) to limit the permissions granted to your database processes.

#### Encrypt your data

Encryption is another important layer of defence. We already detailed the various levels of encryption and their benefits in [this guide](https://ubuntu.com/engage/database-cloud-migration). In this blog, we summarise the main ideas:

- Encrypt data when it is transferred over the network (a.k.a. on the wire encryption) using TLSv1.2+ and use a certificate manager to handle the lifecycle of the certificates.
- Encrypt the data when it is sitting on durable storage (a.k.a. at rest encryption) using database, filesystem or disk level encryption. You should favour the encryption at the highest stack level possible (e.g. filesystem is better than disk).
- Encrypt data in-memory using confidential VMs.
- Encrypt at the client side when you can better control them (compared to the database servers) and when you are ready to deal with the limitations on the server side (e.g. loss of most analytical and comparison features).

Successfully configuring your database to follow best practices in regards to authentication, authorisation, networking, sandboxing and encryption is a major step towards securing your database. Yet, it is equally important to secure the software dependencies of your chosen database solution.

#### Secure your database software supply chain

It is important to secure the packages that you use in your software stack. You can secure those packages by using “private” mirrors that are placed behind your own firewalls. The idea is to ensure that any used package was certified centrally before being exposed to the consuming applications (typically using a proxy). For example, an [air-gapped snap store](https://docs.ubuntu.com/snap-store-proxy/en/airgap) is a solution to manage and expose snaps without the need for a permanent internet connection for all the hosts where you need to deploy snaps.

Before making a package available to the rest of your network, we recommend to:

- Certify the authenticity of your software packages by, for example, checking the checksum of the downloaded package against the provider’s checksum (check [this example](https://ubuntu.com/tutorials/how-to-verify-ubuntu#1-overview) for verifying Ubuntu images).
- Run a [vulnerability scanner](https://owasp.org/www-community/Vulnerability_Scanning_Tools) to ensure that no major known vulnerability will be introduced in your environment.

#### Promptly fix your database software vulnerabilities

Any software package is subject to security bugs. You need to have a process in place to regularly update your software to fix any security issue that affects your software stack.  

With zero-day exploits nearly [doubling in 2021](https://www.technologyreview.com/2021/09/23/1036140/2021-record-zero-day-hacks-reasons/) and with [80% of public exploits](https://unit42.paloaltonetworks.com/state-of-exploit-development/) being published before their CVEs, it is no longer enough to regularly apply security fixes – you need to do so as fast as you can.  

If you’re an Ubuntu user looking for secure software, you can rely on [Ubuntu Pro](https://ubuntu.com/pro) to get up to 10 years patching for more than 25,000 packages including PostgreSQL, MySQL and several other databases. Ubuntu Pro also comes with [Livepatch](https://ubuntu.com/security/livepatch), which ensures a timely roll-out of critical patches without needing an immediate reboot of your hosts. It also provides [tools](https://ubuntu.com/tutorials/comply-with-cis-or-disa-stig-on-ubuntu#2-installing-the-ua-client) to harden your OS following the most stringent compliance regimes and security standards like CIS, DISA-STIG and FedRAMP.  

Hardening your OS is the first step in hardening your environment. The next one should be hardening your databases.  

#### Harden your database deployments

[Hardening](https://ubuntu.com/engage/a-guide-to-infrastructure-hardening) a software component is mainly about reducing its attack surface as much as possible. Typically, we would remove any unneeded service, close unused ports and change default settings (e.g. passwords, accounts).  

In our upcoming whitepapers, we will detail the changes you need to apply to your databases to meet the [CIS security benchmark](https://www.cisecurity.org/cis-benchmarks/).  Stay tuned by [subscribing to our newsletter](https://ubuntu.com/blog?category=white-papers#posts-list).  

Now that we covered the main actions we need to undertake to protect our software stack, we will next cover the measures to put in place to promptly detect security issues in your databases.  

### Detect

In order to promptly fix any security issue concerning your data, you need to monitor your environment to detect:  

- Suspicious behaviours (e.g. too many unsuccessful authentications or privilege escalations).
- Vulnerabilities in your already deployed software.

In order to monitor suspicious activities, you need to implement:

#### Database auditing

Auditing is a requirement within many security frameworks including PCI-DSS.Most popular database products have an auditing functionality that is either built-in or provided by an extension. The functionality consists of writing specific database actions into a specified destination (e.g. file). For example, the [pgAudit](https://www.pgaudit.org/) extension provides extensive auditing capabilities for PostgreSQL databases. Similarly, MySQL’s [query\_log](https://dev.mysql.com/doc/refman/8.0/en/query-log.html) can be used to have a database audit.

#### User actions monitoring

You also need to monitor the actions of the user on the host containing the database. Once a user gains root privileges to the OS, it is only a matter of time before gaining privileged access to the hosted databases. Therefore, it is important to monitor the actions of the user at the OS level. This can be achieved, for example, by:  

- Assigning a unique id for every user.
- Using the [sudoers file](https://en.wikipedia.org/wiki/Sudo#Configuration) to configure the allowed actions for every user or group.
- Enforcing the usage of [jump servers](https://en.wikipedia.org/wiki/Jump_server) to connect to specific parts of your network.
- Send all ssh and sudo logs to a central location for analysis.

#### Buy or build an SIEM solution

Once we automate the collection of audit data for the OS and the database, we need to send them to a centralised security information and event management(a.k.a. SIEM) solution to detect suspicious patterns. For example, you can centralise your logs into a [Spark](https://ubuntu.com/data/spark) cluster and run your own custom rules to detect specific suspicious behaviours (e.g. A sudden surge of human induced deletes of data, a lot of failed login attempts, suspicious changes in user’s connection timestamps).  

Once your monitoring of suspicious activities is in place, you need also to monitor the vulnerabilities in your deployed software.  

#### Monitor the vulnerabilities in your software stack

Software vulnerabilities are published daily and a software version that was believed to be safe one day can become a security threat the day after. Therefore, it is important to keep track of new vulnerabilities. Once again, [Ubuntu Pro](https://ubuntu.com/pro) helps you detect which packages need an update (check [this tutorial](https://ubuntu.com/pro/tutorial) for an example) and allows you to seamlessly update the covered software packages.  

Ubuntu also publishes [Open Vulnerability and Assessment Language (OVAL)](https://ubuntu.com/security/oval) data that can help you programmatically assess your security posture. You can also use our [CVE reports](https://ubuntu.com/security/cves) to search for specific CVEs.  

Now that you are ready to detect security issues, you need to have the processes to respond to them. Let’s dig into some details.  

#### Respond

There is no generic way to respond to a security incident as the response depends highly on the nature and the impact of the incident. Yet, you can have a process that can guide you and your organisation in these, often, chaotic situations:  

- Create a checklist of simple remediations you can try (e.g. terminating user sessions, revoke permissions from a user, disconnect a machine from your network, shutdown servers).
- Create a template for the internal communication you need to send per type of impact (data stolen, corrupted or damaged data …).
- Involve any legal or communication specialist to assist with your external interactions.

It is also important to document and rehearse your planned responses to a security incident.

After detecting a security incident, your initial focus should be to “stop the bleeding” and prevent the propagation of the issue to other systems. Your next focus should be recovering any damaged data or degraded services.

### Recover

We cannot state it enough but a backup is often the ultimate (and sometimes the only) recovery solution for data-related incidents. This [detailed guide](https://ubuntu.com/engage/data-backups) can help you in setting up a comprehensive backup strategy or improve your existing one. It is also important to have a post-mortem session where the lessons learned are documented, the security gaps are identified and timely addressed. It is also important to notify any end user that might have been affected by the security incident.

## Conclusion

In this article, we covered the probable consequences of improperly secured data. We provided an overview of the common security attacks and mediums. We detailed some of the activities and measures you can implement to secure your databases, following the NIST framework.  

At Canonical, we can assist you in securing your data and your business. Please [contact us](https://ubuntu.com/support) to learn more.  

#### Should you use open-source databases?

You are not the only one asking this seemingly popular question! Several companies are torn between the rise in appeal of open-source databases and the...

#### Patterns to achieve database High Availability

The cost of database downtime A study from ManageForce estimated the cost of a database outage to be an average of $474,000 per hour. Long database outages...

#### Let’s play: sharded big data PostgreSQL

Everyone knows that if you’ve got big data, you need Apache Hadoop, right? It’s an affordable, horizontally scalable, clustered data processing platform ideal...