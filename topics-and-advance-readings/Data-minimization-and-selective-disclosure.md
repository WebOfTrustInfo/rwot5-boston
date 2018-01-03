Engineering Privacy for Verified Credentials: 
In Which We Describe Data Minimization, Selective Disclosure and Progressive Trust 
==============================

Contributors:

* Lionel Wolberger, Independent
* Brent Zundel, Evernym/Sovrin
* Zachary Larson, Independent
* Irene Hernandez, Independent 
* Katryna Dow, Meeco

# Introduction

This paper explains how privacy can be enhanced while credential attributes are shared electronically. We explain three related but distinct privacy enhancements of "data minimization," "selective disclosure," and "progressive trust." We describe in plain English, but with some rigor, techniques that enable these enhancements. We also show what we are talking about in diagrams and animations, to visualize the communication flows. 

Our goal is to enable decision makers, particularly non-technical ones, to gain a nuanced grasp of these enhancements along with some idea of how their enablers work. We include enough detail for those who wish to dive deeper. This knowledge will, in the end, lead readers of this paper to be better able to know when they need privacy enhancements, what type of enhancement best suits the use case, assess techniques that enable those enhancements, and adopt the correct enhancement for the correct use case. 

## Three examples

To grasp the problem, here are three examples of how people would like privacy preserved in the process of sharing credentials.

You attempt to login to an online service and are asked for your Facebook name. You know that the service may read from your Facebook account a broad range of data without your meaningful consent. You hesitate, since the service doesn't need everything in your Facebook account. What will it read today? What will it read in future? You are not sure. Is there a way to login with your Facebook data while revealing only a minimal amount of information? 

You hand your driver's license to a bouncer to prove you are of drinking age. As he looks it over, you realize he is looking at your date of birth and home address. He only needs to know that you are over 21. Is there a way to disclose your approximate age without revealing your actual age, along with your home address and city of residence as well? 

In negotiations with a real estate agent to purchase a home, you reveal a letter from your bank stating your credit limit. You wanted to reveal its approximate amount only, but the agent insisted on verifying that the letter was authentic. You feel the agent now has the upper hand in the negotiation. Could you have revealed only an approximate amount, and reveal more details as the negotiations progress?

Each story highlights a particular privacy enhancement: the first "data minimization," the second, "selective disclosure," and the third, "progressive trust." 

## What are credentials and attributes?
A credential is a statement of information relating to a subject, such as "my age." The precise definition from the W3C VC: A credential is a qualification, achievement, quality, or piece of information about an entity's background such as a name, government ID, payment provider, home address, or university degree. Such a credential describes a quality or qualities, property or properties of an entity which establish its existence and uniqueness. A credential has an issuer, inspector, subject and holder. 

An attribute is a value associated with a credential. For example, "January 1, 1980" is a date that could be an attribute associated with a birthday. 

## What are verifiable credentials?
A verifiable credential is a credential that is effectively tamper-proof, and whose authenticity can be verified in an automated fashion.  A credential in-and-of-itself, as long as it is stored properly, does not need privacy enhancement. It is when the credential is verified that it is exposed to inspection and our privacy concerns are brought to bear. 

## Do attributes need to be formatted for privacy-enhancement?
Yes. The formatting of an attribute makes it more or less amenable to privacy-enhancing treatment. Privacy enhancement is much more efficient when standardized formats are used. 

The World Wide Web community has many ways of formatting data. Some were standardized to enable search engines to understand the information on web pages and provide richer search results. While unformatted data can be interpreted by using data extraction methods, these can be error prone because information can be represented in so many different ways. 

## Do attributes need to be numeric?  
While all electronic information is handled as numbers, there are different kinds of numbers. The ability of a system to enhance privacy depends on the kinds of numbers involved. 

* Nominal numbers answer the question, "what is the identifier?"
* Ordinal numbers answer the question, "in what order?"
* Cardinal numbers answer the question, "how many?"

