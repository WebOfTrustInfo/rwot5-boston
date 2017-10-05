==# Breaking (Down) the Law


## Intent

This document begins to simplify how we understand and especially how we talk about signatures with non-experts as well as in legal settings, specifically for the purposes of evidentiary proceedings.

The Parking Lot includes a digest of legal and other sources of information that supported the development of this work. Some topics covered are: legal statutes,  links to past work, and more... 

## Unraveling Signatures: Technical, Business, and Legal Perspectives

Imagine a scenario where Alice needs to sign a document to transact transact with Bob. That can happen via paper signature, electronic signature or digital signature. 

**Electronic vs. Digital Signatures** 

Computer-based forms of signatures such as electronic (scanning a signature and pasting it on a `.pdf`) and digital (using  public-private key pairs to generate signatures with strong cryptographic properties) are gaining widespread adoption. By ***electronic*** we mean "any sound symbol or process associated with an electronic document" (UETA) whereas by ***digital*** we mean using a unique cryptographic fingerprint that identifies the signer. Today, electronic signatures are very common and we are increasingly seeing the growth of digital signature usage via cryptographically secure mechanisms.

**Notaries**

Often the process of signing and verifying a paper signature requires the inclusion of a notary to verify the process. For Alice (labeled _A_), the notary ensures that A's signature was actually done by A (_Authenticity_ and _Provenance_) which prevents A from ever denying having signed that document (_Non-repudiation_). Furthermore, the notary also has the ability to judge A's state of mind and testify that the document was signed with free will and not under coercion (_Intent to Sign_).

 Table X shows a comparison between these three types. As one can see, electronic signatures offer the possibility of easily sharing the signed document (_Availability_) and Digital signatures introduce the possibility of hiding the signers identity (_Confidentiality_) and assurance that the document has not been tampered with (_Integrity_).

This table summarizes the challenges with the different means of creating signatures with technologies.

>**Table 1: Evolution of Signature Technologies and Legalities**

| What's the objective?  | What does this mean? | Paper | Electronic Signature | Digital Signature  |
| -------- | -------- | -------- | ------ | -------- | 
|Authentication     | You are who you say you are     | Yes**     | No | Yes |
| Provenance (also called attribition)  | You are the one who signed   | Yes** | No | Yes |
| Non-Repudiation     | You cannot deny having signed it     | Yes**     | No | Yes |
| Intent* | You meant to sign it | Yes** | No | Yes |
| Availability     | What you signed is available to all relevant parties     | No     | Yes | Yes |
| Confidentiality | The signature does not reveal the signer     | No | No | Supports     |
| Integrity     | What you see has not been tampered with     | Yes**     | No | Yes |






*Intent is a combination of Authentication, Non-repudiation, and perhaps something else.
** By a notary


So, how does a cryptographic/ digital signature happen... technically? 

Through the exchange of public-private key pairs (also called assymetric key-pairs, which consist on a private key and a public key), we can acheive many of the above objectives.  Here is an example of  key pair exchange.  

