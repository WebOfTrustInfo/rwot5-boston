# Sixteen Lightning Talks

## Identity Mental Models

Three types of mental models for identity:

   1 _Security._ Reduce your identity to your physical body. (TSA, Law Enforcement.) = Singularity
   2 _Freedom._ Identity is how you express yourself, not tied to physicality. (Digital Libertarians.) = Multiplicity
   3 _Data._ Attributes are identity. (Engineers.) = Specificity
   
People talk past each because they think they have a common language, and they _don't_.

The gaps between these three models are what we argue about.

Am I missing one?

## Language & Liability
### re: Self Sovereign Identity

#### The Language

We don't have a good language to talk about self-sovereign identity.

Those of who talk about it here are a little revolutionary and rebellious, and other people might think it sounds "cultish", and the UN and government may not like it either. But it's all about _vocabulary_!

So how do we develop a vocabulary thats friendly to every one?

We have to build a system for users, but regulators and industry partners have to accept it.

#### The Liability

What are the unintended consequence of self-sovereign identity?

Are we shifting the liability for data to the user?

We know how to go after Equifax when they mess up.

Are we really going to accept liability for ourselves when we lose our keys?

Are we increasing liability for other people with this?

## Reconciling Privacy & Security with Usability & Convenience in Distributed Systems

There are trade-offs!

Usability vs security
Privacy vs convenience

We need to identify these, so that they can be balanced.

Discussion of needing to bake security into system rather than depending on user to make decisions.

How can you build modular systems that incorporate new systems while simultaneously letting laggards in.

## Too Much Info
### Is the First Amendment Dead?

Based on an article.

It argues that First Amendment only became issue with WWI and US propaganda. It then goes on to say it's not free speech which is issue, because anyone can speak through blog. So free listening is the new problem, to minimize the noise.

This links to issue like China drowning out problems, Reputation.com doing the same, arguments over Fake News.

So should we _limit rights of government to drown out signal!?_

Should there be regulation?

## Non Correlatable Individual Data Storage

How do you make your verifiable claims from your self-sovereign identity without them being correlated over time?

Identifiers resolve to an identity! That is correlation!

Where do you find the balance?

Perhaps if you could distribute methods that prove verifiable claim without actually giving verifiable claim? A zero-knowledge proof?

Perhaps you could offer misinformation to increase the noise!

Perhaps you could use that misinformation as active measures that would identify people misusing the reinformation.

## BOPS

Biometrics is really coming to the forefront, independent of old hardware.

BOPS is IEEE 2410.

Collection, storage, processing, transmission

BOPS talks about where you store (mobile or server) and where the match occurs, and covers all the options.

Here's the big concern:
This should _not be your identifier_, just one point toward that.

## Impact Claims

A whole category of claims that are about a subject rather than an entity. 

Such as claim that "I have immunized a child". 

You are evaluating the _content_ of a claim, where most claims are just evaluated based on who is making the claim and whether they're trusted!

## Beyond Incompetence
### Sabotage of Standards & Examples

Groups see various different problems and want to solve them.
But somewhere along the line something goes wrong.

Solve some problems, but create new ones!

These are _unintended consequences_.

So we're now dealing with legacy problems like certificate authorities.

EXAMPLE: Dual-ECC
Where the NSA generated keys that gave them a backdoor into cryptography standard.

EXAMPLE: Intel Backdoor
God mode in Intel ME (Management Engine) that gives full control and access to your computer
And may have been broken. Also, AMD PSP. 

_So for this group, whenever says they're going to make the world a better place, there's probably a downside that you're not seeing. KEEP AN EYE OUT FOR IT. Don't surpress criticism!_

## Who Pays?
### How Does the average user use?

If you're going to be having decentralized things, you want them highly replicatable and available, and you need economic incentives to make this happen.

So who pays??

The questions of constraints and costs don't come up very often.

## Social Key Recovery

A humancentric to a technical problem: I have a thing that's valuable and I need to store it and have it not be compromised.

   1 Shard a key and distribute it among people in my network. 
   2 Or: a friend must approve large-scale transfer of tokens.

The latter example of _social elevation_ is a powerful idea.

Unfortunately, examples have suggested that shard lossage is much higher than expected.

Notaries are an example of existing social verification of this sort.

## Verifiable Claims for Energy Distribution, Telecom, etc.

Use verifiable claims to source your source of electricity.

Solar energy, wind energy, traditional means energy.

It would help encourage more available energy sources.

And customers could choose what they're willing to pay. 

Could similarly source telecomm, based on price, how good they are.

An exciting example is _GreenCerts_, and it would be great to use verifiable claims with them.

## Offline Solutions

Puerto Rico has lots of power, cell, and water down. 

This was a large storm, and people were _surprised_.

Where was the backup?

This got people thinking about what systems require you to be online?

_Disasters are not only risks, also political problems? How can we mitigate?_

Three ideas to consider

   1 Verifiable claims require a nonce to be signed, which requires an online connection; we want to be able to identify when something uses a connection, and when you want to be able to make a claim without network
   2 Apps would be a great way to solve this, but they'd have to be apps that everyone wants.
   3 It's a new set of adversarial condition where someone has more info than you because they're online and you're not
   
## Compatibility / Interoperability Between Systems

All sorts of signatures and IDs need compatibility and interoperability, but they don't work together well!

Examples:

1. **Verifiabile Claims & SOLID.** May not get claim out of RDF structure in the same form as you put it in. Also, you can't store multiple claims in same RDF.

2. **DIDs & WebIDs.** They both identify and they both have associated public keys, but they don't work in the same way. 

3. **DIDs & Other Data Stores.** Authorizing a device and friends to access data store and giving someone permission to update DID all require different interfaces. Why!?

Could there be more harmonization?

## Building a Decentralized Game

Converting the web into an open metaverse!

What do we need?

   1 3D & XR support for the web
   2 Decentralized file system
   3 Identity system
   
Why is this important?

   1 Privacy
   2 Lots of heavy file servings
   3 Identity
   
We're sharing a lot of information, and we need to be careful about what we share. Needs to be good inventory systems to link with identities. Finally, we need whole metaverse to be seemless, with consistent identities.

## Web of Trust Now
 
Early PGP adopter, but only signed a few important message. Still, it's important for signing GitHub.
 
Doesn't like PGP!
 
So, is there a way to anonymously get info on who is seeing commits for code that we're thinking about now?
 
Is there a way to start simple stuff now?
 
Don't worry about perfection now.
 
## Social Web & RWOT
  
Today, we have the least self-sovereign possile.
  
Now, we can do ActivityPub. Mastodon has adopted. They have different nodes, so you can have separate nodes. And Mastodon is adopting other elements like signatures.
  
So how do we get to actual self-sovereign, where we're a full network? Subscribe to each other on social networks and use that for PGP signing!  But what we really want is DIDs. Because then even if Mastodon nodes go down, we still have links. 

We can _incrementally_ move through networks like this without just throwing away what we have.

Mastodon is a use case happy to adopt ourselves as soon as we have it in a good-enough state!


