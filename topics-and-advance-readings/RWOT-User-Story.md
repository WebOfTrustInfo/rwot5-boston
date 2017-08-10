# #RebootingWebOfTrust User Story & Tech Concept

##### By Christopher Allen — Copyright 2017 Licensed CC-BY

**Contributors:** Shannon Appelcline

### Who is Alice?

**Alice** is a first-generation citizen of a western country (United States, Britain, Germany), born of two immigrants from a country of significant repression (Iran, Cuba, North Korea) who are now permanent residents. Her parents were settled in a small city near the agricultural heart of the county (Midwestern United States, Midlands of Britain, Saxony of Germany) where they have become successful small business owners.

As a child **Alice** was told stories of the abuses her parents suffered in their country of origin, a place they cannot return to. She knows some cousins and other family members in other countries who have told similar stories, but mostly through the internet or through traveling to the various countries that her extended family has settled in.

Both **Alice** and her parents have experienced some unkind words and minor discrimination in their newly adopted country, but largely the benefits of being in a modern western country overwhelm any disadvantages. The parents have found others to practice their religion with; **Alice** respects this, but in general is more secular.

**Alice** has recently graduated with a computer science degree, and has pleased her parents by settling nearby, working for a small regional bank. The bank is quite conservative and has a “no social media” policy at work. This rule is regularly broken, but there have been some object lessons, especially for those who stand out as non-conformists.

However, the winds of populism are blowing. **Alice** has personally heard more slurs lately and has seen more covered the media. Many local political parties of rising significance have publicly targeted her ethnicity and her parents' religion. Added to the stories of repression in her parent’s birth country and even greater stories of conflict reported by distant family members, **Alice** has some legitimate fear.

**Alice**, like most millennials, doesn’t wish to leave her head in the sand; she wishes to take a more active role in making a better world. However, she knows if she stands out from the crowd, then her activism may affect not only her, but also her parents and even her extended family abroad. Increasingly **Alice** has been more careful: self-censoring social media, using end-to-end encryption software to talk to her family abroad, etc.

### Bob may have an opportunity for Alice

**Bob**, a mainstream citizen of his western country, is also worried about the rising tide of populism in his own country and of extremism in other countries. Raised by a middle-class family he has travelled widely as a young adult and was supported by his parents when he joined a non-profit organization as an employee. **Bob** is not a programmer, but he is an active user of social media and other internet technology and he has some ideas about how his non-profit could use mobile applications to serve their advocacy. He shares his ideas out in the world in a public forum.

**Alice** reads this request, and has the skills to help **Bob** to make a a mobile applications. However, she has a dilemma: she wishes to introduce herself and present credentials that she is qualified for the work, but wants to remain pseudo-anonymous. She has heard of other professional women who have been public about work and have been heavily criticized or even doxxed (such as in gamergate), and she doesn’t want to risk her job or her extended family if she is revealed to be helping **Bob**. She also doesn’t have a reputation in the developer community as a mobile programmer. Finally, she has limited time to be able to help and so has to be focused and careful about what she can offer.

### Alice establishes a pseudo-anonymous identity

So first **Alice** establishes a DID (Decentralized Identifier) and a self-signed DDO (DID Data Object). Now she needs proof of her mobile compentency.

**Alice** has a professional colleague and friend **Donna** with a public persona that is not anonymous, who indirectly knows **Bob** through yet another colleague. That is, **Bob** and **Donna** share a trust network but are connected by multiple degrees of separation.

**Donna** issues a Verifiable Claim that she "knows" **Alice** and she is willing to attest to her competence in mobile development. She then gives a signed copy of the claim back to **Alice**. Alice countersigns this claim and adds it to her DDO. (This is something unique to the very self-sovereign BTCR method, which may not apply to other methods.)

**Alice** then sends a response to **Bob's** request for programming assistance, along with the claim issued by **Donna**.

### How can Bob learn to trust Alice?

Now we dive into some mechanics of how the the did:btcr method of creating pseudo-anonymous identies operates. (Different DID methods will function differently.)