Numbers that name things are like the number 012 representing the letter, "A," according to ASCII, or telephone numbers and sports team jersey numbers. Called "nominal," from the word for name, these numbers identify things and act like names. They do not reflect a quantity, or a preferred ranked order. Some numbers account for a rank or position, called "ordinal," from the word for order. These numbers' are intended to state their position or rank in relation to a set of other numbers—3rd fastest runner, 6th in line, or 1st letter of the alphabet. Numbers that count quantities, confusingly called "cardinal," from the word for "chief," tell "how many" we have: 8 puppies, 14 friends or 26 letters of the English alphabet. Cardinal numbers resemble ordinal—3rd is more than 2nd—but they differ in subtle ways that are important to data minimization.

To illustrate why these differences between numbers are important, imagine you are buying a car, you open your bank account page and it says "52433". Is this number nominal, the name of your bank account? Is it ordinal, showing the 52,433rd transaction of the day? Or is it a quantity, perhaps your bank balance showing that you have $52,433.00? Privacy enhancement strategies will differ, depending on the numeric qualities. 

##Do we need cryptography?

##The role of cryptography
In privacy enhancement of credentials, some data parts are revealed while others are concealed. Concealment is achieved mostly by the art of cryptography, from the greek word "kryptos," meaning hidden, like in a crypt. Cryptography makes privacy enhancement possible in electronic communication. 

### Crypto Goals 
Privacy-enhancing cryptography has four primary goals.

* **Confidentiality**: a hidden part of a credential cannot be understood by anyone for whom it is unintended. Often called "privacy," we avoid that word here since it can mean many thingsz in addition to confidentiality. 
* **Authentication**: the identity of information shared can be validated as authentic. 
* **Integrity**: the revealed part of the credential cannot be altered without such alteration being detected. Also known as validity, fidelity or verifiability. 
* **Non-repudiation**: aka non-deniability, a credential's creator cannot deny at a later stage his or her involvement.

### Crypto enablers
Cryptography's ability to enhance privacy relies on a broad range of techniques, algorithms and protocols. For the purposes of this paper we can group them into three primary cryptographic enablers: secret management, difficulty levels, and zero knowledge. 

The three enablers can be explained by considering the "Where's Waldo?" visual puzzles. On each page of these books a distinctively dressed man in a striped hat appears at a stop on his "world-wide hike". Somewhere amid each densely illustrated crowded scene is Waldo and readers are asked to scour the page and locate the lost traveler. 

* **Secret management**: The location of Waldo is a kind of secret: the illustrator knows it, and you don't. You could raid the publisher's offices and perhaps find the secret stored somewhere. Of course, once you find Waldo you could keep it secret by circling him in red and putting the book in your safe. Secrets in cryptography are usually called "keys," and a "private key" is a particular kind of secret that must be managed. 
* **Difficulty**: Waldo puzzles are difficult to solve yet easy to verify. That's why it is a puzzle! You have to search everywhere and mistakenly eye many characters who look like Waldo before reaching a satisfactory finish and finding him. But checking if Waldo was found is rather simple. Just point to Waldo before a verifier and he can see--there he is. You did solve the puzzle correctly. This difference between the difficulty of solving as opposed to verifying is a core concept in computational complexity, and lies at the heart of cryptographic enablers. 
* **Zero knowledge**: You can prove that you found Waldo without revealing the secret that you labored hard to uncover. Take a huge white rectangular piece of white cardboard that is much larger than the Where's Waldo illustration. Cut a hole exactly fitting Waldo, that reveals only his silhouette and nothing else. You can now show Waldo to any verifier: there he is! Yet the cardboard is so wide, hiding the book so well, a verifier has no idea where Waldo is on the page's illustration. A verifier can say without any doubt yes, you have indeed found Waldo, because Waldo is right there. you solved the puzzle and had someone verify that achievement, without revealing any knowledge of how to solve the puzzle yourself. This is a zero knowledge proof, an useful capability in privacy enhancement. 

