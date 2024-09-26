---
author: "Eldridge Alexander"
date: 2020-07-14T12:03:11Z
excerpt: "Discussions of Signal's new SVR feature should consider not only the Signal app, but the Signal ecosystem as well."
draft: false
hero: "/cdn-cgi/image/format=auto/img/signal.jpg"
slug: "discussions-of-signal-svr-should-consider-network-effects"
title: "Discussions of Signal SVR Should Consider Network Effects "
authors:
  - Eldridge Alexander
---

There is currently a lot of discussion around Signal’s new [PIN](https://signal.org/blog/signal-pins/) decisions. In particular, the discussions have focused on the decision to use the PIN as a seed to encrypt backup data that will be stored on Signal servers using Secure Value Recovery (SVR). So user data will be stored in a way so that even Signal cannot access it. SVR uses [Intel SGX](https://en.wikipedia.org/wiki/Software_Guard_Extensions) to ensure this.

This week there was [an excellent post](https://blog.cryptographyengineering.com/2020/07/10/a-few-thoughts-about-signals-secure-value-recovery/) by [Matthew Green](https://twitter.com/matthew_d_green), a cryptographer and professor at Johns Hopkins University, where he discussed some of the concerns he has with Signal’s SVR system, especially around SGX. He also touched on the rollout methods and delivery Signal has used to communicate this new feature. It’s an excellent breakdown and I can’t effectively summarize it here, I highly recommend reading it.

(To *ineffectively* summarize it however, SGX isn’t foolproof and has had issues in the past. Signal is pushing this hard on users without a lot of context or easily understood options for disabling SVR.)

Matthew’s criticisms are all valid and I don’t disagree at all. But I want to add something to the discussion that is being mostly omitted -- the network effect of a messaging app, and the considerations Moxie and Signal have to take into consideration to effectively secure your and my communications.

Signal must take into account multiple users accessing identical data as a first-class concern. Every communication you have on Signal must be decrypted by an endpoint you don’t control -- the device of the person you’re messaging. A similar use case is email. Hypothetically, let’s say you avoid Google like the plague. Even then, approximately 50% of your email will still reside on Google servers due to your recipients using either Gmail or G Suite.

As Signal is a closed(ish) ecosystem, unlike email, they have to deal with this concern too. Not only do they have to make sure that the security on your endpoint is as strong as possible, but they also have to make sure the same is true of the other endpoints where you’re sending data.

In this situation Signal has to consider that doing what many suggest and making SVR as an opt-in, or not offering at all will likely *reduce* adoption by a broader userbase, who want things like contact syncing, and easy backups. So while adding user choice may make *my* data storage more secure, the fact that it hurts adoption means a smaller percentage of my communications will be end-to-end encrypted at all because they’ll go over channels like Slack, email, or SMS.

It is worth keeping in mind that Signal is maintaining not only an application, but an ecosystem, and the security considerations must take both areas into account. It is better, in my mind, to have a goal of really good security on the majority of my communications, as opposed to exceptional security on just some of my communications. And Signal has always been a secure messaging player in the consumer and non-expert space, as opposed to something like Keybase which targets more knowledgeable users and makes different tradeoffs accordingly.

As Matt says in his post, criticizing Signal is difficult as their overall work is great, and I'm glad the criticism and discussion are happening. We should continue to hold them to a high standard. But the network effects and ecosystem should be considered as much as the application and security architecture. If they aren’t then we risk repeating the mistakes of PGP email where we have an amazingly secure system that is rarely used in practice.