**Bob** receives an offer based his request from **Alice** (possibly itself a self-signed claim), along with the claim issued by **Donna**. The first thing his software does is do an INTEGRITY CHECK of **Donna's** claim itself. Is it properly formed? Has it expired? Is it properly signed by the issuer? Is it properly countersigned by the subject? If it fails any of these INTEGRITY CHECKS, **Bob** will not even know about it, and the whole message and its claims will be rejected.

The next thing that **Bob's** software might do is INSPECT INTO the DID numbers found in **Donna** claim. This will typically be automatic, but if **Bob** is hyper-concerned about internet traffic correlation (e.g., if he were a vulnerable citizen advocating against their nation-state) it may require a human to decide if they wish to proceed further. But **Bob** is an EU citizen and feels sufficiently protected, so his software is set to INSPECT INTO claims he receives automatically.

The first DID is **Donna's**. His software INSPECTS INTO the Bitcoin Blockchain for the appropriate transaction, and then looks at the first TXOUT of that transaction to see if it has been spent. In this case, it has, so this transaction cannot be VALIDATED. However, the claim has not totally failed quite yet, so the software now goes forward to that new transaction (the "tip" of the DID chain).

The software INSPECTS INTO this transaction's first TXOUT and it is not spent *and* there is a properly formatted op_return pointing to a DDO, which reside's on **Donna's** github account. The software now INSPECTS INTO and finds the DDO.

Now the the software does an INTEGRITY CHECK on the DDO, and if it is successful, then it VALIDATES the DDO by comparing it to the Control Key that was found in the signature that was used to send the transaction to the Bitcoin Blockchain, which was in turn revealed by the INSPECTION CHECK. If they match, both the DID and the DDO are now VALIDATED.

However, the claim itself was not signed by the Control Key so it is not VALIDATED yet. So the software INSPECTS INTO the DDO, and finds another key (either by looking through all the appropriately listed keys, or possibly because of a hint added in the claim). If the signature on the claim matches, now the claim issuer is VALIDATED.

However, the claim makes a statement to yet other DID, so it not yet VERIFIED, only VALID. The software must now do the same set of operations on **Alice's** DID to INSPECT INTO her DID and determine if it too can be VALIDATED.

