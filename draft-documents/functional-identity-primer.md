# A Primer on Functional Identity
---
By Joe Andrieu, Legendary Requirements [joe@legreq.com](mailto:joe@legreq.com) 

There are many ways to approach identity. For the Rebooting Web of Trust, we prefer a **functional approach** to focus conversations on how identity works and how we use it.

The varied facets of identity are so rich that we each bring our own **hot buttons** and **agendas** to any discussion. Some people engage from a **philosophical** perspective, others **cultural**. Some dive into **political** issues and others get **meta-physical** and **spiritual**. These different perspectives are valid views of identity’s impact on our lives. More than valid. **__Vital__**. They help answer the question of “Why?” Why identity matters, why we should care. Unfortunately, they also inflame **passions**. We sometimes talk past each other to make points that have minimal relevance for others, leaving people frustrated and unheard.

As **engineers** and **system designers**, we’re concerned with **how things work**. We want to fix what’s broken and build new things. To do that, we want to discuss how things function. With identity, this functional perspective sidesteps the inflammatory rabbit holes, without dismissing them. Functional Identity lets us investigate **the HOW** without prejudice **to WHY**, viewing identity systems based on how they work and then, in turn, how they affect individuals and society.

# A Functional Definition
> Identity is how we keep track of people and things and, in turn, how they keep track of us.

**That’s it**. We learn people’s names, we observe them and hear gossip and consume media. We then apply our sense of who they are to our dealings with them. Others do the same in return.

For many, this simple definition is **provocative**. It triggers thoughts of **Big Brother** and the **surveillance** state. It brings up ideas about embedded chips and tattooed serial numbers. It conjures fears of government or corporations constantly tracking what we do.

Which is ok, because, in fact, those are the most **feared abuses** of identity. It’s important to realize when we talk about identity that we are always talking about how we keep track of people. 

There are also a number of wonderful uses of identity. The joy of **a child** asking for “Momma” or **a lover** calling out your name. The pride in your name on a diploma. The simple benefit of seeing another’s name tag at a workshop and better remembering that fascinating conversation. Identity enables so much good stuff because it **helps** us keep track of people and things. 

The functional approach reaches **beyond digital** systems to understand how identity works throughout society. Our identity is bigger than our digital selves. Our identities existed before and continue to exist independent of any digital representation. Digital identities are simply **tools** which help organizations and individuals manage real-world identity. In the simplest terms, digital identities help keep track of people digitally. 

Unfortunately, digital systems can **unwittingly compromise** real-world identity. Sometimes this occurs because digital identity systems neglect to consider external effects. Other times, it happens with systems that didn’t even realize they were dealing with identity-related personal information. A functional perspective allows engineers to see **beyond** static attributes and traditional notions of “Personally Identifiable Information” to better understand how engineering choices can impact identity, even outside their systems.

With a better understanding of how identity functions, we will be able to build systems that **enhance** privacy and human dignity, while **improving** identity assurance and security. 

# Identity Systems
An identity system is a collection of tools and techniques used to keep track of people and things.

As individuals, we do this **naturally**, in our minds. We name things, then use names and distinguishing features to remember what we learn. We treat people differently based on their identity: treating our friends and family differently from strangers and known threats.

Organizations create processes, software, and services to **achieve** similar ends. These identity systems are best understood in terms of how they function, which is the same as how identity has worked since the dawn of **civilization**. 

# Terminology
In the diagrams below, the blue boxes are nouns and the red ovals are verbs – the building blocks for describing identity systems.

We start with the simplest identity system, using three nouns and a verb:

<img alt="Subjects, Identifiers, Attributes, and Correlate" src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/master/topics-and-advance-readings/functional-identity-primer-diagrams/sub.id.attr.corr.svg" width="450px">

* **Subjects** are entities—people or things—under consideration.
* **Identifiers** are labels which refer to entities. They are used to keep track of what we know about those entities.
* **Attributes** are what we know about people and things. They describe the state, appearance, or other qualities of an entity.
* **Correlate** means to associate attributes with particular entities, to associate what we know about someone with either an identifier in the system or a subject in question.
 
Identity systems **correlate** **subjects** with **attributes** in two ways. First, attributes are associated with **identifiers** referring to specific **subjects**, thus building a body of knowledge. Then, when we recognize a subject, we associate them with one or more identifiers, and in doing so, associate them with everything we know about those identifiers. 

These terms apply equally to things other than people, such as organizations, groups, or places. We correlate new attributes with identifiers and vice-versa as we learn about subjects. When we recognize a person or thing we can apply everything we have learned about them. In digital systems, this set of related attributes is sometimes referred to as a digital identity or profile.

