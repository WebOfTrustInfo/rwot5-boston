##### Author: Kyle Den Hartog
##### Title: Framework for the Comparison of Identity Systems
##### Date: 2017-05-12

# Abstract:
This paper intends to address the different types of identity systems and develop a method of comparing the identity systems. It is the goal of this paper to first identify the types of identity systems that have been created in the past as well as newly emerging identity systems. These identity systems can be used in many ways, but they often have many similarities allowing for the comparison of these identity systems. Outlined in this paper is a framework to make these comparisons by relying upon 4 categories that are apart of identity systems. They are verifiability, system architecture, accessibility, and security.

# Introduction:
Throughout history, identity has come to mean many different things. An identity can be representative of a trait or many traits with which a person identifies with. It can also take on a third-party view in which other people choose traits to describe and identify another person other than themselves. In general, we will describe an identity as a collection of traits or properties used to describe a human or a group of humans to uniquely categorize a subset of a population. It should also be noted that an identity can also be used to describe things, however this paper will focus on human identities to build a framework for analyzing human identity systems.

As new technologies have developed the methods of used to build systems of verifiable identity have changed. One of the earliest systems that predates National ID card systems, was an implementation put in place by Napoleon to streamline the capabilities of a centralized government. <sub>1</sub> As centralized governments progressed in their needs to identify their citizens they improved national ID systems eventually moving to a national ID card system. The ottoman empire was one of earliest adopters of a national ID card system launching it in 1844. <sub>1</sub> However, it wasn’t until post World War II era that national ID card systems became a commonality between many countries.<sub>1</sub> Through the modernization of the computer, internet, and new sensors, we have seen many new systems put in place.

With the usage of these new technologies, a different realm of identity exists built upon digital platforms. With these digital identities, humans can now maintain various pseudonymous identities. Pseudonymous identities such as email accounts, social media accounts, and even the emergence of fully anonymous identities have surged in recent years. One of the key uses today for identity systems, is to authenticate users through a variety of means. The three main ones are “What you know” (Passwords and Pins), “What you have” (Bluetooth key, NFC key, cell phones), and “what you are” (biometrics like fingerprints).

Within the space of digital identities, we have seen organizational structures change. The main changes that have occurred is the shift away from centralized identity system architectures. Identity systems have shifted towards federated identity systems, delegated identity systems, and even some self-sovereign identity systems. <sub>5</sub>

The key difference between these identity systems is who creates the identity and how the identity is validated. Traditionally with central identity systems, governments have been the ones to create and validate the identity, creating a low necessity for external verification. When federated identity systems emerged, digital identities begun to place more emphasis on cryptography as a means of validation relying upon protocols agreed upon by many parties. The primary purpose federated identity systems emerged was to reduce the number of identities a user may need when using the internet. With these new Federated identity systems, users could maintain fewer accounts while gaining access to more services on the internet.

Similarly, delegated identity systems have emerged in recent years which operate very similarly to how federated identities are validated through cryptographic logic. The key difference between federated identities and delegated identities is that identities in a delegated system are created by a single party who then validates the identity for other service access. <sub>2</sub> This in turn pushes back towards centralization architecture of identity systems, which is much different from self-sovereign identities.

With self-sovereign identity systems, a paradigm shift has occurred in how the identity system creates, validates, and verifies an identity. In a self-sovereign identity system, users now no longer need another party to create an identity, but rather create the identity themselves. <sub>7</sub> Another significant change is in the way a user’s identity is accepted. In all the other types of identity systems, identities we’re indirectly validated because they were created by a trusted 3rd party. However, in self-sovereign identity systems, identities are validated and trusted each time the identity is used. This happens because each time the identity is used it is verified by a new party among the system, which over time validates and gives more credibility to the identity. As such, self-sovereign identity systems create a system where trust is built up over time rather than being instantly granted.

One of the more concerning issues that has arisen with digital identities is the issue of Sybil attacks in identity systems.<sub>4</sub> Sybil attacks occur because it is difficult to verify that a user has a single digital identity without a method of physical verification. This however is not always possible, which is where new projects have emerged to resolve this issue using video chats. <sub>6</sub>