This terminology, while highly simplified, will help the lay reader understand just how privacy enhancement works. For example, we may say: to enhance the privacy of an age credential (I am older than 21 years), the credential holder has a secret to manage. This secret key is applied to hide her birthday in various difficult mathematical puzzles. The inspector performs a zero knowledge proof on those puzzles and determines the credential is valid, without revealing her birthday. 


# Privacy enhancements
We have three strategies for enhancing privacy while credential attributes are shared: data minimization, selective disclosure and progressive trust. Each strategy involves the use of cryptography, which in turn requires that the credentials and their attributes be formatted in specific ways.

## Data minimization
Data minimization is the act of limiting the amount of shared data strictly to the minimum necessary in order to successfully accomplish a task or goal. 

Minimization has three types:

* Content minimization – the amount of data should be strictly the minimum necessary.
* Temporal minimization – the data should be stored by the receiver strictly during the minimum amount of time necessary to execute the task
* Scope minimization – the data should only be used for the strict purpose of the active task. 
Data minimization is largely a policy decision.

Data minimization capabilities impact the credentials ecosystem in the following ways.

* issuer: ensure that the credential is presented in such a way as to enable data minimization. This may require issuing multiple, related, atomic sub-credentials. 
* inspector: establish in advance policies regarding:
	* what is the minimum data necessary to accomplish the task or goal. 
	* what is the minimum time the data can be stored to execute the task
	* how to ensure that the data is applied only to that task and does not, by a process of scope creep, become applied to other tasks or goals.

## Selective disclosure
Selective disclosure is the ability of an individual to granularly decide what information to share. Selective disclosure is a means by which data minimization can be achieved.

Selective disclosure capabilities impact the credentials ecosystem in the following ways.

* issuer: format the credential in such a way as to enable selective disclosure. This may require issuing multiple, related, atomic sub-credentials. It also may require formatting the credential to support mathematical queries and cryptographic proofs
* inspector: ensure the request is framed in such a way as to enable selective disclosure. (This is a data minimization task that impacts selective disclosure). What is the way to request the credential that would enable a subject to selectively disclose the minimum data necessary to accomplish the task or goal. 

## Progressive trust
Progressive trust is the ability of an individual to gradually increase the amount of relevant data revealed as trust is built or value generated. 

Progressive trust capabilities impact the credentials ecosystem in the following ways.

* issuer: format the credential(s) in such a way as to enable progressive trust. This may require issuing multiple, related, atomic sub-credentials. It also may require formatting the credential to support mathematical queries and cryptographic proofs. Finally, it requires a data model expressing how the various sub-credentials are related in a scenario involving progressive trust. 
* inspector: ensure that requests are framed in such a way as to enable progressive trust. (This requires the first two enablers, data minimization and selective disclosure as well). Structure the communication in order to to gradually escalate credential requests in such a way that would enable a subject to progressively trust the inspector more and more, revealing the minimum data necessary to accomplish each step of the task or goal, and reveal more and more as our communication progresses. 


# Implementations
Follow the process step-by-step by viewing the diagrams.

