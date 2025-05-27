# Output handling
- Handling the output from a web application is exactly the same as passing data to subsystems
	- The final subsystem we pass data to is the **visitor's browser**, and the **HTML Parser** in the browser is just another system
# Cross-site scripting (XSS)
- XSS is about tricking a web server into presenting **malicious HTML**, typically **script code**, to a user
	1. The intention is often to **steal session information**, and thus be able to contact the site on behalf of the victim.
	2. Scripts may also be used to **change** the contents of web pages in order to displays **false information** to the visitor, and it may be used to redirect forms so that secret data are posted to the attacker’s computer
- XSS generally attacks **the user** of the web application, **not the application itself**
	- The attacks are possible when the web application **lacks proper output filtering**
# XSS attack phases
- In general, XSS attacks are conducted in a cycle of five substantial phases
	- **Gathering info**: Attackers make **deep research** and **analysis** on the target (vulnerable web service VWS, and/or a victim)
	- **Planning**: **Identify** and **make** a concrete choice of the potential VWS and/or client (victim)
	- **Choosing**: The attacker **develops the payload** of malicious code MC to penetrate the target’s defense
	- **Delivery**: **Deliver** an XSS attack to the target (installing the payload of MC in the target)
	- **Data exfiltration**: **Transfer** sensitive **personal information** of the target to the attacker
# XSS subcategories
- XSS has three subcategories. Each subcategory is defined by the mechanism used to inject malicious code (MC):
	- **Reflected XSS**
		- Targets a single user
		- Occurs when user input is immediately returned by a web application in an error message, search result, or any other response. **MC is not stored**
	- **Persistent XSS**
		- Targets any user
		- Occurs when user input is stored on the target server, such as in a database. then a victim can retrieve the stored data from the web application. **MC is stored on the server**
	- **DOM-based XSS**
		- Targets a single user
		- the source of the data is in the DOM, the sink is also in the DOM. **Data flow including MC never leaves the browser**
# XSS types
- XSS attacks can exploit vulnerabilities of servers and/or clients
	- **Server XSS**: In this case, the server will generate a response including **malicious code** that can come directly from a **user request** or from a **stored location**
	- **Client XSS**: In this case, the client will update the Document Object Model (DOM) using **malicious code** that comes directly from the DOM or from a **response of the server** (MS could be from a request or a from a stored location)

| XSS       | Server               | Client               |
| --------- | -------------------- | -------------------- |
| Stored    | Stored server XSS    | Stored client XSS    |
| Reflected | Reflected server XSS | Reflected client XSS |
# XSS-based session hijacking
- As cookies are available to a script, XSS may be used to hijack cookie-based sessions
- If a bad guy gets access to someone else’s session cookie, he may often appear as that someone to the server by installing the cookie in his own browser
- A victim logging in to a web site will get a unique session ID cookie
- The attacker wants that cookie to impersonate the victim
- How does the attacker get to the cookie?
## The mechanism
- Four steps are needed in the simplest possible XSS-based session hijacking.
- The wanted cookie exists only in communication between the **victim** and the **target web server**
- For a script to successfully access this cookie, it will have to be included in pages sent from the web server **directly** to the victim’s browser
	1. The attacker first joins a discussion, **entering a note** that contains some cookie-stealing JavaScript. The web server stores the note in its **internal database**. Later, another user, the victim, logs in to the discussion site. Upon logging in, he receives his personal session ID from the web server
	2. When the user asks to read the attacker’s note, the web server builds a web page containing the note text, **including the malicious script**. This page is then passed to the victim
	3. As part of displaying the web page, the victim’s browser will also **run** the script. The script picks up the **cookie** that is associated with the web page, i.e. the cookie containing the **session ID**, and immediately passes the cookie to the attacker’s computer
	4. After receiving the cookie, the attacker installs it in his own browser, and visits the discussion web server. The web server receives the stolen session ID from the attacker, and thinks it is talking to the victim. The attacker now fully **impersonates** the victim on the discussion site
## The malicious script
- The malicious script makes the browser of the victim pass **the cookie** to the computer owned by the attacker
- Passing the cookie is most easily done using a script that **redirects** the browser to a web server running on the attacker’s computer, taking the cookie with it on the journey
## Stealth
- To hide the theft, the attacker’s web server may generate a response containing a new redirect that immediately sends the browser **back to the original site**
# How to avoid XSS
- Since Cross-site Scripting is a **metacharacter problem**, we will have to do something to the metacharacters to make them lose their meaning
	- We have to escape them in some way, and when dealing with HTML, the escaping is called **HTML encoding**
## When
- Many people choose to handle the XSS problem at **input time**
- Cross-site Scripting is clearly a **data passing problem**, so it should be dealt with at **the time data is passed**
	- For HTML that time is whenever our **application generates some output**
- There are at least three good reasons for delaying the HTML filtering to output time:
	1. It is not just user generated input that must be HTML encoded. When reading data from a file, from a database or any other external source, HTML encoding should be done **before passing the content to the client**. It is easier to remember doing the filtering if the rule is ‘‘filter output when output is to be done’’
	2. When filtering at input time, any incoming data that is stored in a database will be HTML encoded. Any **non-HTML part** of the application that uses the same database (e.g. an invoice printing unit, to be overly creative) will have to remove the HTML encoding
	3. HTML encoding expands **data strings**. The expansion may give **surprising results** when incoming data are stored in restricted length database fields, which is common practice
# HTML filtering
- There are generally three options depending on the data:
	1. If **data is not supposed to contain markup** at all, we simply HTML encode them before passing them to the client
	2. If the user **should be allowed to enter some markup** but not the dangerous constructs, it gets quite hard. We will need to look at all tags and attributes and let some through, while HTML encoding others
	3. If the application should have **full trust in the users** and allow them to enter whatever markup they like, we simply just send the data as they appear. No special handling needed, but keep the consequences in mind
# HTML encoding
- HTML encoding is the mapping of certain HTML metacharacters to their character entity equivalents:
	1. Map every occurrence of `&` to `&amp`
	2. Then replace every `"` with `&quot`
	3. Then every `<` with `&lt`
	4. And finally replace every `>` with `&gt`
- The implication of doing HTML encoding is that the browser will display data exactly as they were written