# Benefits:
In this paper, there are 4 main categories that we use to compare identity systems.  They are verifiability, system architecture, accessibility, and security. Using these categories, the focus is to establish a framework that can be used to compare identity systems in a standardized way. These categories were selected as way to cover a broad basis of properties that emerged from many different identity systems.

Throughout this paper, a scale is used to identify the ability of a system to meet the requirements. The scale will be as follows, high will be for an identity system that meets the criteria entirely. It is intended to be representative of an ideal identity system. Medium will be used to represent an identity system that meets some of these needs of an identity system or meets all the criteria, but creates friction in doing so. Lastly, we will use a low to indicate that the system does not meet the criteria in any capacity. This will allow for a broader range of identity systems to be analyzed.

## Verifiability
Verifiability serves in important role in an identity system, particularly digital identity systems. Verification is one of the integral features of an identity system and must be quick, efficient, and decisive in its ability to verify a legitimate identity versus a falsified identity. The two subcategories of verifiability is Trusted and Verification method.

*Trusted source:*
The purpose in having a trusted source in an identity system is important to being able to guarantee the validity of the system. If falsified identities can be created, it degrades the integrity of all other identities in the system. As such the criteria for trusted source is as follows.
* High: A user can independently determine its ability to trust another user
* Medium: A user requires a trust link to verify another user
* Low: A user cannot trust another user in the system

The rationality of setting high as any node being able to independently verify another user is that it allows for the greatest level of ease as well as meeting the guarantee of verification. Medium is more representative of a centralized system which requires barriers of entry to verify another user. Last, a low is intended to be given to systems that have no trust and as such the identity system can be falsified.

*Verification method:*
The verification method criteria are intended to look specifically at how the verification of the data is conducted. This is important to be able to identify the level of ease a false identity would have in being able to pass as a legitimate identity. The ranks for verification methods are:
* High: Mathematical proof
* Medium: provides reasonable certainty of verification
* Low: Verification doesn’t provide certainty

The rationality of setting high as a mathematical proof is that the system provides a perfect guarantee of the verification of the identity. With a perfect guarantee of the identity we can be certain the user is legitimate if the source of the identity didn’t cheat the system. For medium, only reasonable certainty is needed to verify an identity of a system. Reasonable is subjective, so to better define reasonable, it shall be considered a system in which cheating the verification method requires an excessive amount of time to cheat once, or requires an excessive amount of resources to cheat the system once, or it is deemed highly economically inefficient to cheat the system once. The purpose in stating once is of importance because if it requires an excess once to cheat the system many times, the criteria of reasonable is not met. With Low, no verification is provided which makes the identity system weak in terms of its purpose.

## System Architecture:
System architecture addresses the ways in which the system is architected. This is an important factor in any system and can be the difference between a successful and a failed identity system.

*Organizational structures:*
Organizational structure is an important to be considered in an identity system because it allows for subsets of a population larger than a single user to emerge. As such an identity system benefits immensely from the formation of organizational structures, otherwise known as groups, within the system. The ranking for organization structures is:
* High: Organizational Structures are integrated into the system
* Medium: Organizational structures can be formed by application of the system, but not integrated in the system
* Low: Organizational structures cannot be formed by using this system

High is given to a system that directly integrates organization structures directly into the system and builds around them. Medium is intended to be used for systems which have strong identities, but must conduct the implementation outside of the identity system. A low should be given to a system which doesn’t allow organizational structures to form either through the system or outside of the system.

*Centralization:*
Centralization is a key feature of identity systems, more particularly digital identity systems which have utilized new structure formats. Centralization looks to address the structure of the identity system on a high level regarding the creation, and verification of identities. The rankings of centralization as a criterion is:
* High: Decentralized allowing anyone apart of the system
* Medium: Hierarchical with trusted parties used by the system
* Low: Centralized trusted parties used by the system

