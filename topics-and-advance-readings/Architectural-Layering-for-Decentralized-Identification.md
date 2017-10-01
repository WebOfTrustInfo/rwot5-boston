# Architectural Layering for Decentralized Identification
*A submission to Rebooting the Web of Trust \#5\
2017-09-30\
Drummond Reed, Co-Chair, DIF Identifiers, Names, and Discovery Working
Group*

Introduction
============

This document explains why, in building infrastructure for decentralized
identification, semantic identification should be layered over
decentralized identifiers (DIDs). It also proposes four key requirements
for this semantic identification layer.

The DID Layer
=============

DIDs (decentralized identifiers) solve a fundamental problem in digital
identity by providing a completely decentralized way to identify a
resource. Following is the abstract of the [*DID Data Model and Generic
Syntax
spec*](https://docs.google.com/document/d/1Z-9jX4PEWtyRFD5fEyyzEnWK_0ir0no1JJLuRu8O9Gs/edit?usp=sharing):

> **DIDs** (decentralized identifiers) are a new type of identifier
> intended for verifiable digital identity that is “self-sovereign”,
> i.e, fully under the control of the **identity owner** and not
> dependent on a centralized registry, identity provider, or certificate
> authority. DIDs resolve to **DID documents**—simple JSON documents
> that contain all the metadata needed to prove ownership and control of
> a DID. Specifically, a DID document contains a set of **key
> descriptions**— machine-readable descriptions of the identity owner’s
> public keys—and a set of **service endpoints**—resource pointers
> necessary to initiate trusted interactions with the identity owner.
> Each DID uses a specific **DID method**, defined in a separate **DID
> method specification**, to define how the DID is registered, resolved,
> updated, and revoked on a specific distributed ledger or network.

Section 1.3 of the specification explains the specific technical
motivations for DIDs:

> The growing need for decentralized identity has produced three
> specific requirements for a new type of URI that fits within the
> URI/URL/URN architecture, albeit in a less traditional way:

1.  **A URI that is persistent like a URN yet can be resolved or de-referenced to locate a resource like a URL.** In essence, a DID is a URI that serves both functions.

2.  **A URI that does not require a centralized authority to register, resolve, update, or revoke.** The overwhelming majority of URIs today are based on DNS names or IP addresses that depend on centralized authorities for registration and ultimate control. DIDs can be created and managed without any such authority.

3.  **A URI whose ownership and associated metadata, including public keys, can be cryptographically verified.** Control of DIDs and DID documents leverages the same public/private key cryptography as distributed ledgers.

The Semantic Identification Layer
=================================

While DIDs provide a machine-friendly layer of decentralized resource
identification similar to the IP layer of addressing on the Internet,
they do not solve the problem of human-friendly semantic identification,
i.e., how to map from the semantic identifiers that humans use to
identify a resource—which may change over time—to a machine-friendly
persistent DID. From section 1.4 of the DID spec:

> DIDs achieve global uniqueness without the need for a central
> registration authority. This comes, however, at the cost of human
> memorability. The algorithms capable of generating globally unique
> identifiers automatically produce random strings of characters that
> have no human meaning. This leads to the axiom about identifiers known
> as [*Zooko’s
> Triangle*](https://en.wikipedia.org/wiki/Zooko%27s_triangle):
> “human-meaningful, decentralized, secure—pick any two”.
>
> There are of course many use cases where it is desirable to discover a
> DID starting from a human-friendly identifier—a natural language name,
> a domain name, or a conventional address for a DID owner, such as a
> mobile telephone number, email address, Twitter handle, blog URL, etc.
> However, the problem of mapping human-friendly identifiers to DIDs
> (and doing so in a way that can be verified and trusted) is
> out-of-scope for this specification.
>
> Solutions to this problem (and there are many) should be defined in
> separate specifications that reference this specification. It is
> strongly recommended that such specifications carefully consider: (a)
> the numerous security attacks based on deceiving users about the true
> human-friendly identifier for a target entity, and (b) the privacy
> consequences of using human-friendly identifiers that are inherently
> correlatable, especially if they are globally unique.

Requirements of the Semantic Identification Layer
=================================================

Following are the key proposed requirements for the semantic
identification layer.

\#1: The Semantic Identification Layer MUST Map to a DID
--------------------------------------------------------

This requirement is paramount due to a fundamental security requirement:
the resource identified by an identifier MUST NOT change over time. The
OpenID community learned this lesson very painfully when it did not
realize that domain names in the URLs used as OpenID identifiers
permitted these URLs to be reassigned to new identity owners. For
example, the URL:

[*https://janedoe.com/*](https://janedoe.com/)

is controlled by the domain owner of “janedoe.com”. If this domain name
is reassigned, either directly or maliciously, then it represents a
different identity owner, which means all relying parties who have
granted access rights to the original identity owner are now vulnerable.

The OpenID authors subsequently changed the OpenID specification to
explicitly require OpenID providers to use non-reassignable URLs by
appending a unique fragment to the URL. However this solution was
acknowledged to be weak because the owner of the domain name for a URL
controls the fragment space, not the OpenID provider. The OpenID
community has never adequately solved what came to be known as the
“OpenID recycling problem”.

Furthermore, the OpenID recycling problem—or more generically the
identifier reassignment problem—is inherent at the semantic
identification layer because of [*semantic
drift*](https://en.wikipedia.org/wiki/Semantic_change). The human brain
is constantly remapping semantic identifiers and cannot be constrained
in the same way machine code can.

Therefore, to avoid reproducing the OpenID recycling problem and the
attendant security hole it introduces, any solution for semantic
identification of a resource MUST map to a DID for the resource. Only a
DID can offer the structural characteristics of non-reassignability
required of persistent identifiers. (Note that even a DID cannot prevent
reassignment of ownership by the identity owner via transference or
reassignment of the private keys. However DID architecture prevents that
reassignment from being outside of the control of the identity owner.)

\#2: The Semantic Identification Layer MUST Allow Many-to-One Mapping
---------------------------------------------------------------------

Another fact of human semantic identification is that humans assign
multiple identifiers to same resource. Even a single human being often
responds to many names—for example, an “Elizabeth” may also be
identified as “Liz”, “Beth”, “Lisa”, “Liza”, etc.

The same goes for organizational entities—for example a single
corporation may have multiple DBAs that “resolve” to the same unique
business identifier (or [*LEI—legal entity
identifier*](https://en.wikipedia.org/wiki/Legal_Entity_Identifier)).

So at the semantic identification layer it MUST be possible to assign
multiple semantic identifiers to the same DID.

\#3: The Semantic Identification Layer MUST Support Web Resource Mapping
------------------------------------------------------------------------

Web architecture inherently enables the mapping of arbitrary strings to
URIs. Typically those URIs are human-readable (or semi-human readable)
URLs. However that is often not the case. For example, the Google
doc where this paper was originally drafted has the following distinctly un-human-friendly URL:

**https://docs.google.com/document/d/12suJL5sX3CsNex\_mMhUW7A2mAmS50HjAaUUvq8O52-I/**

This is a classic example of using a machine-friendly identifier for
persistence. The semantic mapping necessary for a human to recognize the
document is provided by a link, e.g.:

[*Architectural Layering for Decentralized
Identification*](https://docs.google.com/document/d/12suJL5sX3CsNex_mMhUW7A2mAmS50HjAaUUvq8O52-I/)

At a minimum, this form of semantic mapping MUST also be supported for
DIDs. This requires either or both of two mechanisms:

1.  **DID Web proxy resolvers.** These are web servers that accept a URL containing a DID and return the DID document. Almost all new identifier formats require Web proxy resolvers—for example this is still the way most DOIs ([*digital object identifiers*](https://en.wikipedia.org/wiki/Digital_object_identifier)) are resolved today.

2.  **Native DID resolvers.** These are URI processors built into the browser or OS that handle DID resolution natively just as they currently handle DNS name resolution natively. Note that implementing a universal resolver for DIDs that supports all popular DID methods is a core focus of the [*Decentralized Identity Foundation*](http://identity.foundation/).

\#4: The Semantic Identification Layer SHOULD Support Market-Driven Mapping Solutions
-------------------------------------------------------------------------------------

While the traditional approach to semantic identification has been a
“name service”, the introduction of a layer for persistent,
cryptographically-verifiable decentralized identifiers enables a
semantic identification layer to be “liberated” from the traditional
constraints of a semantic name service. For example, a semantic
identification layer over DIDs could support:

1.  **Global names.** These would be the DID infrastructure equivalent of domain names.

2.  **Local names.** This “name service” is not globally unique, but locally-unique using P2P connections. See Christopher Allen’s [*Rebooting the Web of Trust*](http://www.weboftrust.info/) paper on [*linked local names*](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/linked-local-names.md).

3.  **Structured directory services.** These are services similar to LinkedIn or corporate LDAP services that permit queries by attributes.

4.  **Unstructured web search.** This is simply applying the same Web document spidering/indexing (and even PageRank-style reputation) to locating a link to the DID for the target entity. Note that verification of the actual ownership of the DID by this entity is out-of-scope for the DID specification but directly in scope for the [*W3C Verifiable Claims Working Group*](https://www.w3.org/2017/vc/charter.html).


