---
permalink: /secure-applications/preventing-xss/
title: Preventing Cross-Site Scripting 
---

*Cross-site Scripting* (XSS) attacks are a type of injection attack, where malicious scripts are inserted into your web site. 

For example, imagine a site like Twitter where users can enter messages, which are then displayed to the world. If an attacker entered a message like `<script>alert("hi!")</script>`, and that message wasn't escaped, then the script would execute any time someone visited the page. Alerts are harmless, but XSS attacks can do far more malicious things: steal cookies, break session tokens, and even re-write the content of the HTML page.

XSS comes in several "flavors":

* *Stored XSS* (also sometimes called *Persistant XSS*) are attacks where the injected script is permanently stored on the server (e.g. in a database). The malicious script is served whenever someone hits a page where that value is rendered unescapted. Stored XSS attacks are generally the highest risk, since they can persist indefinately.

* *Reflected XSS* occurs where the injected script is "reflected" from user input, such is from an error page, or search query, etc. Reflected attacks are harder to deliver to victims since they'll show up in the URL of shared links, require tricking a victim into posting a form, or othewise require extra steps than just getting a user to visit a page. 

* *Self-XSS* occurs when user-supplied data is only reflected back to the user who entered it. Self-XSS are generally lowest risk (since they can only hurt the user executing them), but should be fixed as they often indicate the potential for a worse issue later on.

## Preventing XSS

There are several techniques you can use to protect against XSS:

* Option 1 (preferred): Use a templating engine that protects against XSS
* Option 2 (acceptable): Sanitize user-supplied content with a library designed for the job
* Option 3 (last resort): Escape output

You should also look into [implementing a Content Security Policy](content-
security-policy.md); CSP, in concert with one of the above techniques, makes for
incredibly effective XSS prevention.

Read on for details!

### Preventing XSS using a template engine

These days, it's rare to generate HTML without the use of a template engine. And, most modern template engines will automatically escape provided data, thus easily protecting you from XSS attacks.

Some examples of libraries that have built-in XSS protections are:

* [Mustache](https://mustache.github.io/) (multiple languages)
* Django's templates (Python)
* Rails ERB (Ruby)
* Jinja 2 (Python)

Generally, libraries provide utilities for turning off XSS protection, for example in Django:

```python
{{ some_variable|safe }}
```

Or Rails:

```erb
<%= some_variable safe %>
<%= raw some_variable %>
<%= content_tag some_variable %>
```

Use these methods with great care! If the content in question might contain data that could have been user-supplied, these methods might be introducing an XSS hole. If you must present unescaped, user-provided data, you should sanitize it first (see below for details).

And of course, you should consult the documentation for your chosen library to see if there are any other caveats to be aware of.

### Preventing XSS with a santization library

### Preventing XSS by escaping output

## Further reading

* [OWASP: Cross-site Scripting](https://www.owasp.org/index.php/XSS)
* [OWASP: XSS Prevention Cheat Sheet](https://www.owasp.org/index.php/XSS_%28Cross_Site_Scripting%29_Prevention_Cheat_Sheet)

