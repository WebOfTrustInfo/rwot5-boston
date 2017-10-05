DID Method Spec Template Definition

2017-10-05

*A paper from the DID Specification working group at Rebooting the Web of Trust #5, Boston, MA, USA.*

# Introduction

This paper represents the consensus of the authors of several DID method specifications about the recommended template for a DID method specification. For background on DIDs (Decentralized Identifiers) and DID methods, please see the [DID Primer](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md).

Our i document will be contributed to the W3C Credentials Community Group in order to be turned into a template specification document published in ReSpec format.

# ReSpec

It is RECOMMENDED to use the [ReSpec](https://github.com/w3c/respec/wiki) format for a DID method specification. The authors of this paper intend to create the template defined in this paper in the ReSpec format and contribute that template to the W3C Credentials Community Group.

# Notation

In the following template, plain text and headers should appear in every method spec. Variables are denoted in [square brackets]. Explanatory comments are highlighted in <em>italics</em>. Examples of section content content appear in [[[ three square brackets ]]].

...................Template begins immediately below this line.........................

# <em>[Name]</em> DID Method Specification V<em>[x]</em>

# <em>[Author], [Affiliation]</em>

# Preface

This is a DID method specification that conforms to the requirements specified in the [DID specification](https://w3c-ccg.github.io/did-spec/) currently published by the W3C Credentials Community Group. For more information about DIDs and DID method specifications, please see the [DID Primer](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md).

# Abstract

<em>(recommended)</em>

[[[ The Bitcoin Reference (btcr) method for managing DIDs on Bitcoin is formally specified. ]]]

# Introduction (Informative)

[[[ Managing DIDs on Bitcoin requires transactions with these characteristics: … Once a transaction has been submitted … Details follow. ]]]

# Examples (Informative)

<em>(examples of DID documents or other artifacts used by this method; prefer short ones)</em>

# Target System(s)

<em>(Describe the system or systems which are the target of this DID method. The target system may be any DLT or other distributed network or other system capable of supporting the CRUD operations. This section should also specify any constraints it assumes or imposes on the target system.)</em>

[[[ This targets Bitcoin consensus rules exactly equal to the ones in binary X with hash Y. (Any time the binary changes, the spec will have to be updated accordingly, to clarify how it relates to forks and other evolution.) ]]]

# DID Method Name

The namestring that shall identify this DID method is:

	[[[ btcr ]]]

A DID that uses this method MUST begin with the following prefix:

	[[[ did:btcr ]]]

Per the DID specification, this string MUST be in lowercase.

# DID Method Namespace Specific Identifier (NSI)

<em>(This section describes how DIDs in this method are formatted, parsed, and generated. For example, are they sequences of 31 digits, or 24 alphanumerics? How is uniqueness guaranteed? Etc.</em>

## Namestring Generation Method

<em>(definition of how the NSI is generated under this method) </em>

## ABNF Definition

<em>(section contains an ABNF definition of the NSI; if there is a canonical regex, it could also be noted here)</em>

## Example

<em>(include at least one example of a DID that conforms to your spec's rules)</em>

# JSON-LD Context Definition

<em>(If your method involves storing any state in a DID document for purposes of controlling updates to the DID document, you MUST define a JSON-LD context in this section.)</em>

[[[ The official definition of the btcr JSON-LD context is:
<pre>
{   "@context":   {      "Person": "http://xmlns.com/foaf/0.1/Person",      "xsd": "http://www.w3.org/2001/XMLSchema#",      "name": "http://xmlns.com/foaf/0.1/name",      "nickname": "http://xmlns.com/foaf/0.1/nick",      "affiliation": "http://schema.org/affiliation",      "depiction":      {         "@id": "http://xmlns.com/foaf/0.1/depiction",         "@type": "@id"      },      "image":      {         "@id": "http://xmlns.com/foaf/0.1/img",         "@type": "@id"      }

}
</pre>

With minor edits, this is published at [https://example.com/mycontext.jsonld](https://example.com/mycontext.jsonld).  Changes are expected as this template evolves... ]]]

# CRUD Operation Definitions

## Create (Register)

<em>([Instructions from the DID spec: ](https://w3c-ccg.github.io/did-spec/#create)The DID method specification must specify how a client creates a DID record—the combination of a DID and its associated DDO—on the target system, including all cryptographic operations necessary to establish proof of ownership.)</em>

[[[ To create a DID, you must submit a transaction that looks like this: …

The transaction must be signed <in the following way>, and must meet these additional requirements: …

Possible outcomes from the creation operation include: 0 "Success", error 1 “Malformed transaction”, error 2 “Permission denied”... ]]]

## Read (Resolve)

<em>([Instructions from the DID Spec: ](https://w3c-ccg.github.io/did-spec/#read/verify) The DID method specification must specify how a client uses a DID to request a DDO from the target system, including how the client can verify the authenticity of the response.

This section should define both lookup of a DID document from a DID and how to cryptographically verify the response.)</em>

[[[ Anyone can read a DID, using the following procedure: …

Be aware of the following latency issues: … To help manage latency wisely, the response includes a proof of correctness at a given timestamp, which works like this: ... ]]]

## Update

<em>([Instructions from the DID Spec: ](https://w3c-ccg.github.io/did-spec/#update)The DID method specification must specify how a client can update a DID record on the target system, including all cryptographic operations necessary to establish proof of control.

The DID Specification does not prescribe any single DID Document update mechanism, but a mechanism SHOULD be chosen to support key recovery.  

Some early implementations relied on permissions that could not be attenuated in a composable manner.  Veres One uses a narrower capacity as follows:

"The authorizationCapability field must contain a capability for the delegate that includes UpdateDidDocument as the capability, the DID of the delegate as the entity, and may include a more specific set of authenticationCredentials that the delegate may use to authenticate when updating the DID Document."

We're trying to NOT suggest anything other than a fully composable capability attenuation system as Best Practices.  Chris Webber proposed a workable system based on certificate chaining, but there are no current examples using the idea.  A paper is forthcoming.)</em>

## Delete (Revoke)

<em>(The method spec MUST define how to revoke a DID. Revocation is non-reversible--do not confuse it with key rotation. For example, how would you handle the DID for a company that has declared bankruptcy?.)</em>

<em>[Instructions from the DID spec: ](https://w3c-ccg.github.io/did-spec/#delete/revoke)Although a core feature of distributed ledgers is immutability, the DID method specification must specify how a client can revoke a DID record on the target system, including all cryptographic operations necessary to establish proof of revocation.

Revocation is the one way final operation for a DID.  No use after revocation is an equivalent problem to the double-spend problem, which is what motivates the use of blockchains and other distributed ledger technologies.</em>

# Versioning

## Version of this Specification

<em>(Define how this spec will be versioned. This SHOULD be by using the ReSpec template and standard ReSpec versioning mechanism.</em>

## Version of the JSON-LD Context

<em>(Define how your JSON-LD context will be versioned. This MUST use the mechansim defined in the DID spec.)</em>

# Security Considerations

<em>([See requirements in the DID spec](https://w3c-ccg.github.io/did-spec/#security-considerations)</em>

### attacks and their residual risks

*At least the following forms of attack MUST be considered: eavesdropping, replay, message insertion, deletion, modification, impersonation, and man-in-the-middle.  Potential denial of service attacks MUST be identified as well.  If the protocol incorporates cryptographic protection mechanisms, it should be clearly indicated which portions of the data are protected and what the protections are (i.e., integrity only, confidentiality, and/or endpoint authentication, etc.).  Some indication should also be given to what sorts of attacks the cryptographic protection is susceptible.  Data which should be held secret (keying material, random seeds, etc.) should be clearly labeled. If the technology involves authentication, particularly user-host authentication, the security of the authentication method MUST be clearly specified.

residual risks (such as the risks from compromise in a related protocol, incorrect implementation, or cipher) after threat mitigation has been deployed.

Recovery from a key compromise MUST be addressed.

This section MUST provide integrity protection and update authentication for all operations required by Section 7 of this specification (DID Operations).

<pre>
Confused Deputy Problem 

  When attempting separation of writeAuthorization from authenticationCredential. 

  [https://en.wikipedia.org/wiki/Confused_deputy_problem](https://en.wikipedia.org/wiki/Confused_deputy_problem)
</pre>

Other sections from DID spec to incorporate into the outline:

	9.3 Authentication Service Endpoints
	9.4 Non-Repudiation
	9.5 Notification of DDO Changes
	9.6 Key and Signature Expiration
	9.7 Key Revocation and Recovery *
</pre>

# Privacy Considerations

[[See requirements in the DID spec]](https://w3c-ccg.github.io/did-spec/#privacy-considerations)

	10. Privacy Considerations
	10.1 Requirements of DID Method Specifications
	10.2 Keep Personally-Identifiable Information (PII) Off-Ledger
	10.3 DID Correlation Risks and Pseudonymous DIDs
	10.4 DDO Correlation Risks
	10.5 Herd Privacy

<em>Consider all 4 types of privacy in http://www.lifewithalacrity.com/2015/04/the-four-kinds-of-privacy.html.</em>

# Reference Implementations

[[[ The code at [https://github.com/myaccount/myrepo](https://github.com/myaccount/myrepo) is intended to be the preferred embodiment of this DID method. Commit hash 4fc87fc5e85b2a071abfa7d8dfb15c06cd266dd5 is the version that officially aligns with this version of the spec.

Note that the code includes a test suite (see tests/compliance_suite); any other implementations should ensure that all tests pass before they claim compatibility. ]]]

# Links and Resources

[[[ Issues/bugs for this spec, and for the reference implementation, are managed on github at [https://github.com/myaccount/myrepo/issues](https://github.com/myaccount/myrepo/issues). Many developers maintaining the code and spec tend to hang out in RocketChat at chat.myorg.org, #btcrimpl. ]]]

# Acknowledgements

