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


#### Explain how cookie based authentication works
##### Notes
##### Refs
- https://edward-huang.com/authentication/tech/2019/09/10/all-you-need-to-know-about-authentication-is-here/
- https://swagger.io/docs/specification/authentication/cookie-authentication/
- https://www.yegor256.com/2015/05/18/cookie-based-authentication.html
- https://auth0.com/docs/sessions-and-cookies/spa-authenticate-with-cookies 


#### Explain how a Java MVC web framework works.
##### Notes
##### Refs
- https://javarevisited.blogspot.com/2017/06/how-spring-mvc-framework-works-web-flow.html#:~:text=xml%20and%20finds%20the%20Servlet,MVC%20based%20Java%20web%20application.
- https://www.tutorialspoint.com/spring/spring_web_mvc_framework.htm
- https://stackify.com/spring-mvc/


#### Walk me through the process of TLS encryption (high level.) Explain certs, cipher suites, and certificate authorities.
##### Notes
The exact steps within a TLS handshake will vary depending upon the kind of key exchange algorithm used and the cipher suites supported by both sides. The RSA key exchange algorithm is used most often. It goes as follows:

- The 'client hello' message: The client initiates the handshake by sending a "hello" message to the server. The message will include which TLS version the client supports, the cipher suites supported, and a string of random bytes known as the "client random."
- The 'server hello' message: In reply to the client hello message, the server sends a message containing the server's SSL certificate, the server's chosen cipher suite, and the "server random," another random string of bytes that's generated by the server.
- Authentication: The client verifies the server's SSL certificate with the certificate authority that issued it. This confirms that the server is who it says it is, and that the client is interacting with the actual owner of the domain.
- The premaster secret: The client sends one more random string of bytes, the "premaster secret." The premaster secret is encrypted with the public key and can only be decrypted with the private key by the server. (The client gets the public key from the server's SSL certificate.)
Private key used: The server decrypts the premaster secret.
- Session keys created: Both client and server generate session keys from the client random, the server random, and the premaster secret. They should arrive at the same results.
- Client is ready: The client sends a "finished" message that is encrypted with a session key.
- Server is ready: The server sends a "finished" message encrypted with a session key.
- Secure symmetric encryption achieved: The handshake is completed, and communication continues using the session keys.

All TLS handshakes make use of asymmetric encryption (the public and private key), but not all will use the private key in the process of generating session keys. For instance, an ephemeral Diffie-Hellman handshake proceeds as follows:

- Client hello: The client sends a client hello message with the protocol version, the client random, and a list of cipher suites.
- Server hello: The server replies with its SSL certificate, its selected cipher suite, and the server random. In contrast to the RSA handshake described above, in this message the server also includes the following (step 3):
- Server's digital signature: The server uses its private key to encrypt the client random, the server random, and its DH parameter*. This encrypted data functions as the server's digital signature, establishing that the server has the private key that matches with the public key from the SSL certificate.
- Digital signature confirmed: The client decrypts the server's digital signature with the public key, verifying that the server controls the private key and is who it says it is. Client DH parameter: The client sends its DH parameter to the server.
- Client and server calculate the premaster secret: Instead of the client generating the premaster secret and sending it to the server, as in an RSA handshake, the client and server use the DH parameters they exchanged to calculate a matching premaster secret separately.
- Session keys created: Now, the client and server calculate session keys from the premaster secret, client random, and server random, just like in an RSA handshake.
- Client is ready:
- Same as an RSA handshake.
- Server is ready
- Secure symmetric encryption achieved

##### Refs
- https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/
- https://security.stackexchange.com/questions/20803/how-does-ssl-tls-work
- https://blog.ivanristic.com/SSL_Threat_Model.png
- https://www.altaro.com/hyper-v/public-key-infrastructure/
- https://www.thesslstore.com/blog/cipher-suites-algorithms-security-settings/
- https://www.garykessler.net/library/crypto.html

#### What is kerberoasting?
##### Notes
Kerberoasting is a technique which exploits a weakness in the Kerberos protocol when requesting access to a service. 

- The user authenticates with the Key Distribution Centre (the Domain Controller in this case) using an AS-REQ packet.
- The KDC validates the user credentials and if valid, returns a Ticket Granting Ticket (TGT).
- When the user wants to authenticate to a service such as IIS, a request is made to the Ticket Granting Service (TGS) containing the TGT and the Service Principal Name (SPN) of the service to be accessed.
- If the TGT is valid and has not expired, a TGS creates a service ticket for the target service. The service ticket is encrypted with the credentials of the service account.
- A TGS response is sent to the user with the encrypted service ticket.
- The service ticket is finally forwarded to the service, which is decrypted by the using the service account credentials.

##### Refs
- https://www.qomplx.com/qomplx-knowledge-kerberoasting-attacks-explained/
- https://blog.xpnsec.com/kerberos-attacks-part-1/
- https://www.blackhillsinfosec.com/a-toast-to-kerberoast/
- https://www.hackingarticles.in/deep-dive-into-kerberoasting-attack/


#### What is a golden ticket? 
##### Notes
A Golden Ticket attack is a type of attack in which an adversary gains control over an Active Directory Key Distribution Service Account (KRBTGT), and uses that account to forge valid Kerberos Ticket Granting Tickets (TGTs).

Whatever the circumstances, once an attacker has a foothold on a network, they can start laying the groundwork for a Golden Ticket Attack. This involves:

- Reconnaissance to gather information about the domain, such as the domain name and domain security identifier (SID), both of which are relatively easily obtained by a whoami command on Windows.
- Acquisition of local administrator-level access to the domain controller in order to steal an NTLM hash of the Key Distribution Service account (KRBTGT). An attacker may -obtain access to the Domain Controller, and then run a tool such as Mimikatz to harvest the credential. Optionally, attackers might use other password-grabbing attacks such as Pass-the-Hash or DC Sync to obtain the KRBTGT password hash from the domain controller without first authenticating to it.
- With the password hash for the Key Distribution Service account, the Golden Ticket Attack can be launched. Mimikatz creates a relative ID (RID) in Active Directory, supplies an account username for impersonation, and ultimately, obtains a Kerberos Ticket Granting Ticket (TGT), which gives the threat actor access to the domain controller as a domain administrator. These privileges allow the attacker access to any domain, group, or resource on the network.
- An attacker can set the ticket to be valid for any time period, up to 10 years (tickets are generally valid only for a few hours) granting them indefinite persistence as a legitimate user with a valid ticket that is virtually undetectable because it does not appear to be malicious traffic. However, sophisticated attackers with “Golden Ticket” access may choose not to employ extended validation periods so as to avoid detection.

##### Refs
- https://www.qomplx.com/qomplx-knowledge-golden-ticket-attacks-explained/#:~:text=A%20Golden%20Ticket%20attack%20is,Ticket%20Granting%20Tickets%20(TGTs).
- https://resources.infosecinstitute.com/active-directory-walkthrough-series-golden-ticket/
- https://en.hackndo.com/kerberos-silver-golden-tickets/


#### What is a silver ticket?
##### Notes
A Silver Ticket is a forged service authentication ticket. A hacker can create a Silver Ticket by cracking a computer account password and using that to create a fake authentication ticket. ... In the simplest terms, a Silver Ticket is a forged authentication ticket that allows you to log into some accounts

- Conduct reconnaissance to gather information about the domain, such as the domain name and domain security identifier (SID), both of which are relatively easily obtained by a whoami command on Windows.
- Obtain the DNS name under which the service principal name (SPN) for the targeted, local service they wish to attack is registered as well as the service type.
- Use Mimikatz or a similar tool to obtain the local NTLM password (or password hash) for the Kerberos service running on the compromised system, for example: Windows file share, SQL, email, Microsoft Sharepoint and so on. Service password hashes can be obtained from a number of sources on a compromised local system. For example, they can be dumped from the local computer’s Security Account Manager (SAM) or local service account.
- Obtain the unencrypted password for the service. These can be obtained from the hash using methods like offline cracking (“Kerberoasting”) to obtain the unencrypted password data.
- Use Mimikatz or a similar tool to forge a Kerberos Ticket Granting Service (TGS) ticket allowing the attacker to authenticate to the targeted service.
- Authenticate to the local service directly using the credentials and forged TGS.
- Manipulate the TGS to elevate the attacker’s permissions to that of Domain Administrator.

##### Refs
- https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-silver-tickets
- https://www.qomplx.com/qomplx-knowledge-silver-ticket-attacks-explained/
- https://resources.infosecinstitute.com/active-directory-series-silver-ticket/
- https://en.hackndo.com/kerberos-silver-golden-tickets/ 