High has been given to a decentralized structure to allow for largest amount of control by the user of the identity. Medium has been given to identity systems that use hierarchy connecting trusted parties to establish trust in the identities of the system. Low has been given to systems that rely upon a central party to establish trust of the identities.

## Accessibility
With identity, it is important that the identity has some accessibility guarantees. If the system is not accessible then the identities it impacts the usage of the system. Accessibility places an emphasis on how the system is used as well as the ability for the user to establish their control of their identity.

*Independence:*
Independence of an identity system is important to best adapt to the users of the actual identities. A system that is more adaptable to the users will provide better availability of the identities allowing for the integration of the identities in a better manor. The rankings of independence are:
* High: Open source system changeable by system agreement
* Medium: business controlled and developed, but open source and changeable by system agreement
* Low: Business controlled and developed, proprietary system, licensed for use

The high ranking places an emphasis on an open source system that allows for the system to be changed by the users as well as focusing on system agreement. System agreement is important to be able to keep the usage of the system. With medium, there is a focus on business controlled systems. By having the system controlled by a business as opposed to controlled by the users, it creates a vector for the system to be hijacked or steered in a direction against the will of the users. Low was given to an identity system that focuses on the proprietary aspects of a business which limits the adoption of the system.

*Devices:*
The focus of this subcategory is to establish the easy of the system to be integrated quickly. A system that can be deployed and requires less barriers of entry will allow the system greater access to the identity system. As such it is important to consider what is necessary to use the system which is what this criterion is for. The rankings for devices is as follows:
* High: System provides all components necessary
* Medium: System relies upon common devices to implement
* Low: System requires users to purchase a new device to use the system

An identity system that provides all necessary components or requires no components other than what is inherent to a person should receive a high in this criterion. A medium should be given to a system that relies upon common devices. This is a medium because it cannot guarantee that the system is adoptable by all people which could pose limitations for accessibility. A low should be given to a system which requires a new device to use the system. This creates a significant barrier on accessibility to the system.

*Deployability:*
If an identity system is too difficult to deploy or requires more work than current systems, it likely will not see a mass adoption. The accessibility of an identity system relies heavily on its ability to be deployed easily and efficiently by any user who wants to build on top of the identity system. The rankings for the criterion of deployability are:
* High: Easy to adopt onto all current systems without changes being made
* Medium: Requires some changes to current infrastructure to become widely adopted
* Low: Requires “scrap and replacing” to adopt

A high should be given to systems that can be easily used and adopted by any user who wishes to utilize the identity system. This grants the highest level of accessibility to the system. It is important to consider whether changes must be made to current infrastructure in order to adopt the system. If some changes must be made the system should be given a medium ranking. Last, a low should be given if the system requires a “scrap and replace” approach to implement the system. This will likely be costly pushing users away from the system and limiting its accessibility.

*Account recovery:*
Account recovery is important to the accessibility of a system because it is what allows for persistence of an identity if a user makes a mistake. As such the rankings for account recovery is as follows:
* High: Account recovery is easy and secure
* Medium: Account recovery is difficult and secure
* Low: Account recovery is impossible or unsecure

With account recovery, it is important to consider the tradeoff of convenience and security. A system that receives a high from this criterion should meet this tradeoff in an optimal fashion. A system that is not an optimal tradeoff between security and usability, and is still secure should receive a medium ranking. Last, a system that either does not allow for account recovery or is unsecure in the ability to recover an account should be considered low. A system with a low criterion can have a significant impact on accessibility to users.

*Portability:*
Portability looks at the accessibility of a system to be used in both physical applications and digital applications. As such the ranking for portability is as follows:
* High: Able to be integrated with both physical and digital applications without additional requirements (nothing needed)
* Medium: Able to be integrated with both physical and digital applications, but has additional requirements (devices, cards carried)
* Low: Able to integrate with only digital or physical applications, but not both

The purpose in ranking in this manor is to grant the greatest level of accessibility and as a system reduces how an identity system can be used in terms of physical and digital applications it reduces the accessibility of the identity system.

