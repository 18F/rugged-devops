---
permalink: /secure-applications/cryptography-101/
title: Cryptography 101
---

# Math is hard

Cryptography is amazing. Done right, it's our strongest tool against determined adverseries; proper cryptography can defeat even the most resourceful attackers. However, getting crytopgrahy right is devilishly complex. Crypto engineering is unlike most other forms of engineering: most other kinds of bugs might cause a crash or two, but crypto bugs *break the intended security completely*. Incorrect crypto is as bad as no crypto at all — or sometimes even worse (the Heartbleed vulnerability didn't just break TLS; it also allowed arbitrary disclosure of server memory!). Even experts get it wrong — not just sometimes, but often. The only way that cryptography becomes bulltetproof is through extensive, large-scale peer-review - the kind of review that only happens to free standards and open source software.

This leads directly to The Three Laws of Cyprotography Implementation:

1. Don't implement your own cryptography.
2. No, really: **don't implement your own cryptography!**
3. Instead, use an established, peer-reviewed open source library (like the ones linked in the following sections).

This can sound scary - and, compared to much of the rest of this guide, it is. Failure here can be pretty catestrophic. Still, like most basic security engineering, if you follow some simple rules you'll be okay. The rest of this guide lays out a bunch of situations where you'll need cryptography and explains what the "right answers" are in each situation.

By the way: all of these situations are good candidates for the buddy system. Weather you practice pair programming religiously or not at all, when faced with one of the situations described below it'd be a great idea to get someone else to work on the problem with you. Two minds are *always* better than one!

# Cryptography "right answers"

For the impatiant, here's the cheat sheet:

Are you...

* ... encrypting data in transit (e.g. between machines)? [Use TLS](#data-in-transit).
* ... generating random keys/secrets? [Use urandom](#random).
* ... storing passwords? [Use bcrypt](#passwords).
* ... signing messages? [Use HMAC-SHA256](#signing).
* ... encrypting data to be shared with a trusted source? [Use Fernet](#symmetric-encryption).
* ... doing anything else? **Ask an expert for help!**

<a id="data-in-transit"></a>
## Data in transit: Use TLS.

- tls is specifically designed for this use case; anything else is not as good.
- usually this means an existing protocol - https, databases-with-encryption, etc
- tls with other protocols is probably a bad idea, stunnel can help here
- most languages: built in
- see TLS guide for some more details (cert validation)

<a id="random"></a>
## Generating random keys or secrets? Use urandom.

- psudorandomness vs real random
- it's fine to use real random all the time if you want!

<a id="passwords">
## Storing passwords? Use bcrypt

- bcrypt, 10 rounds
- crypto agility
- reasonable people can disgree, so if you must, other acceptable answers are argon2, scrypt, pdkdf2 - but if someone wants you to do anything else, resist
- don't store any metadata (length, strength, etc etc - http://gavinmiller.io/2016/a-tale-of-security-gone-wrong/)

<a id="signing"></a>
## Signing messages? Use HMAC-SHA256

- what's signing?
- HMAC-SHA256

<a id="symmetric-encryption"></a>
## Symmetric encryption? Use Fernet

- sym enc use cases
- I thought you said "use tls?"
- using fernet

## Doing anything else? Ask an expert!

If you're doing anything not covered by this guide, you're travelling beyond Cryptography 101 territory. This means it's time to reach out to security experts in your organization. If you don't *have* those kinds of experts, you should be thinking very carefully about whether to proceed at all!

# Further reading

- https://www.crypto101.io/