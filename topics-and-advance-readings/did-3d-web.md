# DID for the 3D Web

By Alberto Elias

## Introduction

Virtual Personas are a P2P Web and blockchain based [DID](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/did-implementer-draft-10.pdf) identity system. It’s an identity system thought out to fulfill all needs on the decentralized 3D Web, that requires a single global identity for all sites to make the experience seamless. The user experience to have a different avatar and profile for each site would be subpar.

The DID is a content address that points to a DDO that is hosted as an RDF file in a decentralized file system such as [IPFS](ipfs.io), [DAT](https://datproject.org/) or [Swarm](https://github.com/ethersphere/swarm). The DDO can hold certificates that prove the information stated within it, but also the ownership of blockchain addresses.

Both IPFS and Dat, when creating a new decentralized directory, they create a private key, and only the owner of said key can update the content. To properly tie the Web identity with the blockchain identity, I’m looking into using the same private key that holds the DDO for a blockchain public address. Currently, they might use different signature systems, but there might be a way to derive one from the other. Looking forward, it’d be interesting to look deeper into this idea of having just one key pair to control every aspect of an identity, and the public key acting as both the DID and the public address on the blockchain.

Blockchains can bring in value as they allow identities to easily handle payments in different cryptocurrencies, hold virtual property or interact in new token based protocols. They are not efficient enough to have an identity system that’s solely blockchain based, and they’re not Web compliant, but this identity system can work off-chain, and do all necessary transactions on-chain easily. Also, many of their shortcomings are being worked on, like what the [Ethereum project](https://ethereum.org) is doing with the transition to [Proof of Stake](https://github.com/ethereum/casper) or [Plasma](http://plasma.io/).

Currently, DIDs would be public keys which are very hard to remember. DNS is a centralized system, but both IPFS and Dat are working to make their decentralized protocols work better with DNS. This could be a temporary option while decentralized naming systems like [Blockstack](https://blockstack.org) and [ENS](https://ens.domains/) are further developed.

## DDO Format

It should be in an [RDF](https://www.w3.org/RDF/) compatible format like [JSON-LD](https://www.w3.org/TR/json-ld) or [Turtle](https://www.w3.org/TR/turtle/). The base format is suggested in the [DID spec](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/did-implementer-draft-10.pdf). On top of that, I’d like to suggest some additions.

I believe the [SOLID project](https://solid.mit.edu/) has many interesting ideas about designing a Web compliant identity system. It has some equivalences with the DID spec like a [WebID](https://www.w3.org/2005/Incubator/webid/spec/) being a DID, and a WebID profile being a DDO. The DDO would be a multi file object, each file holding different pieces of information and with different access control policies. An identity could decide to share all her information just to herself, most of it just with friends and maybe just her job title to unknown identities.

[Verifiable Claims](https://www.w3.org/2017/vc/charter.html) would also work just fine with this proposal, which will allow entities to prove facts about their identities by providing a proof from a 3rd party (like a government issued ID), without having to reveal information that wasn’t solicited.

For the 3D Web, some other properties are needed in the DDO. A clear example would be a [GLTF](https://github.com/KhronosGroup/glTF) formatted avatar, so the identity can have a single avatar for all sites. At some point, we’ll have virtual objects that can be possesed by identities. There are several blockchain projects like [Mediachain](http://www.mediachain.io/) to handle property which can be held and transferred by an identity.

## Web APIs

There are many existing specs, and others that are being worked on that can make this possible. For starters, [DID](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/did-implementer-draft-10.pdf)s and [WebID](https://www.w3.org/2005/Incubator/webid/spec/)s have specs, and the [Verifiable Claims Working Group](https://www.w3.org/2017/vc/charter.html) are doing great work on that front.

Authentication is another important element. We have the [Credential Management API](https://w3c.github.io/webappsec-credential-management/), though it only supports passwords and federated logins. It is compatible with creating custom credentials, so a new key-pair system could be implemented. A site could check that it’s the owner of a DID by sending a message encrypted with the DID’s public key, the owner decrypts it with their private key, and sends it back encrypted with the sites public key.

From there, we would need to start working on a browser API for identity management. This would provide features such as soliciting permissions to read specific information fields and handling social aspects like adding friends, following another identity or adding new information. The team from [Beaker Browser](https://beakerbrowser.com), a Dat based browser, are building a [social API](https://github.com/beakerbrowser/beaker-profiles-api) based on Dat archives.

## Framework

[This paper](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/Framework-for-Comparison-of-Identity-Systems.md) by Kyle Den Hartog sets a framework for identity systems to compare them with each other. Below I explain how Virtual Personas apply to this framework. There are four categories with different subcategories ranked as *High, *Medium* and *Low*.  

### **Verifiability**

* **Trusted source:** *High*. It is provable that the DID is associated to a DDO, and that the DDO is owned by a public key. That DDO can only be modified by the entity that owns the corresponding private key. There can be Verifiable Claims in the DDO that can prove information about the identity, but these come from third party trusted sources such as government agencies.

* **Verification method:** *High*. A DDO has an owner associated with it, and only the entity that has the private key corresponding to the public key in the DDO can be verified as said owner.

### **System Architecture**

* **Organizational structures:** *High.* DIDs can have multiple owners.

* **Centralization:** *High.* Completely decentralized system since DDOs are hosted on the network, and anyone can host them. DIDs are just the address to that content wherever it may be in the network.

### Accessibility

* **Independence:** *High.* Everything will be completely open source and is based on open standards. Elements that aren’t standards yet will be proposed as such.

* **Devices:** *Medium.* Entity needs a device (phone, laptop, hardware key..) to hold the private key.

* **Deployability:** *Medium.* Virtual Personas are based on current standards and new ones that can be implemented as tools, like libraries, while they’re developed.

* **Portability:** *Medium.* You do need to carry a device with the private key to use the identity in both physical and digital environments.

* **Identity removal:** *Low.* An entity owner could stop hosting a DDO, but there could be others hosting it, specially if it’s a public person. Blockchain addresses can’t be deleted, nor the transactions linked to it, but it’s usage with its assigned identity can be blocked. Also, entities control which pieces of information they decide to share, and at any time they could decide to share less.

### Security

* **Integrity:** *High.* DDOs can only be modified by those holding the private key to that content. Also, protocols like DAT keep a history of changes.

* **Confidentiality:** *High.* Only entities with the allowed private keys can read/write information related to an identity that explicitly gives them the necessary permissions.

* **Theft prevention:** *Medium.* Devices holding a private key can be compromised, though systems can be in place to revoke a private key and swap it for a new one. 

* **Data revocation:** *Medium.* At any time, an entity could reemove any data they want except for transactions made with other entities as they could still hold a public log of transactions. Also, some protocols keep a history of changes, so they wouldn't be deleted from there. With proper access control policies, access to the information can be revoked. Non-anonymous transactions made on a public blockchain also can’t be hidden.

* **Anonymity:** *High.* DDOs don’t need to hold critical pieces of information about an entity. They can be empty even. Also, they can contain private information.

I believe this to be a good compromise on the different categories, with identity removal being the main issue. It’d be great to work more on finding a way around current issues.