*Identity removal:*
Identity removal is important for the purposes of privacy of an identity system. Privacy provides some important properties, so a quality identity system must have a method to reconcile the removal of an identity. The levels of identity removal are:
* High: A user may delete their identity from the system at anytime
* Medium: A user may delete their identity with approval of a 3rd party
* Low: A user is unable to delete an identity from the system

The high ranking should be given to an identity system that allows for the easy removal of an identity from the system allowing for the user to have full control of the identity. Medium is a slight deviation from high in that to remove an identity from the system a user must gain 3rd party approval. This still allows for the user to delete an identity, however the 3rd party provides vectors for inefficiency and can potentially be abused. Last, low should be given to a system which does not allow the removal of an identity. This poses a threat to privacy.

## Security
Security is an important part of an identity system as it maintains the trust in the system. A system that is secure is a system that can be relied upon. The criteria of security are integrity, confidentiality, theft prevention, data revocation, and anonymity. In this category, there is a large focus on the system’s security as well as the control of the user data.

*Integrity:*
A system that provides integrity guarantees is important because it shows that the data that is being transacted is reliable data. This is an important factor in being able to trust the system, and be certain of its security as well. The rankings for integrity are:
* High: Data history is immutable and all changes are recorded
* Medium: Data is maintained by a trusted source with proper security controls
* Low: Data has no integrity guarantees

Through the integrity of this system a user will have full control of the data, but it can be verified that the data is kept in the state that it was intended. High ranking is intended to hold this by representing a system with a high level of data integrity because the history can be seen of when the data was created and changed. A medium ranking is given when a trusted source maintains the data securely. By relying upon a 3rd party it becomes possible that the data could be manipulated reducing the integrity of the data. Last, a low score is given to a system which disregards the integrity of the data of the identities.

*Confidentiality:*
Confidentiality is also an important point of security to consider. This focuses on user control of data. The rankings of confidentiality are:
* High: Guaranteed protection through mathematical proof
* Medium: Computationally unlikely to be broken
* Low: Computationally likely to be broken

A high ranking should be given to a system that provides mathematical proof that the system and its data is secure. This provides the strongest guarantees for the security of the system. A medium ranking should be given to identity systems that are computationally secure, but are not considered perfectly secure. Last, a low ranking should be given to an identity system which provides either no guarantees of confidentiality or utilizes deprecated processes that are easily broken.

*Theft prevention:*
Identity theft is important to address with an identity system. An identity system that is not secure to identity theft reduces the trust in the system as well as causes issues of concern for many other categories of this framework. The ranks for identity theft prevention are:
* High: not possible
* Medium: Difficult with little prevalence
* Low: Easy and highly prevalent

A system which can guarantee an identity cannot be miss represented or stolen will receive a ranking of high. A ranking of medium should be given to a system which allows for little prevalence of identity theft and is difficult to conduct. To meet the tolerance level should be very small (> 1% of the system) and anything with a greater amount of prevalence should be given a low ranking.

*Data revocation:*
Data revocation is important to the accessibility of an identity system because it places emphasis on the system’s ability to remain under control of the user. If the data of a user can be stolen, or accessed in a way that the user did not intend it could impact the security of the identity severely. The rankings for data revocation are:
* High: Data access can be shared and unshared by the identity holder
* Medium: Data access is shareable, but not revocable
* Low: All data is public, therefore irrevocable

A system which grants more data control should be ranked higher in this criterion. As such a high should be given to a system that allows a user to take away all access to data shared at any point in the past and doesn’t grant access to future data. A medium rank focuses on systems that allow some control of data, but do not allow for the system to remove data shared previously. A low should be given to a system that makes all data public as no control is given to the user.

*Anonymity:*
Anonymity is an important aspect to consider when it comes to privacy. A system that does not allow for privacy hurts the security of the system because it prevents users from remaining in control of their data as well as what they choose to share. The rankings for this criterion are:
* High: Allows for Anonymous users to join the system
* Medium: Anonymity is allowed, but the anonymous identity can be linked to the person
* Low: Anonymity is not allowed or is easily broken

