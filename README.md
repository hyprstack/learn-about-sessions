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

There are various types of cookies. Those that are of interest for this tutorial, will be the first three of the following list:

- **Session Cookie** - also known as an _in-memory_ or _transient cookie_, exists only in temporary memory while the user navigates the website.
Session cookies are created by not setting an *expiry date* or *validity interval* at the cookie creation time and web browsers normally delete
these cookies when the user closes the browser.

- **Persistent Cookie** - also know as a _tracking cookie_ due to the fact that these cookies can be used to record vital pieces of information, such as
user preferences, login details, etc. If a persistent cookie has its _Max-Age_ set to one year (for example), then, during that year, the **_initial value_ set in that
cookie** would be sent back to the server **every time** the user visited the server.

- **Secure Cookie** -


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
