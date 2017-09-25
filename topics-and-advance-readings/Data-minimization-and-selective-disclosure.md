# Introduction

Data minimization and selective disclosure (D&S, DataMin, SelDis) are very cool applications of crypto to do magic tricks, such as proving a person is over 25 years old without revealing their birthday or even which credential vouched for the person.
 
These capabilities are needed for creating, storing, presenting, and verifying user-controlled credentials among other things: DataMin is one of three mitigations against privacy threats in RFC6973, it is featured in article 5 of the GDPR, the USA Privacy Act of 1974 and often appears in FIPPs. This group's goal is to standardize D&S techniques for the Verifiable Claims work (to be used in Blockchain systems supporting self-sovereign identity), an official work item of the W3C Credentials Community Group. Some topics we plan to address include Merkle trees for redaction, Progressive disclosure, CL Signature schemes (Camenisch-Lysyanskaya), ZK (zero knowledge) protocols such as Fiat-Shamir, ZK Snarks and Starks; also commercial providers such as Qredo. 

Current known participants in this work item are:

- * Lionel Wolberger
- * Jan Camenisch
- * Maria Dubovitskaya
- * Christopher Allen
- * Kim Hamilton Duffy
- * Manu Sporny
- * Dave Longley

The overall agenda is to bring a range of intellectual horsepower from cryptography interest/expertise to simply wrapping one's head around what we can (practically) accomplish in this space. We may pop up several levels to think through user stories to clarify the needs. 
- * Logistics
- * Go wide before we go deep
- * Go deep on language
- * Go deep on crypto & tech
- * Get code
- * Organize, prioritize
- * Report


This inventory is a step towards supporting the drafting and incubating of related Internet specifications, as well as further standardization and prototyping and testing reference implementations.


# REFERENCES WITH SOME ANNOTATIONS

Data Minimization and Selective Disclosure Repo: https://github.com/w3c-ccg/data-minimization

2010 Pfitzmann, Hansen. A terminology for talking about privacy by data minimization: Anonymity, Unlinkability, Undetectability, Unobservability, Pseudonymity, and Identity Management" Link: https://www.researchgate.net/publication/234720523_A_terminology_for_talking_about_privacy_by_data_minimization_Anonymity_Unlinkability_Undetectability_Unobservability_Pseudonymity_and_Identity_Management

RFC6973 Cooper, Tschofenig, Aboba, Peterson, Morris, Hansen, Smith, Janet 2013. Link:	https://tools.ietf.org/html/rfc6973. The draft can also be helpful, "This document focuses on introducing terms used to describe privacy properties that support data minimization." 2012 Hansen, Tschofenig, Smith, Cooper. Privacy Terminology and Concepts. Network Working Group Internet-Draft Expires: September 13, 2012. Link: https://tools.ietf.org/html/draft-iab-privacy-terminology-01

Redaction Signature Suite 2016, Draft Community Group Report 26 June 2017. Longley, Sporny. Link: https://w3c-dvcg.github.io/lds-redaction2016/  "This specification describes the Redaction Signature Suite created in 2016 for the Linked Data Signatures specification. It enables a sender to redact information in a message without invalidating the digital signature."

# AGENDA IN MORE DETAILS

- * Logistics: Who are we, who should we work with, what is our cadence, how do we meet, when is this due. 
- * Go wide before we go deep. What is this? Discovery of other groups working on these issues; literature review. Find standards, FIPPS, trends. Bring a range of intellectual horsepower from cryptography interest/expertise to simply wrapping one's head around what we can (practically) accomplish in this space. We may pop up several levels to see the broader picture. 
- * Go deep on language. Clarify our nouns and verbs: Nouns, Inventory of relevant terms (glossary), the things/algorithms/protocols etc.  Verbs; Inventory of relevant use cases, journies, what are we trying to achieve, what the relevant nouns *do* for us. How does someone represent what they need, and how can we minimize this or be more selective? Can we handle partial claims e.g. someone asks for proof of zip code? 
- * Go deep on technical issues. What crypto is available? Innovations in the blockchain space? How do we canonicalize (JSONLD)?
- * Get code: What procedures exist? Is there a low hanging fruit (e.g. Merkle Tree redaction?) Discover or generate examples, sample code, prototypes. 
- * Organize, Prioritize, Bring order: - List the gnarly parts: key management and revocation. Rank solutions for relevance to CCG
- * Report: Submit a report back to the CCG