The focus on high and medium is to address anonymity in terms of its difficulty to be broken. If a user’s anonymity cannot be broken at all it should be given a high ranking. However, if it can be broken in some capacity, but is difficult or requires a large amount of resources, a medium ranking should be given. A low is to indicate that the identity system places little to no emphasis on anonymity.

# Conclusion:
In conclusion, identity has grown throughout our society and the need for the different types of identity systems need to be assessed. This is important to place a focus on the ability to analyze and detect potential risks, threats, and problems of an identity system so that they can be improved upon. It is also important to consider that with so many teams working to build better identity systems, so it is important to compare these various systems.

# Sources:
1 Madsen, Paul, ed. "Liberty ID-WSF People Service – Federated Social Identity." LIBERTY ALLIANCE PROJECT WHITE PAPER (n.d.): n. pag. 05 Dec. 2005. Web. 08 Apr. 2017. <http://www.projectliberty.org/liberty/content/download/387/2720/file/Liberty_Federated_Social_Identity.pdf>.

2 Shirky, Clay. "Delegated vs. Federated ID." Nothing to See Here. Pennsylvania State University, 15 Feb. 2010. Web. 08 Apr. 2017. <http://sites.psu.edu/ntsh/2010/02/15/delegated-vs-federated-id/>.

3 Jerzak, Connor T. "A Brief History of National ID Cards." FXB Center for Health & Human Rights | Harvard University. FXB Center for Health and Human Rights, 12 Nov. 2015. Web. 08 Apr. 2017.

4 Yu, Haifeng, Michael Kaminsky, Phillip B. Gibbons, and Abraham Flaxman. "SybilGuard: Defending Against Sybil Attacks via Social Networks." SIGCOMM (2006): n. pag. Web. 15 Apr. 2017. <http://www.math.cmu.edu/~adf/research/SybilGuard.pdf>.

5 Allen, Christopher. " The Path to Self-Sovereign Identity”. Life With Alacrity. N.p., 25 Apr. 2016. Web. 15 Apr. 2017. <http://www.lifewithalacrity.com/2016/04/the-path-to-self-soverereign-identity.html>.

6 "Anti-Sybil Protocol Using Virtual Pseudonym Parties." Proofofindividuality.online. N.p., n.d. Web. 18 Apr. 2017. <http://proofofindividuality.online/>.

7 Lundkvist, Christian, Rouven Heck, Joel Torstensson, Zac Mitton, and Michael Sena. "UPORT: A PLATFORM FOR SELF-SOVEREIGN IDENTITY." UPORT: A PLATFORM FOR SELF-SOVEREIGN IDENTITY (2017): n. pag. Uport.me. 21 Feb. 2017. Web. 18 Apr. 2017. <https://whitepaper.uport.me/uPort_whitepaper_DRAFT20170221.pdf>.

8 Mittal, Prateek, Matthew Wright, and Nikita Borisov. "Analyzing an Adaptive Reputation Metric for Anonymity Systems." HotSoS (2014): n. pag. Hatswitch.org. Web. 07 May 17. <http://hatswitch.org/~nikita/papers/anon-reputation-hotsos14.pdf>.

9 Shrier, David, Weige Wu, and Alex Pentland. "MIT: Blockchain and Infrastructure (Identity & Data Security, Part 3)." Transportation Infrastructure Security Utilizing Intelligent Transportation Systems (n.d.): 14-30. Getsmarter.com. MIT, 17 May 2016. Web. 07 May 2017. <https://www.getsmarter.com/career-advice/wp-content/uploads/2016/12/mit_blockchain_and_infrastructure_report.pdf>.

10 TSA. "Transportation Security Timeline." Transportation Security Administration. N.p., n.d. Web. 07 May 2017.

11 ID2020. N.p., n.d. Web. 07 May 2017. <http://id2020.org/home>.