# Input and Effect

We learn or acquire identity information over time, then apply what we’ve learned to various interactions, usually elsewhere. 

<img alt="Acquire and Apply" src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/master/topics-and-advance-readings/functional-identity-primer-diagrams/acq.apply.svg" width="300px" >
  
* **Acquire** means to gather identity information for use by the system.
* **Apply** means to use identity information to affect change outside the identity system, typically to moderate an interaction of the subject with a related system. 
 
Identity information might be **acquired** by observation or by importing from elsewhere. We may learn about someone by watching them, or we may learn through references, rumors, and reputation. Identity systems acquire new information throughout their operational life, just as we continue to learn about people throughout our lives.

Once acquired, identity information must be **applied** in a specific situation to have impact. If we know something about someone and that information never influences our behavior and is never shared, it doesn’t affect the world. The way that identity information is applied tells us how an identity system affects our lives.

For example, a website might apply the email associated with my account to allow me to reset my password or it may send me unwanted advertisements. The U.S. Transportation Security Administration (TSA) applies the information on its no-fly list to prevent those identified as potential threats from flying.
 
# Making New Ideas

We gain new insights by considering both existing identity information and previously unrelated observations. Identity is more than just what we know about people and apply to our interactions. It’s also how we make judgments based on what we know, gaining insights into character, capabilities, and proclivities. 
 
<img alt="Raw data, Derived Attributes, and Reason" src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/master/topics-and-advance-readings/functional-identity-primer-diagrams/raw.der.reason.svg" width="300px">

* **Raw data** are data which may or may not contain information relatable to any particular person or thing. 
* **Derived attributes** are conclusions reached by reasoning over identity information. They are what we learn when we consider what we know about people and things.
* **Reason** means to evaluate existing identity information to generate new derived attributes. 
 
**Derived attributes** are created by **reasoning** using **raw data** and known attributes. By applying reasoning to existing observations and related knowledge, we can gain insights that neither the subject nor the original author anticipated. Raw data such as search history, web browsing, and the time & location information captured by our phones, may contain identity-related information, even when that was neither the purpose nor the intention at the time of capture. 

We also reason using known attributes to derive new ones. For example, we calculate a person’s age based on the birthdate on their driver’s license to determine if they are old enough to drink legally. Credit companies evaluate recent income, past transactions, and projections of future income to set interest rates and make loan approvals. We remember how people treat us and alter our behavior in future interactions. If someone repeatedly breaks their word, we may stop depending on them.  

# Securing Identity Information

We go to great lengths to keep identity information secure.

<img alt="Secure" src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/master/topics-and-advance-readings/functional-identity-primer-diagrams/secure.svg" width="150px">

* **Secure** means to restrict the creation and flow of identity information to the right people at the right time.

Sometimes we keep **secrets** to prevent information from reaching certain people. We do this with tools like encryption, access control, and minimal disclosure. Legal **agreements** between people, businesses, institutions, and governments specify **appropriate use** of certain information while laws, regulations, and the courts allow governments and institutions to **oversee**, monitor, and intervene in the capture and use of identity information. How identity systems secure certain information, and not others, defines how they preserve and respect **privacy**. 

The right to keep private information private is often referred to as the **right** of privacy.
Many people feel their privacy is **threatened** because so much information is shared over the Internet, in our workplaces, and through our devices. Information we share in different contexts (business, family, community, etc.) can **leak** unexpectedly and undesirably into other contexts.

It is difficult as individuals to understand of all the ways we are publicly or privately tracked. Information is **shared** on social media, tracked in Internet searches, monitored when using navigation software, and captured as we use our phones. The sheer magnitude and complexity of the information tracked and used means the average person is essentially **incapable** of making informed decisions to consent to appropriate use. Some people **give up**, divulging personal information without regard to consequences. Others **opt-out**, participating as little as possible in our digitally connected world. 

Identity matters because the myriad ways we are tracked can **impact** our lives. It pays to **understand** the options we have as engineers, and as individuals, for protecting ourselves, our families, and our businesses. 

# Bridging the Gap

The nouns and verbs above are grounded in the world of technology and may be unfamiliar for the average individual. More conversational synonyms are presented in the tables below. Use the most appropriate terms for your audience. 

# People, Places and Things
This is the point of identity: those people, places, and things we recognize. 

| Technologists | Laypeople | Common Meaning                                     |
|---------------|-----------|----------------------------------------------------|
| Subject       | Person    | Someone under consideration. The focus of inquiry. |

# Identity Information
These are the abstract nouns of identity, the informational assets created and used by identity systems.