### Code for [Web Sequence Diagram](https://www.websequencediagrams.com/):
Copy and paste the code below into the [Web Sequence Diagram](https://www.websequencediagrams.com/) webpage to generate the flow diagram. 

~~~~

title Verifiable credential using Selective Disclosure
participant Valid Time Oracle
participant Janet
participant ID Provider
participant Ledger
participant Bar

note over Janet:Prover
note over Bar:Validator

note over Janet,Bar: Preparation and Setup

note right of ID Provider:Infrastructure
ID Provider->Ledger: Define Schema (Name, Birthdate, Address)
ID Provider->Ledger: credential Definition (Pub Key, etc.)
ID Provider->ID Provider: Generate Prv Key for this credential
ID Provider->Ledger:Revocation Registry

note left of Bar: Prepare to accept credentials
Bar->Bar:Install Agent
Bar->Ledger: Check schema

note over Janet,Bar: Begin Use Case
Janet->ID Provider: Request ID
ID Provider-->Janet: ID will be issued as a digital credential
note right of Janet: Prepare to receive credentials
Janet->Janet: Install Agent
Janet->Janet: Prv Key Generate, Store
Janet->Ledger:Check Schema
Ledger->Janet:credential Definition
Janet-->ID Provider:Proof of Name, Birthdate, Address
Janet->ID Provider: Blinded secret
ID Provider->Janet: credential
Janet->Janet: Validate credential against credential Def

note over Janet,Bar: Janet goes to the bar
note left of Bar: Can Janet Enter?
Bar->Janet: Request Proof of Age
Janet->Valid Time Oracle: Get time
Valid Time Oracle->Janet: Time credential
Janet->Janet:Generate Proof (This person is over 21)
Janet->Bar: Provide Proof
Bar->Bar: Evaluate proof
Bar->Ledger: Verify on Ledger
Ledger->Bar: Verification
Bar->Janet: Come in

note left of Bar: Invite to club

Bar->Janet: Join loyalty club? (requires valid postal code)
Janet->Janet:Generate Proof (postal code)
Janet->Bar: Provide Proof
Bar->Bar: Evaluate proof
Bar->Ledger: Verify on Ledger
Ledger->Bar: Verification
Bar->Janet: Have Loyalty Card

~~~~

# Methods
This section will show an implementation of verifiable credentials that allows for privacy enhancement of credential attributes. In order facilitate understanding of the implementation, we first provide a section providing a view of topics in number theory and cryptography.

## Background
We begin with a brief overview of several concepts from number theory that serve as a foundation for the cryptography that enables selective disclosure.

Cryptography is a huge field with highly specialized jargon, too much to cover here. But non-specialists who use verified credentials need some understanding of cryptography in order to make informed decisions. The next section covers a set of basic concepts that enable users of verifiable credentials to understand the most critical cryptographic concepts. We present a curated list of topics progressing from the simple to the more complex. Notice how ideas are re-used and layered as read on. 

### Number Theory
Number theory refers to the study of the behavior of integer numbers such as 1, 2, 500. The following are behaviors of these numbers that make them useful in cryptography:

* Prime or not: A prime number is divisible by only itself and 1. 
* One way function: A numerical function that takes a publicly known number, and without any secret information, computes a value. Given that value, it is hard to find the publicly known number. Like a one way street, computation goes only one way. 
* Modular arithmetic, aka clock arithmetic: a system of arithmetic where numbers "wrap around" upon reaching a certain value—the modulus. A familiar use of modular arithmetic is in the 12-hour clock, in which the day is divided into 12-hour periods. If the time is 7:00 now, then 8 hours later it will be 3:00. 7 + 8 usualy equals 15, but this is not the answer because clock time "wraps around" every 12 hours. 
* Groups and Finite Fields: A subset of all integers can form a group, which behaves in ways very useful to the performance of cryptography. Finite fields are types of groups that satisfy certain demanding properties. 
* Discrete Logarithms: The logarithm log(b) of a is an exponent x such that b^x (b raised to the x exponent) = a. A discrete logarithm is a property for numbers in a group. Since there is no efficient method for computing discrete logarithms, they are very useful in cryptography. 
* Quadratic Residues: Quadratic refers to 'squared' numbers, a number raised to the second exponential power. Quadratic residues are a useful property of squared numbers as they behave in modular arithmetic. 

### The Cryptographic Zoo

Let's meet the inhabitants of the cryptographic zoo, by name:

* PKI, or "public and private keys": A person with a private key can, with the right software, participate in PKI (public key infrastructure) cryptography. PKI can enable all our objectives. Processes like "digital signature," "authentication," and "certificate validation," all use PKI commands which in turn require a private key. 
* Elliptic-curve cryptography (ECC) is an approach to public-key cryptography based on the numeric structure of elliptic curves over finite fields. ECC is useful as it require smaller keys compared to non-ECC cryptography. There are many variants of ECC used including Edwards-curve Digital Signature Algorithm (EdDSA) which uses a variant of Schnorr signature based on Twisted Edwards curves.
* Hash or message digest: One way functions, such as SHA 256. A Merkle tree is a set of many one way functions applied to a tree of data in which every leaf node is labelled with the hash of a data block and every non-leaf node is labelled with the cryptographic hash of the labels of its child nodes. 
* Signature: A signature in this context is a use of PKI. A signature can prove authenticity, integrity and non-repudiation of a message since a valid digital signature gives a recipient reason to believe that the message was created by a known sender (authentication), that the sender cannot deny having sent the message (non-repudiation), and that the message was not altered in transit (integrity). Signatures enable every cryptographic objective except for confidentiality. There are many types of signature schemes in use including Digital Signature Algorithm (DSA), Camenisch-Lysyanskaya (CL) signatures, and Boneh–Lynn–Shacham (BLS) signatures. 
* Key exchange: exchange methods enable two parties that have no prior knowledge of each other to jointly establish a shared secret key over an insecure channel. This key can then be used to encrypt subsequent communications using a symmetric key cipher. Diffie–Hellman is a common example. 
* Zero-Knowledge (ZK): Many ZK methods are used in cryptography incuding Fiat Shamir, Proof of knowledge of discrete logarithms, ZK Snarks, ZK Starks.
* Cryptographic accumulators: one way membership functions that answer a query as to whether a potential candidate is a member of a set without revealing the individual members of the set. Similar to a one-way hash function, cryptographic accumulators generate a fixed-size digest representing an arbitrarily large set of values. Some further provide a fixed-size witness for any value of the set, which can be used together with the accumulated digest to verify its membership in the set.  
* Commitments
* Witness: The term has different applications in cryptography. In this paper a witness is a value used in a cryptographic accumulator. In bitcoin the unlocking signature is called the "witness data." 
* Quantum Computing and Cryptography: as quantum computing is developed it poses a threat to the difficulty of puzzles. For example Shor's algorithm for integer factorization on q	uantum computers makes it much easier to discover a number's prime factors.



## verifiable credentials in Sovrin
## Indy SDK


# Appendix

Interviews regarding data minimization, selective disclosure and progressive trust.

This section contains definitions we collected that we considered in the formation of our definition above. 

## Data Minimization
Definitions of data minimization that we considered in the formation of our definition above. 

* GDPR Rec.39; Art.5(1)(c) definition: “The personal data should be adequate, relevant and limited to what is necessary for the purposes for which they are processed. This requires, in particular, ensuring that the period for which the personal data are stored is limited to a strict minimum. Personal data should be processed only if the purpose of the processing could not reasonably be fulfilled by other means.”
* Reducing your overall footprint of data outside of your control. Can be accomplished by using selective disclosure. 
* Adequate, relevant and non-excessive.
* Reducing the amount of data you are sending in a payload to only the one is needed. That prevents leakage of confidential information.
* Providing people with the information they need without revealing non necessary info. If I need to prove if I am old enough without revealing an actual birthdate.
* Best practices – your should deeply inspect your use case and come to a conclusion as to what is the minimum data you need to accomplish your goal. Don’t be greedy. Data has proven to be toxic.
* Mathematical – finding a way to express the data that you wish as an equation related to the data you have.
* Minimizing the amount of data to achieve your goal or communicate what you need to.
* Designing systems to operate efficiently in order to maximize privacy.
* Choosing to only share the minimal amount of data about yourself or something during an interaction. 
* Trying to keep the amount of info that is being disclosed as limited as possible to the requirements of the vulnerability. The minimum is what is will lead them to move to action. 
* Always happens in a context: a relationship where the two parties are considering interacting in some way. Sending only the signals that I want to send and that are needed by the other party, hem to interact with me in a particular 
* The least amount of data needed for a system to function
* Collecting the least amount of date for the highest outcome. 
* Also known as minimal disclosure, data minimization is the principle of using the least amount of data to accomplish a transaction. This is incumbent on all three parties in an exchange. The holder should attempt to share the minimum. The issuer needs to create attributes designed for composition and minimal use, as opposed to monolithic credentials with all the data. The verifier needs to ask only for what they need. The motivation to minimize data is that unneeded data is potentially “toxic.” 

## Selective Disclosure

Definitions of selective disclosure that we considered in the formation of our definition above. 

* Ability to decide what info you give and how it can be used.
* Smart disclosure, allows to select what information to give based on logic. 
* Blind search. You can decide who gets to see what. 
* Means by which we achieve data minimization. Form of policies. Ability to mask attributes that you do not have to share.
* Relates to mathematical definition – the computational ability to reveal only parts of your data profile. 
* Act of communicating or revealing only what you intend to, and not any peripheric data
* Having granular control over the ways in which data is shared
* Is a pattern for user interfaces allowing people to choose what to share about them during an interaction
* Method for achieving data minimization where only certain signals are being shared and there is control of who it is being shared with. That control is never perfect. The communication channel matters.
* An entity having granular control on what’s revealed.
* The individual having the freedom to decide what to share, or the acquirer using data minimization approach requesting the minimum amount amount of data for the maximum impact

## Progressive Trust

Definitions of progressive trust that we considered in the formation of our definition above. Note that we included definitions of progressive trust and progressive disclosure as well. 

* Procedure for increasing revelation of relevant data as the communication proceeds. As we continue to communicate we decide to reveal more information. It becomes more generous as trust builds. 
* Being able to reveal more data as you need to given certain conditions
* Information is disclosed as needed when needed.
* You can choose to increase the amount of data you disclose over time as needed. 
* Taking as little vulnerability as possible at the beginning, then gaining information and becoming willing to take on additional vulnerability by revealing more information. 
* Trust is built through step by step interactions where we start making ourselves vulnerable in a very small way and we observe how this works out. Based on results we consider making ourselves further vulnerable or not. It is about increasing levels of familiarity and prediction making (I am better able to predict your behavior). 
* Releasing information as needed
* Escalation of the previous steps (data minimization, selective disclosure) in line with the value increasing. 
* Purpose binding is the auditable use of data, so I can audit the use of my data and determine that it was used for the purposes declared. Progressive trust is the feeling of assurance and safety that develops over time, based on a history of data used only for its bound purposes, and so based on this feeling a data holder will be ready to share more data or other data, if at some point in the relationship this other data is requested. 
* Trust is required when you depend on the actions of someone who you can't control. 

# References:
 * [Data Minimization and Selective Disclosure Repo] (https://github.com/w3c-ccg/data-minimization)
 * Camenisch, Lysyanskaya. [An Efficient System for Non-transferable Anonymous Credentials with Optional Anonymity Revocation] (http://www.cs.ru.nl/~jhh/pub/secsem/camenish2001idemix-clean.pdf)
 * 2010 Pfitzmann, Hansen. [A terminology for talking about privacy by data minimization: Anonymity, Unlinkability, Undetectability, Unobservability, Pseudonymity, and Identity Management] (https://www.researchgate.net/publication/234720523_A_terminology_for_talking_about_privacy_by_data_minimization_Anonymity_Unlinkability_Undetectability_Unobservability_Pseudonymity_and_Identity_Management)
 * 2013 Cooper, Tschofenig, Aboba, Peterson, Morris, Hansen, Smith, Janet. [RFC6973] (https://tools.ietf.org/html/rfc6973). The draft can also be helpful, "This document focuses on introducing terms used to describe privacy properties that support data minimization." 2012 Hansen, Tschofenig, Smith, Cooper. Privacy Terminology and Concepts. Network Working Group Internet-Draft Expires: September 13, 2012. https://tools.ietf.org/html/draft-iab-privacy-terminology-01
 * Redaction Signature Suite 2016, Draft Community Group Report 26 June 2017. Longley, Sporny. Link: https://w3c-dvcg.github.io/lds-redaction2016/ "This specification describes the Redaction Signature Suite created in 2016 for the Linked Data Signatures specification. It enables a sender to redact information in a message without invalidating the digital signature."

