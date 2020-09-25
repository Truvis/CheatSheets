#### What are the types of Cross-site scripting?
##### Notes
###### Stored XSS (Persistent XSS)
An attacker uses Stored XSS to inject malicious content (referred to as the payload), most often JavaScript code, into the target application. If there is no input validation, this malicious code is permanently stored (persisted) by the target application, for example within a database. For example, an attacker may enter a malicious script into a user input field such as a blog comment field or in a forum post.

When a victim opens the affected web page in a browser, the XSS attack payload is served to the victim’s browser as part of the HTML code (just like a legitimate comment would). This means that victims will end up executing the malicious script once the page is viewed in their browser.

###### Reflected XSS (Non-persistent XSS)
 the attacker’s payload has to be a part of the request that is sent to the web server. It is then reflected back in such a way that the HTTP response includes the payload from the HTTP request. Attackers use malicious links, phishing emails, and other social engineering techniques to lure the victim into making a request to the server. The reflected XSS payload is then executed in the user’s browser.

Reflected XSS is not a persistent attack, so the attacker needs to deliver the payload to each victim. These attacks are often made using social networks.

###### DOM-based XSS
s an advanced XSS attack. It is possible if the web application’s client-side scripts write data provided by the user to the Document Object Model (DOM). The data is subsequently read from the DOM by the web application and outputted to the browser. If the data is incorrectly handled, an attacker can inject a payload, which will be stored as part of the DOM and executed when the data is read back from the DOM.

A DOM-based XSS attack is often a client-side attack and the malicious payload is never sent to the server. This makes it even more difficult to detect for Web Application Firewalls (WAFs) and security engineers who analyze server logs because they will never even see the attack. DOM objects that are most often manipulated include the URL (document.URL), the anchor part of the URL (location.hash), and the Referrer (document.referrer).

###### XSS Discovery and Prevention
Cross-site Scripting is a very old technique but XSS vulnerabilities remain one of the most common ones on the web. They are still mentioned by the Open Web Application Security Project (OWASP) as one of the top-10 security risks.

An easy way to test if your website or web application is vulnerable to XSS and other vulnerabilities is to run an automated web scan using the Acunetix vulnerability scanner, which includes a specialized XSS scanner module. Take a demo and find out more about running XSS scans against your website or web application.

##### REFS:
- https://portswigger.net/web-security/cross-site-scripting
- https://owasp.org/www-community/Types_of_Cross-Site_Scripting
- https://sucuri.net/guides/what-is-cross-site-scripting/

#### Explain the difference between encoding and escaping
##### Notes
Encoding is when you transform between a logical representation of a text ("logical string", e.g. Unicode) into a well-defined sequence of binary digits ("physical string", e.g. ASCII, UTF-8, UTF-16). Escaping is a special character (typically the backslash: '\') which initiates a different interpretation of the character(s) following the escape character; escaping is necessary when you need to encode a larger number of symbols to a smaller number of distinct (and finite) bit sequences.

#### What is cross-site request forgery? What causes it?
##### Notes


##### Refs
- https://www.netsparker.com/blog/web-security/csrf-cross-site-request-forgery/
- https://portswigger.net/web-security/csrf
- https://owasp.org/www-community/attacks/csrf
- https://www.acunetix.com/websitesecurity/csrf-attacks/
- https://seclab.stanford.edu/websec/csrf/csrf.pdf

#### Explain the nature and root cause of XML external entity injection attacks
##### Notes

##### Refs
- https://www.acunetix.com/blog/articles/xml-external-entity-xxe-vulnerabilities/#:~:text=XXE%20vulnerabilities%20are%20caused%20by,out%2Dof%2Dband%20XXE.
- https://portswigger.net/web-security/xxe
- https://owasp.org/www-community/vulnerabilities/XML_External_Entity_(XXE)_Processing
- https://research.cs.wisc.edu/mist/SoftwareSecurityCourse/Chapters/3_8_4-XML-Injections.pdf