0. Alice and Bob know each other exist
1. Alice generates a public-private key pair (because Alice wants to establish a relationship with Bob)
2. Alice gives Bob a public key (because Bob wants to authenticate Alice's data) 
4. Alice signs data with private key (see below)
5. Alice sends Bob the signature and data 
6. Bob verifies Alice's signature and data with Alice's public key (see below)

(Note: Alice and Bob may be humans, machines, or any combination)

Signing the Data / Locking the Padlock: Understanding this in a different context, signing data with a private key *(step 3 above)* is similar to using a padlock. A padlock has 2 important characteristics - it can be locked by anyone and it can only be unlocked by the person with the correct combination. If we consider that unlocking the padlock is similar to signing the document, then we can be sure that Alice is the only person who signed the data (with her private key). [Note: this example will be updated over time due to the inelegance of unlocking = signing. Suggestions are welcome!]

Verifying the Signature + Data / Unsealing the Envelope: When Bob gets the data (message + signature) and verifies Alice's signature to be sure that it is the original document she provided, he uses Alice's public key to unlock it *(step 5 above)*. A public key is similar to the historical example of a King sealing an envelope with a stamp. A stamp/seal combination allows only 1 person to seal the envelope while anyone can open it. 

An attorney can use digital signatures with strong cryptographic properties to satisfy evidentiary requirements. Let us walk through it:

>* Did Alice sign the document? 
>* Are we sure it was Alice?
>* Can Alice deny that she signed the document?
>* Did Alice intend to sign the document?

Yes. The authenticity and non-repudiation properties (see Table 1) are sufficient to satisfy this.

>* Does Alice know what she signed?

Not necessarily. To ensure this a secondary mechanism should be implemented, such as a pop-up box that asks for confirmation or a complicated pattern to trace, similar to a software license agreement. The point here is to require an action to acknowledge awareness.

>* How did Alice sign it? 

She signed it by providing her private key (that only she controls) to a piece of software responsible for generating the digital signature.

 
>* Who verified that Alice signed the document?

Pending on the availability of the document and Alice's public key, anyone can verify the signature.

>* Did Alice sign the document before Bob verified it? 

Yes. Bob requires a digital signature to input into a digital signature verifier software. Without that input (which is provided by Alice) verification is impossible.

>* Is Alice a person?

Digital signatures do not offer this by default, an aditional sofware mechanism would be required to verify that Alice is a person.



## Next Steps  
1. Review/cull all Parking Lot content
2. Supplement the technical explanation with additional legal language and statutes
3. Differentiate legal language and technical realities (eg: owning a single digital copy of something isn't possible as it is with paper)
4. Answer the question: What gaps exist in today's legal frameworks?
5. Better understand why the legal requirements have been established to satisfy technical capabilities 
6. Answer the question: How does the current non-digital signing behavior compare to technical capacity () and how can current technical advance current legal capacity?
7. More and more and more


## Contributors  
Dazza Greenwood <dazza@civics.com>
Eva Shon <eva.shon@consensys.net>
Tiemae Roquerre <roquerre.t@gmail.com>
Peter Todd <pete@petertodd.org>
Lily Bragg <lilyb@vouch.id>
Christian Smith <smith@anvil.io>

===========================
===========================

# PARKING LOT


## Intro

Decentralized trustworthy computational systems, such as blockchain and DID's are bringing up valid questions on how to treat requirements on legal primitives such as signature, commitments and single use seals. The very nature of decentralized technoligies requires a re-examination of why certain requirements exist and an understanding of how they can be mapped to said technologies.

Building an appropriate and robust blockchain-based digital signature or notarization tool requires not only business and technical requirements but also legal and evidentiary requirements. Part of the crosswalking from digital to manual, will require a process for people to change (involving management, and training). Moreover, appropriately handling scalable processes to execute "digital-unique" processes are needed to transition from manual to digital processes for signatures and related legal activities. 

# Matrix



# Primitives 



# Conclusion 
The intersection of legal primitives and decentralized computational systems accents the need for the law to be written in a way that is broad enough to be flexible amongst various systems, while also getting to the heart of problem they aim to solve. The question of which parts of the law remain the same, changes or must be completely re-evaluated remains an ongoing conversation that will evolve.


* Slack channel for this workgroup: [#breaklaw](https://weboftrustinfo.slack.com/messages/ZZZ

## Transferable Records: 
* UNCITRAL: [http://www.uncitral.org/pdf/english/texts/electcom/MLETR_ebook.pdf](http://www.uncitral.org/pdf/english/texts/electcom/MLETR_ebook.pdf)
* [UETA (Section 16)]




| Legal Requirement | Tech Capability | Notes |
| -------- | -------- | -------- |
|  single authoritative copy   | Text     | Text     |
|  identifying "the person"   | Text     | Text     |

## single authoritative copy

The phrase "single authoritative copy" is fundamentally incoherent because the word "single" and "copy" conflict on the face of the meaning.  Adding the qualifier "authoritative" provides opportunities for creaetive legal interpretation but the technical reality is that there is ot way to distinguish between copies of digital information.  

* A constructuctive 


# Intro

The goal of this document is to review the requirements related to distributed trustworthy computational systems such as for blockchain, DID's and more generally for electronic signatures and e-notarization, understand why they exist and discuss how they can be mapped to decentralized technologies.

Building an appropriate and robust blockchain-based digital signature or notarization tool requires not only business and technical requirements but also legal and evidentiary requirements. 

Part of the crosswalking from digital to manual, will require a process for people to change ( involving management, training, ...

Moreover, appropriately handling scalable processes to handle "digital-unique" processes are needed to transition from manual to digital processes for signatures and related legal activities. Examples of important and new types of processes include:

Process

1. Generate cryptographic credentials - not necessary for any central party for who generated it...should be generated by subject's own resource (offline process i.e. coin toss) --> no one else knows private part of key pair.
2. Bind real identity to public key - proving key ownership - Use public key to verify the ownership (i.e. certificates, recording on blockchain) --> in order to make sure it's you, a trusted third party would have to verify by putting their signature on the key) --> certificate doesn't include personally identifying identity of owner of key, would give identity of issues and then you would find identity of issuer. With the current PKI mechanism, identity is binded to a key via a Public Key certificate which is signed by a certification authority (a trusted party). In the DID model, that is not the case.  Much like in the PKI with certificate authorities, a DID can be used to retrieve a public key of its owner, however, by itself that provides little information about the identity of the owner. One of the properties of DIDs is that it gives the owner the ability to anchor documents, DID Docs, to the DID itself. This can be leveraged to anchor relevant information about you identity to your DID. The more information diplayed, the more likely another person will be to trust that you are who you say you are.

--> how to create protocal for backwards lookup 

3. 

# Current Matrix

## Cross-Ref for Legal Signature to Technical Capabilities

Legal rules for this come from the [Uniform Electronic Transaction Act](https://github.com/mitmedialab/rebooting-the-web-of-trust-fall2017/blob/master/draft-documents/BreakingDownAndConnectingLawAndTech/LegalSources/ueta_final_99.pdf),
[UNICITRAL Model Law on Electronic Transferrable Records](https://github.com/mitmedialab/rebooting-the-web-of-trust-fall2017/blob/master/draft-documents/BreakingDownAndConnectingLawAndTech/LegalSources/ueta_final_99.pdf), the [Model Notary Act](https://github.com/mitmedialab/rebooting-the-web-of-trust-fall2017/blob/master/draft-documents/BreakingDownAndConnectingLawAndTech/LegalSources/2010_model_notary_act.pdf)

Most important legal rules from which technical requirements can be elicited:

**Definition of signature:** “Electronic signature” means an electronic sound, symbol, or process attached to or logically associated with a record and executed or adopted by a person with the intent to sign the record.

| Legal Rule or Requirement |  Technical Requirement | Can Currently be Provided by |
| -------- | -------- | -------- | -------- |
| "Any sound, symbol or process"     |  Signer Attribution | Digital Signature | 
| "executed or adopted"    | Signature Action/Event     |  Timestamp |
| "by a person"     | Signer Authentication | Digital Signature |
| "with the intent to sign"     | Signer Authorization | Digital Signature &amp; Approval |
| "attached to or logically associated with the record"    | Record Authentication     | Signing a hashed record &amp; later verification |

(TODO - how can the table above be made more useful and is it correct?)

# Connecting Legal and Technical Dimensions

## Any sound, symbol or process	

#### How this technical capability addresses this legal requirements or constraint

#### Why does this legal requirements exist in the first place?

* Evidence

## Executed or adopted 

#### How this technical capability addresses this legal requirements or constraint

#### Why does this legal requirements exist in the first place?

* Ceremony

## by a person	

#### How this technical capability addresses this legal requirements or constraint

#### Why does this legal requirements exist in the first place?

* Distringuish between tools and legal entities

## With the intent to sign	

#### How this technical capability addresses this legal requirements or constraint

#### Why does this legal requirements exist in the first place?

#### Attached to or logically associated with the record

#### How this technical capability addresses this legal requirements or constraint

#### Why does this legal requirements exist in the first place?

* Intent can be proved for someone being forced to track through a process. I.e. trace through a complex design, like a cat, or pattern?


# Decentralization Considerations

What changes might blockchains, [DIDs](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md), and other decentralized web technologies bring to the digital signature process?

| Legal Rule or Requirement |  Technical Requirement | Decentralization Technology |
| -------- | -------- | -------- | -------- |
| "Any sound, symbol or process"     |  Signer Attribution | DID-based digital signature with a log of all key rotations | 
| "executed or adopted"    | Signature Event     |  Digital signatures recorded on a blockchain as a timestamped transaction |
| "by a person"     | Signer Authentication | DID-based identity with claims from KYC providers |
| "with the intent to sign"     | Signer Authorization |  |
| "attached to or logically associated with the record"    | Record Authentication     | Document hashes showing integrity can be on blockchain  |

## Critical Technical Considerations

**Know Your Customer and DIDs** 

Signer and document provider verification will require Know Your Customer (KYC) such as government-issued issued attestations about certain DIDs. Similar to how a 

**DIDs and Key Rotations** 

Cryptographers recommend key rotation with DIDs as a security best practice, but could that invalidate or make DID-based digital signatures using past keys obsolete? Keeping a timestamped log of past keys will be necessary to ensure continued digital signature integrity. Even if a key is compromised in the future, cryptographic timestamp may be able to provide sufficient evidence of past validity. Perhaps future DID method specifications will require 

may say blockchain must keep it but if it can't may have ot keep some portion of it in some did document of retired keys




**Proof of Location for Notary**

Physical requirements of being present at a notarization event with a notary and/or witnesses may not be replicable in digital space. Although some states allow for webcam-based notary, there has been a known case of fraud where a signer was impersonated by an imposter using computer-generated imagry [source???]. [The Model Electronic Notarization Act of 2017](https://www.nationalnotary.org/knowledge-center/reference-library/model-notary-act/model-electronic-notarization-act) recommends that... [TODO - add some summary of this act if its relevant!].

Solving for these problems is still a technical challenge. For example, digital proof of location at a certain point in time to show that all relevant parties were present is still a research problem. Cell phone location data has been admissable for criminal cases but also have privacy tradeoffs. Perhaps in the future other personal device data (Fitbit, Apple Watch, etc.) and other kinds of tracking data can be triangulated as evidence, but these service do not exist in easily digestible format at this time.

#  Legal &amp; Usability Frameworks

The goals of the ESIGN and UETA (Uniform Electronic Transaction Act)

The following sections describe some important legal considerations in designing electronic and digital signature systems. These explain why these systems are the way they are, what they should aim for and what users should perhaps be made aware of when interacting with them.

### The Act of Signing

Signing a record can be an act with legal impact. The [American Bar Association's Digital Signature Guidelines](http://apps.americanbar.org/dch/thedl.cfm?filename=/ST230002/otherlinks_files/dsg.pdf) (page 5) explains that the act of signing should provide the following key features: 
> 1. **Evidence** that authenticates and is attributable to the signer and of the integrity of the record
> 2. **Ceremony** as an act of signing and its legal significance
> 3. **Approval** as the signer's agreement with and authorization of what is written and
> 4.  **Efficiency &amp; Logistics** in the clarity and finality a signature imparts in consenting to a transaction or negotiation (to improve the efficiency of commerce).

The general goals are to prevent fraud and tampering, inconsiderate engagements, misconstruing what has been approved, ambiguity and inefficiencies in communication around transactions, and preventing parties from modiying or terminating valid legal obligations that are enforceable in court.


### Legal Risks and Enforcability

Bloomberg's [Enhancing the Admissibility and Enforceability of
Electronically Signed Documents](https://www.esignlive.com/site/_media/pdfs/Bloomberg_Law_Report-Enhancing_the_Admissibility.pdf?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3B%2B74jfaPaTbKtE1C4E5pJEQ%3D%3D) provides the following six-point framework for evaluating risks in electronic signature integrity.

> 1. **Authentication Risk** - a signer or record provider is an imposter or false identity
> 2. **Repudiation Risk** - a record is altered after signing
> 3. **Admissibility Risk** - one party challenges whether a record is admissable because it is unreliable
> 4. **Compliance Risk** - the records or signatures do not comply with requirements of local laws
> 5. **Adoption Risk** - the user experience is too difficult leading to omissions or signer dissatisfaction
> 6. **Relative Risk** - users should evaluate whether an electronic signature process is any riskier than paper and ink signature

Digital signature technology based on public-private key cryptography and hash functions, and now blockchains and other decentralization technology can significantly mitigate many of these risks although in some cases they can also introduce new risks. (We could make another table here or just quickly explain how these can be addressed...)

* Burden of Proof and Evidentiary Requirements for electronic signatures:
 (TODO - 1. talk about differences between US and EU - in the US the burden of proof is on the signer vs. the document owner)
[Source](http://www.pciaa.net/docs/default-source/meetings/20170727_1055_update-on-e-sign-and-digital-business-practices-and-blockchain-101---part-2_denise-vieira.pdf?sfvrsn=2)


## Matrix Roadmap 

| Legal Requirement| Tech Capability | Notes | Why |
| -------- | -------- | -------- | -------- |
| Attribute     | ip address, browser     | Text     | Text   //not sure what this is about... attribute of what? - I knew the link I clicked is tied to the action I intended//     |
| Attest     | Text     | Text     | Certify that affiant is the correct person        |
| License     | state notary public service validation with timestamp      | Text     | Confirm that the notary is entitled to perform the function //should also include active verification + notification of status//       |
| Sign     | Text     | Text     | Commit and associate notary to legal document        |
| Witness     | Text     | Text     | Mitigate the possibility of collusion       |
| Notarize     | Text     | Text     | Certify the integrity of the document with an apostille       |
| Intend     | depends on implementation     | Text     | Text       |
| Require Signature     | Text     | Text     | Text       |
| Text     | Text     | Text     | Text       |


## 

## Use Cases

1. **Legal Signature**
2. **Notary**
2. Birth Certificate
3. Education Credential
4. Profession/Job (Verfication)
5. Transferrable Records (Bearer)
6. Government-issued ID

**focus areas for this project**

## Use Case #2 - Notary
### Participants for Notary
Trudy = Notary
Bob = Customer
Priya = Prosecutor

### User Story

Bob (a Customer) has a will that he wants to notarize. He requests that Trudy (a Notary) witness his signing the will. Later on, Priya (Prosecutor) must verify that the will is legitimate in a court of law. 

### Actions

#### Establish identity page

> Trudy, the notary, needs credentials to prove she's a notary.

- She needs to get training
- She needs to get a Government issued Notary licence
- That Notary license needs to have an ID

> Bob, the customer, needs to find a notary and establish a trust relationship with him.

- Validate the notary's credentials
- Fancy seal?
- Needs to know the physical location of the notary
- Reviews of the notary

> Priya, the prosecutor, needs to ensure that the notatization process obeyed the law


## FAQ

Question: Should the "intent" and "execution" legal elements be combined as one (on the same row)?

Answer: No. Ex. Sometimes when work at company, you recieve a check signed by a signature machine. There are documents agreed upon and documented before that indicates what constitutes intent. 

Question: Should "Sound/Symbol/Process" and "Intent" be combined as one?

Answer: No. 



- 
## Housekeeping



GitHub for draft:

https://github.com/mitmedialab/rebooting-the-web-of-trust-fall2017/tree/master/draft-documents/BreakingDownAndConnectingLawAndTech
?>>
Note: This is the [medialab's forked repo](https://github.com/mitmedialab/rebooting-the-web-of-trust-fall2017) of the RWOT repo.

Slides to collaborate on diagrams: https://docs.google.com/presentation/d/11qrEZk1-FyD9h7mvig7VT5oR-kmZ7PVyeOkx9gmAQwY/edit#slide=id.p

End Goal: 
1. MIT Media Lab
-Medium
-Huffington Post
2. Consensys Blog


Attack Surfaces - Threat Analysis

Soverign Identity v. 





# Blockchain and Law Briefing Book



## The [Blockchain and Law Briefing](https://computationallaw.org/blockchain-briefing-450aa4fb8d7c)

> The [Blockchain and Law Briefing](https://computationallaw.org/blockchain-briefing-450aa4fb8d7c) is a [blog post](https://github.com/mitmedialab/BlockchainBriefingBook/edit/master/README.md) (occassionally updated on [ComputationalLaw.org](ComputationalLaw.org)) providing an informal and general high level overview of blockchain and law.  

Filling out the Blockchain Briefing narrative form, the below table of legal issues and examples is offered as a starting point for in-house and other legal counsel to learn about more general principles and practices related to blockchain technology.

## Table of Blockchain Legal Issues and Examples

| Legal Issue |  Example Situation  |  Leg/Reg Status  | Version & Comments   |
|-|-|-|-|
| Does Blockchain Satisfy Long Term Records Retention Requirements? | US Federal Credit Unions are expected to permanently retain Individual Share and Loan Ledgers | [12 CFR 749](https://www.ecfr.gov/cgi-bin/text-idx?SID=6762593933cc723eab43cd5567470b75&mc=true&node=se12.7.749_10&rgn=div8) | Version 1.0 ([Relevant Materials](https://github.com/mitmedialab/BlockchainBriefingBook/tree/master/IssuesAndExamples)) Public Blockchain [OP_RETURN](https://github.com/mitmedialab/BlockchainBriefingBook/blob/master/IssuesAndExamples/OP_RETURN-BitcoinWiki.pdf) can ensure [evidentiary proof](https://github.com/mitmedialab/BlockchainBriefingBook/blob/master/IssuesAndExamples/OP_RETURN-for-Evidentiary-Records.md) by maintaining long term publicly verifiable hashes of records, addressing a key and costly aspect of ["permanent"](https://github.com/mitmedialab/BlockchainBriefingBook/blob/master/IssuesAndExamples/PermanentRecord.md) retention of [regulated records](https://github.com/mitmedialab/BlockchainBriefingBook/blob/master/IssuesAndExamples/NCUA-RecordsRetentionPost.md) expectations.  |
| Are Blockchain Signatures Enforceable Admissible in Court as Evidence? | A merchant seeks to introduce evidence of the blockchain signature of a consumer on a contract for the sale of a used car  |  [UETA](http://www.uniformlaws.org/Act.aspx?title=Electronic%20Transactions%20Act) and [ESIGN](https://www.gpo.gov/fdsys/granule/USCODE-2011-title15/USCODE-2011-title15-chap96/content-detail.html) and [31 C.F.R. § 370.39](https://www.gpo.gov/fdsys/search/pagedetails.action?collectionCode=CFR&browsePath=Title+31%2FSubtitle+B%2FChapter+II%2FSubchapter+B%2FPart+370%2FSubpart+D%2FSection+370.39&granuleId=CFR-2005-title31-vol2-sec370-39&packageId=CFR-2005-title31-vol2&collapse=true&fromBrowse=true) |  Version 0.2 - ([Relevant Materials](https://github.com/mitmedialab/BlockchainBriefingBook/tree/master/LegalSignatures)) A valid signature may be formed by any sounds, symbol of process including Blockchain based electronic processes.  Blockchains provide extrinsic evidence regarding the authenticity of the digital signature needed to lay a proper foundation for admissibility.  The evidence is sufficient to prove the electronic message to which the digital signature is affixed has not been altered from its original form" and that the "digital signature corresponds to a specific public key pair." |
| Are Smart Contracts Enforceable as Legal Contracts? | tbd | [UETA](http://www.uniformlaws.org/Act.aspx?title=Electronic%20Transactions%20Act) and [ESIGN](https://www.gpo.gov/fdsys/granule/USCODE-2011-title15/USCODE-2011-title15-chap96/content-detail.html) |  Version 0.2 - ([Relevant Materials](https://github.com/mitmedialab/BlockchainBriefingBook/tree/master/LegalContracts)) Current [drafting notes re adequacy of contract formation and evidentiary issues](https://github.com/mitmedialab/BlockchainBriefingBook/blob/master/LegalContracts/README.md) and [good practice examples](https://github.com/mitmedialab/BlockchainBriefingBook/blob/master/LegalContracts/README.md#monax-dual-integration-approach)  |
| Do Records Entered onto Blockchain Satisfy Admissibility Requirements as Evidence? | tbd | tbd | Version 0.1 - ([Relevant Materials](https://github.com/mitmedialab/BlockchainBriefingBook/tree/master/LegalNotice))  |
| Does Blockchain Provide Valid Legal Notice? | tbd | tbd | Version 0.1 - ([Relevant Materials](https://github.com/mitmedialab/BlockchainBriefingBook/tree/master/LegalNotice))  |
| Does Blockchain Provide Satisfactory Record of Legal Title to Property? | tbd | tbd | Version 0.0 -  ([Relevant Materials](https://github.com/mitmedialab/BlockchainBriefingBook/tree/master/LegalTitle)) |


Transferable Records:
Change to make: If you interpret single authorize copy as single authoritatize version
WHY: To act on digital data means you have to make copies, consensus on the version
of document is okay 




## Existing Laws on Blockchain-based Signatures &amp; Smart Contracts

Arizona passed **House Bill 2417** legalizing blockchain-based signatures and smart contracts in commerce:

https://legiscan.com/AZ/text/HB2417/id/1588180


==
