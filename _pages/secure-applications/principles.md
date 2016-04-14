---
permalink: /secure-applications/principles/
title: Secure Development Principles
---

[xxx intro xxx]

## KISS

- "Keep It Simple, Stupid" (link to background so peple get the joke)
- simple is better than complex: easier to test, easier to read, easier to understand

“Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.”
— Brian Kernighan

## DRY

- "Don't Repeat Yourself" - common in software development
- as it applies to security:
    - smaller attack surface
    - keep security stuff in one place --> bugs only have to be fixed once
    - re-use existing components - economy of scale
- "Linus's Law"
    - "given enough eyeballs, all bugs are shallow"
    - all software has bugs; free software's bugs get found sooner
    - this, combined with above, means you should have a strong preference towards re-using existing open source software (this is true everywhere, but especially when it comes to security)
    - some people take the vulnerabilities in e.g. openssl as signs that floss is less secure. Not true. You don't hear about the vulnerabilities in closed source software; did they get fixed? Who knows. Both kinds of software have vulnerabilities, you hear about the free stuff because it gets fixed.  

## Least Privilege

- also an operational principle, see that guide
- in code, means checking for the most specific permission possible
    - and by exntesion means granular is better than corse
    - e.g. `if user.has_permission('edit post')` is better than `if user.is_superuser`.

## Defense in Depth

- multiple layers of security
- don't assume the layer above checked - never hurts to check again
- always log sensitive actions (see logging guide)

## Fail Safe

- bugs should cause systems to fail closed, not open
- example: Django's request.is_secure can't always tell if a connection is secure. If it's not sure, it says "no". Be wrong in that direction, not the other
- when in doubt, crash!
