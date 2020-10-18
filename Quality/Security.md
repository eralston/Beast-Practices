# Security
---
Security standards focus on "Protecting our people and their peace of mind".

Most obviously, this includes cybersecurity and ensuring all our systems allow only authenticated and authorized users. Security also includes protecting privacy and data sovereignty, such as under the General Data Protection Regulation (GDPR). Security includes disaster recovery planning, but NOT business continuity planning. Finally, this includes managing the risk that key partners may introduce security vulnerabilities into our platforms and workflows.

It is best to remember that security is about the risk-based proactive activity to prevent and mitigate, rather than trying to create a perfect "guarantee" that nothing bad will happen.

The first goal is to be mindful of the cybersecurity environment in the world nowadays. Cybersecurity events can bring down organizations, based on the potential outcomes such as theft of IP, loss in customer confidence, and media scandal. Your organization carries insurance on the assumption to will happen one day. The question isn't "if", but "how bad". Everyone at the company must be defending their access credentials and preventing attacks through phishing and social engineering. Similarly, our systems should be designed to work within these environments -- providing direct and unambiguous awareness of this landscape.

## Security Resources
---

Some resources across the web to better understand the scope of Security:
- [General Data Protection Regulation (GDPR) *on Wikipedia*](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)
- [Web Application Security *on Wikipedia*](https://en.wikipedia.org/wiki/Web_application_security)
- [Website Security *on Mozilla Developer Network (MDN)*](https://developer.mozilla.org/en-US/docs/Learn/Server-side/First_steps/Website_security)
- [Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/Main_Page)
- [Security Principles *from OWASP*](https://www.owasp.org/index.php/Category:Principle)
- [Cheat Sheet Series Project *from OWASP*](https://github.com/OWASP/CheatSheetSeries)
- [National Cybersecurity and Communications Integration Center](https://www.us-cert.gov/)
- [Azure Trusted Cloud](https://azure.microsoft.com/en-us/overview/trusted-cloud/)
- [Web Application Hacker's Handbook](https://www.amazon.com/Web-Application-Hackers-Handbook-Exploiting/dp/1118026470)

## Security Principles in Detail
---

Here are the ten security principles in detail:

**Accountability** - Security concerns around a certain scope -- such as an information system used internally, or production system deployed for a customer -- should have a single, unambiguous owner when it comes to security. This is most strongly canonized in GDPR through the "Data Protection Officer" role. While not all organizations are obliged to have such a role, it comes from a need to have an unequivocal obligation and authority in the system.

**Is there an "owner" for the service/product/account?** If so, the owning individual should be identified in a central place.

**Is there a succession plan for if the current owner moves on?** By default, the manager in the org chart should receive all accounts on departure.

**Can the system send alerts?** Ideally, notifications should be sent to Engineering@Product.Com for unifying security events and making it so a team can respond instead of an individual.

**Can we add the LiveDevApi account as a co-owner/admin?**

**For this information system, is there a communication plan outlining the groups of people who might be informed of a security event pertaining to it?**

**Detection** -- While not everything can be prevented, almost everything can be logged. This means that detecting threats -- even those we have no ability to mitigate -- is the first step of building a risk-based framework for accountability and knowing what requires an emergency response. The [OWASP Cheat Sheet on Logging](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Logging_Cheat_Sheet.md) covers even more best practices.

**Does all logging contain full When, Where, Who, and What information?**

**Does logging NEVER contain PII, proprietary data, source code, secrets, connection strings, etc?**

**Are all production systems recording Warning and Error messages at all times?** Is it easy to elevate them to All messages during an incident?

**Do production systems send automatic alerts to owners when sufficient warnings or errors arise?**

**Are exceptions of all calls logged as "Error" level with full-stack traces?** This is automatically available with App Insights in most cases.

**Are all suspicious actions logged as "Warning"?** For instance, recoverable inconsistencies from input validation, which are likely NOT exceptions, but could indicate probing from an outside actor. For a complete rundown of Input Validation concerns, consult the [OWASP Cheat Sheet on Input Validation](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Input_Validation_Cheat_Sheet.md).

**Are there "Information" log statements for every authentication, authorization, and data access operation in the system?** This includes client-side console logging in the browser session when a secure REST call is made, along with server-side logging to a persistent log (EG, App Insights) for server-side actions. These may include GUID-based (immutable across backups) IDs of resources, but should NOT emit PII or proprietary data.

**Defense in Depth** -- In general, a system is only "secure" once one needs to violate more than one component of the system to succeed. For instance, if you have a database with encrypted information, the keys to that data should NOT go into that database, it should be stored through another means (EG, Azure Key Vault) which spreads the risk into two separate systems.

**How many components (web app code, web app config, SQL Database, Azure Storage, etc) would an attacker need to have control over to pull out PII or proprietary data from the system?** For instance, if there are encrypted values in your database, is that key stored in the same database? Ideally, it's sitting in the web.config or better yet Azure Key Vault, meaning at least two components must be compromised before any sensitive information can be decrypted.

**Are you using Azure Key Vault as the primary store for all secrets (Connection Strings, non-transient Security Tokens, etc)?**

**Principle of Least Privilege** --Each piece of the system only having minimal access to do its work and no more. For instance, if you have an application accessing a database to only do reporting, it should use a read-only user to that database.

**Are you using application-specific user accounts when accessing your SQL Database?**

**Are you using SAS tokens with a scope no greater than the tenant's data to read information from Azure Storage?**

**If you're using JWT authentication, are you requesting the minimum scope for the current action in your application?**

**Are you storing JWT tokens in secure locations?** Server-side, behind another layer of security

**Disaster Recovery Plan (DRP)** -- Having a set of steps for recovering data, a whole tenant, and potentially re-deploying the whole system for every piece of software we make. Similarly, to the extent possible in a third-party system, allowing for the configuration of the system to be re-applied to that environment in the event of a catastrophe. While cloud computing abstracts away hardware failure (EG, SQL Server hard drives), we still need redundancy in the event of application error corrupting data or natural disaster in the region preventing access.

**Is there a backup, versioning, or point-in-time restore for all persistent application state?** Restore should be 30+ days for all primary production systems, backups should be monthly after that, retained for three years.

**Is there georedundancy for all persistent application data for customers paying for premium disaster recovery?** This includes secondary SQL Database in an outside region (still within the desired jurisdiction) with 7 days restore and monthly backup. TODO: Add "Best pairings" doc on Azure redundancy

**Is there a documented process that would enable a single person to create a new region of the application in 4 hours or less?** This includes hooking up to CI/CD pipelines to receive a new LKG build of the product.

**Privacy & Personally Identifiable Information (PII)** -- While it may be obvious our systems contain proprietary data from our customers, it is important to remember they contain private data from our users. Emails, names, phone numbers, etc, all constitute PII that must be protected. Again, the most robust and specific protections and requirements are laid out in GDPR.

**Are you saving Personally Identifiable Information (PII) in this application?** This includes not only obvious PII (Full name, home address, email address, social security number, passport number, driver's license number, credit card numbers (PCI Compliance!), date of birth, telephone number, login details), but also personal information that may be useful in combination to identify someone (First or last name, country, state, city, postcode, gender, race, age range, job position, and workplace). TODO: Should report to Jonathan Green.

**Do you save a security point-of-contact in the system for receiving notifications about security events?** Under GDPR, we are required to notify customers within 72 hours of detection. Failure to do so may result in stiff penalties.

**Data Sovereignty --** While it's easy to forget that "the cloud" really just means "a datacenter somewhere", we must strive to remember that our code is running inside a country somewhere. While we don't have the time to educate everyone that government is more than just real estate with guns, we do need to meet customer expectations that their data is processed and stored in the jurisdiction of their choosing.

**Does the customer's deployed** [**region in Azure live in the country**](https://azure.microsoft.com/en-us/global-infrastructure/locations/) **that matches the expectations of their sales contract?** Does the CRM system include this data sovereignty information?

**Cryptography** -- All data should be encrypted in transit and at rest. Unless you have a PhD in Computer Science and/or Math, you should not write your own cryptographic algorithm. Cryptography in JavaScript is probably dumb. Writing your own cryptographic algorithm in JavaScript is grounds for immediate dismissal.

**Have you required HTTPS everywhere?**

**Have you enabled encryption on all Azure resources?** EG, TDE for SQL Database, Encrypting setting for Azure Storage

**Are you following key management best practices?** Here is the [OWASP Cheat Sheet on Key Management](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Key_Management_Cheat_Sheet.md).

**Are you using Azure Key Vault as the primary store for all secrets (Connection Strings, non-transient Security Tokens, etc)?**

**Front-End Vulnerabilities** -- A catch-all category for vulnerabilities most evidently in the handling and execution of HTML and JavaScript.

**Are you preventing Cross-Site Scripting (XSS) attack?** This includes encoding/decoding user input that is HTML code and is particularly tricky given the extensible nature of our products (where some features may be allowed XSS as designed). Check out the [OWASP Cheat Sheet on XSS Prevention](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.md).

**Avoid Eval** - Executing arbitrary code is dangerous.

**Do calls to APIs only deal in data?** Values returning from an API should be JSON and only ever pass through methods like JSON.parse(), never an eval(), or similar method assuming the response is code. For a complete perspective, check out the [OWASP Cheat Sheet on HTML5 Security](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/HTML5_Security_Cheat_Sheet.md).

**Are you storing any PII or proprietary data in localStorage or other client-side mechanisms?** There is no security around these mechanisms and all data can be inspected. These should only be used for caching non-sensitive application data and IDs for fetching sensitive data during an authorized session.

**Are you relying on third-party tags services (EG, Google Analytics, App Insights), and have you examined security best practices for managing them?** Check out the [OWASP Cheat Sheet on Tag Management](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Third_Party_Javascript_Management_Cheat_Sheet.md).

**Back-End Vulnerabilities** -- A catch-all category for vulnerabilities running on the server-side, most often in C# or SQL.

**Do you have a custom error page that prevents end-users from seeing raw exceptions, most critically stack traces?** Check out the [OWASP Cheat Sheet on Error Handling](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Error_Handling_Cheat_Sheet.md) for more.

In .Net, there are best practices around prevent common attacks such as SQL Injection (parameterized queries, Entity Framework + LINQ only), cross-site request forgery (ValidateAntiForgeryToken), and selecting strong cryptographic algorithms. Check out the [OWASP Cheat Sheet on .Net Security](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/DotNet_Security_Cheat_Sheet.md) for more.

**Are you preventing SQL Injection attack through the use of parameterized queries, stored procedures, or ORM?** Check out the [OWASP Cheat Sheet on Preventing SQL Injection](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.md).

**Are you preventing Cross-Site Request Forgery (CSRF) by using the ValidateAntiForgeryToken?** Ideally, you or your library are implementing some of the best practices in the [OWASP Cheat Sheet on CSRF](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.md).

**Does your REST API follow security best practices for whitelisting actions, safe headers in responses, and not trusting POST data that has a canonical copy on the server?** Check out the [OWASP Cheat Sheet on REST APIs](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/REST_Security_Cheat_Sheet.md).