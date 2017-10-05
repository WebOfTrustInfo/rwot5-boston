# A Primer on Self-Sovereign Identity

#### By Christopher Allen & Shannon Appelcline

Joe Andrieu's [Primer on Functional Identity](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/functional-identity-primer.md) offers a descriptive definition of identity. Quite simply, Andrieu says, "Identity is how we keep track of people and things and, in turn, how they keep track of us." It's an astute description that cuts through the confusion of what an identity database should or shouldn't encompass by instead suggesting that models need only include what's required for persistent identification.

However, the content design of an identity system is only half the battle. There are also questions of jurisdiction, management, and oversight. In other words, once you have an identity system, who runs it, and who are they beholden to? That's where _self-sovereign identity_ enters the picture, as an orthogonal way to look at the question of identity systems.

## A Self-Sovereign Definition

> Self-sovereign identity is centered on a person, free from dependence on any corporation, organization, or nation-state.

This core definition of self-sovereign identity is a simple one, affirming that identity belongs to an individual person and cannot be taken from them. 

However, that flies in the face of how identity systems are administered in the modern world. The constraints that currently exist don't match the _natural_ definition of identity, which says that we are ourselves. They don't match the _functional_ definition of identity, which says we are who we're known to be. They instead make us identity serfs, bound to the custodians of our crucial identity records. With social security cards, passports, and driver licenses, the US and state governments control our fundamental rights of existence. Other governments act similarly. 

In recent years, there has been some hope of emancipation. UN Sustainable Development Goal 16.9 requires that "By 2030, [we] provide legal identity for all, including birth registration". It's not the first time the UN has spoken out for human identity rights. The question is: can we leverage that support into the creation of truly _self-sovereign_ identities?

The danger is that we instead repeat past mistakes; that's unfortunately what we've seen so far on the next frontier of identity, the internet. There, internet corporations like Facebook constrain our ability to project our identity online; they can terminate our ability to interact with our identity circles at a moment's notice and may even be able to deauthenticate our access to linked remote sites. Like nation-states, these internet corporations are dangerously centralized, creating a single point of failure for digital identities. 

And so the future echoes the past, with corporations taking over the centralized roles of nation-states, and the losers are still the people themselves. Even with an understanding of the problems of state-sovereign identity, even with the support of the UN, we have not yet had the ability to change. It demonstrates why we need to radically rethink our concepts of identity, to redefine them, so that we don't end up right back where we started. And we need to do so quickly, because the internet's ideas of identity are coalescing _now_.

## Ten Principles

[The Path to Self-Sovereign Identity](https://www.coindesk.com/path-self-sovereign-identity/) was first detailed in April, 2016. Since, the concept has received widespread adoption. However, it's at an early stage of development. Though we know the fundamentals of what a self-sovereign identity aspires to be, we're still discussing the specifics of how to get there.

The original article on self-sovereign identity included a list of ten self-sovereign principles. They were intended as a starting point for discussion. Some may indeed by critical, but others may be extraneous complications that should be pruned away.

In brief, these ten potential principles are:

      1. **Existence.** Users must have an independent existence. 
      2. **Control.** Users must control their identities. 
      3. **Access.** Users must have access to their own data.
      4. **Transparency.** Systems and algorithms must be transparent.
      5. **Persistence.** Identities must be long-lived.
      6. **Portability.** Information and services about identity must be transportable.
      7. **Interoperability.** Identities should be as widely usable as possible.
      8. **Consent.** Users must agree to the use of their identity. 
      9. **Minimalization.** Disclosure of claims must be minimized. 
      10. **Protection.** The rights of users must be protected.

Further discussion of these principles is available in [the original article](https://www.coindesk.com/path-self-sovereign-identity/). More recently, Natalie Smolenski wrote about the specific issues of "control" in [Owned vs. Unowned Claims and Self-Sovereign Identity](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/owned-vs-unowned-claims-and-ssi.md).

## Self-Sovereign Identity Systems

These definitions and principles describe the philosophy of self-sovereign identity, and they also lay out the technical requirements needed to build such systems. The first three principles are the most important bases of a technical implementation: when we say that users must have existence, and that they must have access and control over their identity, we imagine an identity system where the user is king. He is his identity's root and its executor. 

Put that together with the sixth principle, on portability, and you have an identity system that creates an identity as a discrete unit, with specific access, and with the ability to package it up and bring it to a different identity service. Thus, identity is no longer locked to an organization, a corporation, or a nation-state; instead it resides with the user, who can temporarily home it where he sees fit.

Any self-sovereign identity needs to begin with a trusted root, and that's the focus of the first major implementation of self-sovereign identity: the decentralized identity, or DID, which is now a [W3C draft](https://w3c-ccg.github.io/did-spec/). The [DID Primer](did-primer.md) contains extensive information on DIDs and other related specifications; in short, DIDs provide a methodology for proving control over a key, which can be used to prove identity. Blockchains are the basis of many DID methodologies. 

Self-sovereign identity also require that these free-floating entities be able to make claims about each other; it's how people "keep track of each other", the basis of functional identity. This is the heart of another major project related to self-sovereign identity, the Verifiable Claims initiative, which includes a [W3C working group](https://www.w3.org/2017/vc/WG/). Manu Sporny has written about it in [A Primer on Verifiable Claims](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/verifiable-claims-primer.md).

Doubtless, there will be other technical solutions for self-sovereign identity in the future, as the philosophy behind these identities is still evolving.