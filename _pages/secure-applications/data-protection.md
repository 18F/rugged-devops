---
permalink: /secure-applications/data-protection/
title: Data Protection
---

[FIXME: this document might fit better in more of an operational context, since it doesn't really deal with appsec that much. If/when we have some sort of opsec area we should think about moving this there]

# Private data is a liability, not an asset

In the age of Google and Facebook, we sometimes intuitively think of private data as an asset. After all, those kinds of companies would never exist without the massive amounts of data they've collected. But when we think like a security engineer, it's clear that this data is a liability. Attackers aren't breaking into systems for fun any more; they're after sensitive data. [TODO: say more here, success because they're able to protect this data well.]

*[Note that in this document we use extremely broad terms like "sensitive data" to deliberately. While there are more precise, domain-specific terms like "PII", "PHI", "CHD", and the like, our intension here is to focus on the principles underpinning safe handling of sensitive data, reguardless of its legal or regulatory status. Thus, we deliberately choose to define "sensitive" as broadly as possible.]*

## Collecting sensitive data

When you think about sensitive data as a liability, it should change your approach to data collection. When faced with building an app to collect sensitive data, try to monimize your liability. Ordered from best to worst, here are some approaches you should take:

1. **Don't collect it!** Any time you capture any private data, ask whether you *really* need to collect it at all. If there isn't a direct business need to gather someone's private information -- *don't*. 

2. **Collect it, but discard it immediately.** In some situations, you may be able to collect the data, use it immediately, and then drop or delete the data you've collected. For example, if you were building an app to generate images of business cards, you'd need the person's information to print on the card. But, if you only needed to generate an image to serve back to them, you could generate the image and simply not store information anywhere. Boom: the user gets the image they wanted, and you minimize your liability.

3. **Collect it, but discard it quickly.** (And, probably, store it carefully as below.) In other situations, you may need the information for future use, but possibly not indefinately. In these situations, you should delete the data as soon as you no longer need it. To extend the previous example: if you needed to *print and ship* business cards, you'd obviously need the person's billing information, shipping address, etc. However, once you've shipped the cards (and confirmed delivery), do you really need to store that information? Why not delete that data, and limit your liability, now that the order's complete?

4. **Collect it, but store it safely.** This is your final option: do collect the data, and do store it, but do so carefully. The rest of this document attempts to more accurately define what "careful" means.

## Store sensitive data only in well-protected systems

## Don't download sensitive data

## Don't trust third parties

