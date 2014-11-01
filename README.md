# Learn about client session

##### In this repository I will be sharing the information I came across when learning about sessions in node and hapi.

---

Before anything else, lets understand cookies:

**(If you do not wish to learn about or already know about cookies skip ahead this section)**
- what are cookies?
- how cookies work?

> **All cookies** are subject to browser's **same-origin policy**

#### What are cookies?

In essence cookies are small pieces of data sent from a website and stored in a user's
web browser while the user is browsing the website.

#### How do cookies work?

For a quick answer to this question, every time a user loads the website, the browser
send the cookie back to the server to notify the website of the user's previous activity.

**However this answer is limited in scope and depth of how a cookie really works!
Continue reading to further understand how cookies work.**

##### Types of cookies

There are various types of cookies, as shown bellow:

- **Session Cookie** - also known as an _in-memory_ or _transient cookie_, exists only in temporary memory while the user navigates the website.
Session cookies are created by not setting an *expiry date* or *validity interval* at the cookie creation time and web browsers normally delete
these cookies when the user closes the browser.

- **Persistent Cookie** - also know as a _tracking cookie_ due to the fact that these cookies can be used to record vital pieces of information, such as
user preferences, login details, etc. If a persistent cookie has its _Max-Age_ set to one year (for example), then, during that year, the **_initial value_ set in that
cookie** would be sent back to the server **every time** the user visited the server.

- **Secure Cookie** - A secure cookie has *secure attribute* enabled and is only used via **HTTPS**. This ensures that
the cookie is always encrypted when transmitting from client to server. This makes the cookies less likely to be exposed to cookie theft.

- **HttpOnly Cookie** - The HttpOnly attribute is supported by most modern browsers. On a supported browser, an HttpOnly session cookie will be **used _only_** when
transmitting HTTP (or HTTPS) requests, thus restricting access from other, non-HTTP APIs such as JavaScript. This restriction mitigates but does not eliminate the
threat of session cookie theft via cross-site scripting (XSS). **This feature applies only to _session-management cookies_**, and not other browser cookies.

- **Third-party Cookie** - First-party cookies are cookies that belong to the same domain that is shown in the browser's address bar (or that belong to the sub
  domain of the domain in the address bar). Third-party cookies are cookies that belong to domains different from the one shown in the address bar. Web pages can feature
  content from third-party domains (such as banner ads), which opens up the potential for tracking the user's browsing history. Privacy setting options in most modern browsers
  allow the blocking of third-party tracking cookies.

- **Supercookie** - A "supercookie" is a cookie with an origin of a Top-Level Domain (such as `.com`) or a Public Suffix (such as `.co.uk`). It is important that supercookies
are blocked by browsers, due to the security holes they introduce. If unblocked, an attacker in control of a malicious website could set a supercookie and potentially disrupt or
impersonate legitimate user requests to another website that shares the same Top-Level Domain or Public Suffix as the malicious website. For example, a supercookie with an origin
of `.com`, could maliciously affect a request made to `example.com`, even if the cookie did not originate from `example.com`. This can be used to fake logins or change user information.

- **Zombie Cookie** - Some cookies are automatically recreated after a user has deleted them; these are called zombie cookies. This is accomplished by a script storing the content of
the cookie in some other locations, such as the local storage available to Flash content, HTML5 storages and other client-side mechanisms, and then recreating the cookie from backup stores
when the cookie's absence is detected.

##### Cookie Structure

Browsers are expected to support cookies where each cookie has a size of 4KB, at least 50 cookies per domain, and at least 3000 cookies total and consist of seven components:

1 - (name, value) pair of the cookie (i.e. name=value)

2 - Expiry of the cookie

3 - Path the cookie is good for

4 - Domain the cookie is good for

5 - Need for a secure connection to use the cookie

6 - Whether or not the cookie can be accessed through other means than HTTP (i.e., JavaScript)

