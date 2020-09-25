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

