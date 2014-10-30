# Learn about client session

##### In this repository I will be sharing the information I came across when learning about sessions in node and hapi.

---

Before anything else, to create sessions, it is necessary to understand cookies;
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