| Technologists | Laypeople | Common Meaning                                     |
|---------------|-----------|----------------------------------------------------|
| Identifiers   | Names     | Refers to entities. Used to keep track of people and things.|
| Attributes    | Statements | What we know about people and things. They describe the state, appearance, or other qualities of an entity. |
| Raw data      | Observations | Data which may or may not contain correlatable information. |
| Derived attributes | Beliefs | Conclusions reached by reasoning over identity information. These are what we learn when we consider what we know about people and things. |

# Identity Actions
These are the verbs of identity. These are the actions taken by identity systems working with identity information.

| Technologists | Laypeople | Common Meaning                                     |
|---------------|-----------|----------------------------------------------------|
| Acquire       | Collect   | Intake or generate identity information for use by the system. |
| Correlate     | Relate    | Associate attributes or observations with particular entities. We associate what we know about someone with either an identifier in the system or with a subject in question.|
| Reason        | Reason     | Evaluate existing identity information to generate new beliefs, expressed in attributes, captured in statements. |
| Apply         | Apply      | Use identity information in a system, typically to moderate interactions with known entities.|
| Secure        |Protect     |Restrict the creation and flow of identity information to the right people at the right time.


### For technologists
<img alt="Technologists' language: Subjects, Identifiers, Attributes, Raw data, Derived attributes, Acquire, Correlate, Reason, Apply, Secure" src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/master/topics-and-advance-readings/functional-identity-primer-diagrams/technologist.svg" width="750px">

We assign **identifiers** to **subjects**. We collect **raw data** and correlate **attributes** to the **subjects** we track. We **reason** over raw data and attributes, to **derive** new **attributes**. We then **apply** this information to current and future interactions with subjects. We **secure** identity information to keep secrets and preserve privacy.
 
### For laypeople
<img alt="Regular language: People, Names, Statements, Observations, Beliefs, Collect, Relate, Reason, Apply, Protect" src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/master/topics-and-advance-readings/functional-identity-primer-diagrams/layperson.svg" width="750px">

We give **names** to **people**. We **collect** **observations** and record **statements** relating those observations to people we know. We **reason** over these observations, statements, and **beliefs** to generate new beliefs. We then **apply** what we know and believe when dealing with those we recognize. We **protect** identity information to keep secrets and preserve privacy.

This is the **vocabulary** of Functional Identity, a way to discuss identity in terms of functionality: how it works and what it does for us. This is the language of identity for the Rebooting Web of Trust.

# Why?

Engineers, entrepreneurs, and financiers have asked “Why are we spending so much time with a definition of identity? Why not just build something and fix it if it is broken?” The vital, simple reason is **human dignity**.

When we build interconnected systems without a core understanding of identity, we risk **inadvertently** compromising human dignity. We risk **accidentally** building systems that deny self-expression, place individuals in harm’s way, and unintentionally oppress those most in need of self-determination.

There are times when the needs of **security** outweigh the need for human dignity. Fine. It’s the job of our **political** systems—local, national, and international—to minimize abuse and to establish boundaries and practices that respect basic human rights.

But when engineers **unwittingly** compromise the ability of individuals to self-express their identity, when we expose personal information in unexpected ways, when our systems deny basic services because of a flawed understanding of identity, these are **avoidable tragedies**. What might seem a minor technicality in one conversation could lead to the loss of privacy, liberty, or even life for an individual whose identity is **unintentionally compromised**. 

That’s why it pays to understand identity, so the systems we build intentionally enable human dignity instead of accidentally destroy it.

# Summary

Functional Identity focuses on **how identity works**. At the Rebooting Web of Trust, we ground our work in the functional notion of identity and **avoid** the psychological, cultural, political, and philosophical. These notions are important, but they can also **distract** us from understanding the **technical choices** involved in building and using identity in today’s networked world.

This functional notion of identity began with a conversation at the **[Internet Identity Workshop](http://iiw.idcommons.net)** in May of 2016, followed by conversations at **[ID2020](http://id2020summit.org)** and the second Rebooting Web of Trust workshop that summer, resulting in the paper [Identity Crisis](https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/final-documents/identity-crisis.pdf). It continued in subsequent meetings in all three venues, and in two articles published by the People Centered Internet [Speaking of Identity](https://peoplecentered.net/2017/06/11/speaking-of-identity/) and [How Identity Can Enable A People-Centered Internet](https://peoplecentered.net/2017/07/26/how-identity-can-enable-a-people-centered-internet/). 

This primer represents a **current take** on that conversation, geared to help Rebooting Web of Trust participants **communicate** more clearly and **collaborate** more effectively. We encourage your feedback and look forward to continuing the conversation.
