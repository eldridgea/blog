+++
author = "Eldridge Alexander"
date = 2017-10-10T02:00:00Z
description = "In the wake of the Equifax breach, a proposal for how the US can transition to a new Federal identification system with security as a main component."
draft = false
hero = "/img/proposal.jpg"
slug = "proposal-for-improving-social-security-numbers"
title = "Proposal For Improving Social Security Numbers"

+++

*Update: Added diagrams for an example*

If you're unfamiliar with asymmetric or public key cryptography, a good introduction without the math is [available here](https://blog.vrypan.net/2013/08/28/public-key-cryptography-for-non-geeks/).

In the wake of the [Equifax breach](https://krebsonsecurity.com/2017/09/the-equifax-breach-what-you-should-know/), there's increasing discussion about making changes to Social Security Numbers. Any changes will need to be discussed and will take a long time to implement, but the discussion is overdue. I doubt that there will be any perfect solutions for a while, but the discussion is important. As such I'm publishing some thoughts on what we might do to improve SSNs.

### Considerations

In thinking about security improvements to such a crucial system, some considerations present themselves. 

* SSNs must be extremely long-lasting, a system requiring an update even once a decade is untenable for an entire country.

* SSNs must support all citizens, even those in long term care, those who are homeless, and other situations.

* If a person loses any type of identifier card or hardware, there must be a way to reissue.

* Whatever transition happens must be seamless.

### Current Problems
 
Currently, Social Security Numbers (SSNs) are used effectively as both a username and password to "verify" your identity, occasionally with "security questions" which are often easily answered with public data. This is unacceptable — with an SSN effectively being both a username and password:

* Your password is shared across all services
* Your password can never be rotated
* Your password is [not random](https://www.ssa.gov/employer/stateweb.htm).

### Proposal

I propose a multi-layered identification system.

The core will be a public "key association" database maintained by the federal government. This will allow association of an SSN and cryptographic public keys. When an SSN is issued, a keypair is generated, with the private key placed on a paper card. The public key is associated with the SSN in the gov't database.

In addition to a paper key, citizens can enroll [U2F keys](https://fidoalliance.org/specifications/overview/) by signing onto a government site using the paper key and associate the U2F key with the SSN. (The sign in could be handled by local Javascript so that the private key isn't transmitted). The U2F public key will then be associated in the public database.

In the case of a citizen losing their private key, they could follow a process similar to obtaining a passport — go to a government office in person and present multiple forms of identification, at least one photographic, and the office could purge all associated public keys and reissue a Social Security card with a new private key. This process should be secured by requiring multiple officials to complete and be audited elsewhere.

### Usage

From this point forward, companies such as Equifax  could still collect and store data based on SSN. However, actions that require "pulling" of a full credit report or a similar action should require a U2F authentication where the user must sign into a portal for the bank and authorize the pull. This would be checked against the SSN and the U2F authentication would be checked against the government's public key database.

Example:

![Diagram 1](https://docs.google.com/drawings/d/e/2PACX-1vRU5G-KaxWaAsQhGNcAYwhZctMBHvRxtUblBB0hL2vRaJSNQYBmVGQcpJFrORC1WrRM7qdVAVO-Njai/pub?w=960&amp;h=720)


![Diagram 2](https://docs.google.com/drawings/d/e/2PACX-1vRlbPNKLojsCJC7YsTuwDdXPEROO2ac7uQU86wmbMu0MaCWjEHnCcYBoBOcIsI_ft938f654xC3hMYB/pub?w=960&amp;h=720)



![Diagram 3](https://docs.google.com/drawings/d/e/2PACX-1vSJiClP0AQgegTnmWcLc4pr5QiBX4ptMvCSoaw8cJuAd9Xee50DnJJquu7oBpng8YObXP_HLP6xKSI5/pub?w=960&amp;h=720)



### Transition

From the beginning the government will have to make it illegal to ask for private keys. Any private keys found will trigger a key revocation and reissue.

To make the transition happen successfully would require it to be as seamless as possible for citizens, and as mandatory as possible for financial institutions.

Private keys could be issued in phases over several years, to volunteers at first, and then perhaps synced with tax filings, drivers licenses renewals, or passport requests. Once all SSNs have an associated public key, the phase in can begin for financial institutions.

As we are seeing with the credit card chip rollout, this will be slow, but the government could provide a long but mandated timeline, with a shorter timeline applied as punishment to companies such as Equifax that are negligent in their protections of consumer data.

`Photo Credit: http://www.kiplinger.com/quiz/retirement/T051-S001-how-well-do-you-know-social-security/heros/intro.jpg`