>The first component **(name, value) _is required_** to be explicitly set.

##### Session Management

Cookies may be used to maintain data related to the user during navigation, possibly across multiple visits. Cookies were introduced to provide a way to implement a "shopping cart" (or "shopping basket"),
a virtual device into which users can store items they want to purchase as they navigate throughout the site.

Shopping basket applications today usually store the list of basket contents in a database on the server side, rather than storing basket items in the cookie itself. A web server typically sends a cookie
containing a unique session identifier. The web browser will send back that session identifier with each subsequent request and shopping basket items are stored associated with a unique session identifier.

Allowing users to log into a website is a frequent use of cookies. Typically the web server will first send a cookie containing a unique session identifier. Users then submit their credentials and the web
application authenticates the session and allows the user access to services.

>Cookies provide a quick and convenient means of client/server interaction. One of the advantages of cookies lies in the fact that they store the user information locally while identifying users simply based
>on cookie matching. The server's storage and retrieval load is greatly reduced. As a matter of fact, the possibility of applications is endless—any time personal data need to be saved they can be saved as a cookie (Kington, 1997).

#### Setting a cookie

1 - Transfer of Web pages follows the HyperText Transfer Protocol (HTTP). Regardless of cookies, browsers request a page from web servers by sending them a usually short text called 'HTTP request'.

2 - The server replies by sending the requested page preceded by a similar packet of text, called 'HTTP response'. This packet may contain lines requesting the browser to store cookies.

3 - The server sends lines of Set-Cookie only if the server wishes the browser to store cookies. `Set-Cookie` is a directive for the browser to store the cookie and send it back in future requests to the server
(subject to expiration time or other cookie attributes), if the browser supports cookies and cookies are enabled.

This is a request for another page from the same server, and differs from the first one above because it contains the string that the server has previously sent to the browser. This way, the server knows that
this request is related to the previous one. The server answers by sending the requested page, possibly adding other cookies as well.

The value of a cookie can be modified by the server by sending a new `Set-Cookie: name=newvalue` line in response of a page request. The browser then replaces the old value with the new one.

The value of a cookie may consist of any printable ASCII character (`!` through `~`, unicode `\u0021` through `\u007E`) excluding `,` and `;` and excluding `whitespace`.
The name of the cookie also excludes = as that is the delimiter between the name and value. The cookie standard RFC2965 is more limiting but not implemented by browsers.

##### Cookie attributes

Besides the name–value pair, servers can also set these cookie attributes: a cookie domain, a path, expiration time or maximum age, Secure flag and HttpOnly flag. Browsers will not send cookie
attributes back to the server. They will only send the cookie’s name-value pair. Cookie attributes are used by browsers to determine when to delete a cookie, block a cookie or whether to send a cookie (name-value pair) to the servers.

##### Secure and HttpOnly

The Secure and HttpOnly attributes do not have associated values. Rather, the presence of the attribute names indicates that the Secure and HttpOnly behaviors are specified.

The Secure attribute is meant to keep cookie communication limited to encrypted transmission, directing browsers to use cookies only via secure/encrypted connections. If a web server sets a cookie with a secure attribute from a
non-secure connection, the cookie can still be intercepted when it is sent to the user by man-in-the-middle attacks.

The HttpOnly attribute directs browsers not to expose cookies through channels other than HTTP (and HTTPS) requests. An HttpOnly cookie is not accessible via non-HTTP methods, such as calls via JavaScript (e.g., referencing "document.cookie"),
and therefore cannot be stolen easily via cross-site scripting (a pervasive attack technique).[37] Among others, Facebook and Google use the HttpOnly attribute extensively.

#### Cookie drawback

Besides privacy concerns, cookies also have some technical drawbacks. In particular, they do not always accurately identify users, they can be used for security attacks, and they are often at odds with the Representational State Transfer
(REST) software architectural style.

##### Inaccurate identification

If more than one browser is used on a computer, each usually has a separate storage area for cookies.