Finally, if both the issuer's DID and subject's DID are VALID, (which includes the previous INTEGRITY CHECK of **Donna's** claim and **Alice's** countersignature of **Donna's** signature on the claim), then the claim is VERIFIED. (Thus it is called a "Verifiable Claim".)

However, this verified claim is not yet CONFIRMED. In order to be CONFIRMED,  **Bob's** Web-of-Trust CONFIRMATION criteria needs to be met. In this case, **Donna** is a third-degree connection, making **Alice** a fourth-degree connection. Over half of the world is a fourth-degree connection!

In this case, the software kicks out the verified claim for **Bob** to make a decision on: the claim and DIDs are INSPECTED, VALIDATED and VERIFIED, but not CONFIRMED. He decides to look further into what Donna is willing to share in her DID. In this case, **Donna** is vaguely known to him ("a familiar stranger") and her github repository is active and has a long history of mobile development. He looks now at what **Alice** shares in her DID; it is almost nothing, and contains no personal info. However, her response to his request for a proposal is interesting, and he hasn't found anyone yet, so he decides to CONFIRM and accept this claim to give her a trial.

If **Alice** fails her trial task, **Bob** will change his criteria to never waste any time on her again, or even possibly to never even bother to consider CONFIRMING any more of **Donna's** claims. This would be a locally-negative trust that is non-transitive to others in the self-sovereign scenarios required by the BTC method.

However, **Alice** doesn't fail her trial, and later **Bob** issues her a new verifiable claim saying that he also liked **Alice's** work, and maybe even issues a claim that countersigns **Donna's** original claim, showing appreciation for **Donna's** good recommendation.

---

### Alice and the Syrian Hacker Army

As our user story continues, **Alice** believes she may become targeted the Syrian Hacker Army as the author of an Android app that helps Syrian refugees communicate with the families back home and send them care packages through a random peer-to-peer network of people sharing their car trunk capacity: an Uber of small gifts, an AirBNB of trunk space.

**Alice** has been careful with her cryptographic keys, but she has prepared herself. The special set of public keys that are associated with this app are listed in her master DDO, and the app itself has a DID and DDO associated with it that she owns and controls. **Alice** has a password protected QR-code of the Owner Key for the current DID and DDO, but the Control Keys to update the DDO to a new transaction is with a friend in England locked on a hard drive.

Unfortunately, while traveling through Turkey, **Alice's** laptop is stolen. She is suspicious that someone might be targeting her.

The first thing she could do is just revoke and abandon the DID by simply spending the tip address. However, she doesn't have the Control Keys to enable that DID Control Key rotation transaction—they are in England. She does however hold the current Owner Key, so she can use that to update the DDO object that might be a possibly compromised key. She puts a "hold" notice in the DDO, and adds a timestamp to warn people to no longer rely on values in the current DID transaction until resolved, and wait for the new transaction on the tip.

If the hold expires without an update, or if the tip address is simply spent, all customers of her mobile app will be notified the next time they run the app that they may have a version that has be compromised, and they will be asked delete it before downloading it again from a trusted source.

Instead however, when she returns home to England she spends the tip, revoking the old Owner Key, and enrolling the old Control Key as the new Owner Key. A new address is posted which will be the next Control Key and the new "tip".

She now updates the DDO itself, signing it with the Owner Key just enrolled.  She has no evidence of any key compromise yet, but she has in her DDO claims issued using her revoked old Owner Key; these claims continue to be valid if they were dated before the time the key was stolen (though any claimants should be notified to request for updated claims if possible). As all of her claims are timestamps, there is no way for someone to fake a claim even if they break her old key, as the signature may be valid, but the timestamp is not.

In this case the customers of her app will continue to be able to use the old app (as the claims before the date of change can still be confirmed), but when the customers request an update they will be given the updated keys in the new app.

It is also possible that **Alice** could have set up her Control Key to be 2 of 4 multisig, with keys held by her trusted colleagues **Bob**, **Carol** and **Donna**. In this case, if two of them observed bad behavior in claims being issued by the old DID/DDO while she was traveling, or if she was able to call at least two of them, they could immediately rotate the Control Keys, and give her the new Control Key when she gets home. She maybe even already possesses the new Control Key, at it could have been generated by an xpub key her friends share. (However, this technique does require two transactions rather than one for every Control Key rotation.)

Finally, at some point in the future **Alice** passes this mobile project on to another team to develop, and she gracefully "retires" the DID/DDO pair with a gentle revocation and no new possible Control Key. However, all of her non-expiring claims are still valid: she didn't issue many, but a few are important and they need to remain.

---

Our use case will continue showing how Alice is able to demonstrate and share a positive reputation for her quality work. How **Carol** is able to use **Alice’s** software to protect herself from harm in a third-world country. How **Ted** is able to review **Bob’s** ideas and **Alice’s** work, and offer some funding to help both. How **Alice** is able to increase her reputation in her anonymously developed software to the point where she is offered a job at **Ted’s** company that pays more than her job at a conservative bank. How **Alice** is able to selectively revoke parts of her anonymity to establish her personal reputation her peers and selective colleagues, without at any time putting **Carol** and her other advocacy clients at risk.

**(HISTORY:** *The initial user story was originally written up as an [issue](https://github.com/w3c/vc-use-cases/issues/31) in the W3Cs Verifiable Claims Use Cases repo, with a goal of using it to create a formal use case for new pseudo-anonymous web of trust. Alice's story continues, along with some web of trust concepts and some proposed technical details , in [issue](https://github.com/WebOfTrustInfo/btcr-hackathon/issues/33) developed as part of the [DID:BTCR Hackathon](https://github.com/WebOfTrustInfo/btcr-hackathon). This version is currently being further drafted as a [Topic and Advance Reading](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/tree/master/topics-and-advance-readings) for the Fifth [#RebootingWebOfTrust](http://www.weboftrust.info/) in Boston on October 3-5, 2017 ([register here](https://www.eventbrite.com/e/rebootingweboftrust-design-workshop-v-fall-2017-in-boston-area-usa-tickets-34984665075)). Any comments on this version please use post in these [issues](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/issues).* **)**