##### Inconsistent state on client and server

The use of cookies may generate an inconsistency between the state of the client and the state as stored in the cookie. If the user acquires a cookie and then clicks the "Back" button of the browser, the state on the browser is generally not the same as before that acquisition.

##### Inconsistent support by devices

The problem with using mobile cookies is that most devices do not implement cookies; for example, Nokia only supports cookies on 60% of its devices, while Motorola only supports cookies on 45% of its phones. In addition, some gateways and networks (Verizon, Alltel, and MetroPCS)
strip cookies, while other networks simulate cookies on behalf of their mobile devices. There are also dramatic variations in the wireless markets around the world; for example, in the United Kingdom 94% of the devices support wireless cookies, while in the United States only 47% support them.

#### Alternative to Cookies

##### HTTP Authentication

The HTTP protocol includes the basic access authentication and the digest access authentication protocols, which allow access to a web page only when the user has provided the correct username and password. If the server requires such credentials for granting access to a web page,
the browser requests them from the user and, once obtained, the browser stores and sends them in every subsequent page request. This information can be used to track the user.

##### Web Storage

Some web browsers support a script based on a persistence mechanism, which allows the page to store the information locally for later use. With HTML 5 There are two main web storage types: local storage and session storage, behaving similarly to persistent cookies and session cookies respectively.
Internet Explorer supports persistent information in the browser's history, favorites, in an XML store ("user data"), or directly within a Web page saved to disk.

##### Cache

Browser cache can also be used to store information that will be used to track the user. Until the cache is cleared, the stored resources are not reloaded. For example, serve a resource `current.js` with a unique content `var userId = 3243242`;. Each times this file will be reloaded from the cache,
its content will not change and a JavaScript code can operate it to identify the current user.

---

## Sessions

When creating a session, we need a user first, and this user needs a means to be authenticated and recognised as the user. Only once we have defined and registered a user can we proceed to creating sessions.

### Saving and loading users

When defining users there a few steps necessary to take. These are the barebones of those steps:

- Create a user model (Object);
- Add logic to load and sabe user data using you prefered database;
- Secure user passwords (using bcrypt - https://www.npmjs.org/package/bcrypt);
- Add logic to authenticate attempts to log in (hapi has several plugins for this http://hapijs.com/plugins#Authentication);

### Authenticating users



---
### Resources:
- Article on sessions with nodejs: http://blog.nodejitsu.com/sessions-and-cookies-in-node/
- Plugin for hapi.js session management with yar: https://github.com/hapijs/yar
- Plugin for hapi.js authentication with bell: https://github.com/hapijs/bell
- Managing server user session with client side single page app (**Read first answer**): http://stackoverflow.com/questions/21821937/how-to-manage-server-user-session-within-client-side-single-page-app
- Nodejs cookies and session management: http://stackoverflow.com/questions/24232234/node-js-cookies-and-session-management
- SPA best pratices: http://stackoverflow.com/questions/20963273/spa-best-practices-for-authentication-and-session-management
- About cookies: http://www.allaboutcookies.org/cookies/cookies-the-same.html
- HTTP cookies: http://en.wikipedia.org/wiki/HTTP_cookie
- Session cookies: http://www.allaboutcookies.org/cookies/session-cookies-used-for.html
- Persistent cookies: http://www.allaboutcookies.org/cookies/persistent-cookies-used-for.html
- User authentication libraries for nodejs: http://stackoverflow.com/questions/3498005/user-authentication-libraries-for-node-js
- HTTP Authentication: http://en.wikipedia.org/wiki/Basic_access_authentication
- Session ID: http://en.wikipedia.org/wiki/Session_ID
- SOAP (Simple Object Access Protocol): http://en.wikipedia.org/wiki/SOAP
- How to safely store a password: http://codahale.com/how-to-safely-store-a-password/
- BCRYPT: http://en.wikipedia.org/wiki/Bcrypt
