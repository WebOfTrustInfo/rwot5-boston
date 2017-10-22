# Linked Data Signatures Proclamation Chains

By Christopher Allan Webber and Mark S. Miller

## Overview

[Linked Data Signatures](https://w3c-dvcg.github.io/ld-signatures/) bring
a method of asserting integrity of linked data documents passed throughout
the web.  The [object capability model](https://en.wikipedia.org/wiki/Object-capability_model)
is a powerful system for ensuring the security of computing systems.
In this paper, we explore layering an object capability model on top
of Linked Data Signatures via chains of signed proclamations.
<sup id="fnr.proclamation-terminology">[fn:1](#proclamation-terminology)</sup>

The system we propose can work regardless of whether we are using
https identifiers or [DIDs](https://w3c-ccg.github.io/did-spec/).
Since DIDs work nicely with this system and add an additional layer of
decentralization we use them for the URIs of this system.

## Example scenario

Alice (A) has a direct capability to store files in a "Cloud Storage"
system (C).  She would like to share this capability with Bob, but she
is wary of Bob's fondness of storing high resolution video, so she
would like to add a constraint that he may only upload files that are
no larger than 50 megabytes at a time.  Bob is excited to take
advantage of this service because he has recently been playing with
Dummy Bot (D), which automatically uploads some photos now and then.
But Bob has heard mixed reviews of Dummy Bot and is worried that maybe
Dummy Bot will malfunction.  He has decided that a 30 day window is
good enough of a trial period to permit Dummy Bot to upload to the
storage system so he can determine whether to renew at some future
date.

The initial condition looks like so:

```
     .-.       .-.       .-.
    ( A )---->( B )---->( D )
     '-'       '-'       '-'
       \
        \
         \
          \    .-.
           '->( C )
               '-'
```

<!-- at object capability level, use message
     at crypto level, use envelope, proclamation, messenger -->

(A)lice has a file upload capability to the (C)loud storage system.
(A)lice also has a capability to send a message to (B)ob, and (B)ob
has a capability to send a message to (D)ummy Bot.

Each of these characters has an associated linked data document that
represents them within the system which make use of
[JSON-LD](https://json-ld.org/) and
[Linked Data Signatures](https://w3c-dvcg.github.io/ld-signatures/).

Here is Alice:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     // This is a DID, but it could as well be an https:// uri
     "id": "did:example:83f75926-51ba-4472-84ff-51f5e39ab9ab",
     // This object is a person named Alice
     "type": "Person",
     "name": "Alice",
     // Finally, a signature verification key Alice will be using
     // for her upload capability to the Cloud Storage system
     "publicKey": [{
       "id": "did:example:83f75926-51ba-4472-84ff-51f5e39ab9ab#key-1",
       "owner": "did:example:83f75926-51ba-4472-84ff-51f5e39ab9ab",
       "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n..."}]}
```

Here is Bob:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     "id": "did:example:ee568de7-2970-4925-ad09-c685ab367b66",
     "type": "Person",
     "name": "Bob",
     "publicKey": [{
       "id": "did:example:ee568de7-2970-4925-ad09-c685ab367b66#key-1",
       "owner": "did:example:ee568de7-2970-4925-ad09-c685ab367b66",
       "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n..."}]}
```

Here is Dummy Bot:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     "id": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4",
     "type": "Service",
     "name": "Dummy Bot",
     "publicKey": [{
       "id": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4#key-1",
       "owner": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4",
       "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n..."}]}
```

Finally, here is the Cloud Storage service:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     "id": "did:example:0b36c784-f9f4-4c1e-b76c-d821a4b32741",
     "type": "Service",
     "name": "Cloud Storage Pro",
     "publicKey": [{
       "id": "did:example:0b36c784-f9f4-4c1e-b76c-d821a4b32741#key-1",
       "owner": "did:example:0b36c784-f9f4-4c1e-b76c-d821a4b32741",
       "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n..."}]}
```

Alice's capability to send a message to Bob is encoded in a
proclamation.  Let's look at what that proclamation looks like:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     "id": "did:example:0b36c7844941b61b-c763-4617-94de-cf5c539041f1",
     "type": "Proclamation",
     
     // The subject is who the capability operates on (in this case,
     // the CloudStore object) and the method is what the capability does
     "subject": "did:example:0b36c784-f9f4-4c1e-b76c-d821a4b32741",
     "method": "StoreObject",

     // We are granting access specifically to one of Alice's keys
     "grantedKey": "did:example:83f75926-51ba-4472-84ff-51f5e39ab9ab#key-1",

     // No caveats on this capability... Alice has full access
     "caveat": [],

     // Finally we sign this object with one of the CloudStorage's keys
     "signature": {
        "type": "RsaSignature2016",
        "created": "2016-02-08T16:02:20Z",
        "creator": "did:example:0b36c784-f9f4-4c1e-b76c-d821a4b32741#key-1",
        "signatureValue": "IOmA4R7TfhkYTYW8...CBMq2/gi25s="}}
```

Now Alice wants to share this capability to Bob, but with a caveat
(also known as an "attenuation"): Bob can only upload 50 Megabyte
files at a time.

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     "id": "did:example:f7412b9a-854b-47ab-806b-3ac736cc7cda",
     "type": "Proclamation",
     
     // This new attenuated proclamation points to the prevoius one
     "parent": "did:example:0b36c7844941b61b-c763-4617-94de-cf5c539041f1",

     // Now we grant access to one of Bob's keys
     "grantedKey": "did:example:ee568de7-2970-4925-ad09-c685ab367b66#key-1",

     // This proclamation *does* have a caveat: each upload can only be
     // 50 Megabytes large.
     "caveat": [
       {"id": "did:example:f7412b9a-854b-47ab-806b-3ac736cc7cda#caveats/50-megs-only",
        "type": "RestrictUploadSize",
        // file limit here is in bytes, so 50 MB
        "limit": 52428800}],

     // Finally we sign this object with Alice's key
     "signature": {
        "type": "RsaSignature2016",
        "created": "2016-02-08T16:02:20Z",
        "creator": "did:example:83f75926-51ba-4472-84ff-51f5e39ab9ab#key-1",
        "signatureValue": "..."}}
```

We can now see in the diagram that Alice has created, and has access
to, this attenuated capability.

```
     .-.         .-.        .-.
    ( A )------>( B )----->( D )
     '-'\        '-'        '-'
       \ \
        \ \
         \ '--->(R1)
          \
           \
            \    .-.
             '->( C )
                 '-'
```

But Bob cannot use this capability until he receives it.  Alice
invokes her message sending capability between herself and Bob.

```
     .-.   __    .-.        .-.
    ( A )-[##\->( B )----->( D )
     '-'\ '--/   '-'        '-'
       \ \        |
        \ \       V
         \ '--->(R1)
          \       |
           \      V
            \    .-.
             '->( C )
                 '-'
```

Now Bob has access to upload 50MB or less files to the CloudStore.
But he would prefer that Dummy Bot do uploads for him... well, for a
month.  He'll see how it goes.  Luckily these capabilities are
composable, and so Dummy Bot can create an attenuated capability out of
the attenuated capability he already has!

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     "id": "did:example:d2c83c43-878a-4c01-984f-b2f57932ce5f",
     "type": "Proclamation",

     // Yet again, point up the chain...
     "parent": "did:example:f7412b9a-854b-47ab-806b-3ac736cc7cda",

     // Now we grant access to one of Dummy Bot's keys
     "grantedKey": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4#key-1",

     // We add a new caveat/attenuation: this one will expire 30 days
     // in the future
     "caveat": [
       {"id": "did:example:d2c83c43-878a-4c01-984f-b2f57932ce5f#caveats/expire-time",
        "type": "ExpireTime",
        "date": "2017-09-23T20:21:34Z"}],

     // Finally we sign this object with Bob's key
     "signature": {
        "type": "RsaSignature2016",
        "created": "2016-02-08T17:12:28Z",
        "creator": "did:example:ee568de7-2970-4925-ad09-c685ab367b66#key-1",
        "signatureValue": "..."}}
```

The capability graph now looks like so:

```
     .-.          .-.         .-.
    ( A )------->( B )------>( D )
     '-'\         '-'         '-'
       \ \         | \
        \ \        V  '--v
         \ '---->(R1)<--(R2)
          \        |
           \       V
            \     .-.
             '-->( C )
                  '-'
```

Bob invokes his message sending capability to send the new attenuated
capability to Dummy Bot:

```
     .-.          .-.    __     .-.
    ( A )------->( B )--[##\-->( D )
     '-'\         '-'   '--/    '-'
       \ \         | \           |
        \ \        V  '---v      |
         \ '---->(R1)<---(R2)<---'
          \        |
           \       V
            \     .-.
             '-->( C )
                  '-'
```

Now Dummy Bot has a capability to upload files to CloudStore, but only
files that are within 50 megabytes, and only for the next month. This
is possible because Dummy Bot is authorized on the final proclamation,
but the proclamation "chains upward" including both the immediate
restriction/caveat within R2 on time but also the restriction/caveat
in R1 on space!

```
        .---------.       .---------.
        V         |       V         |
    __________    |   __________    |   __________ 
   (        (_)   |  (        (_)   |  (        (_)
    '        \    '-  '        \    '-  '        \ 
     ) CRT1   )        ) CRT2   )        ) CRT3   )
    '        ;        '        ;        '        ; 
   (________(_)      (________(_)      (________(_)
```

Soon Dummy Bot takes a picture and uploads it:

```
     .-.          .-.                 .-.
    ( A )------->( B )-------------->( D )
     '-'\         '-'                 '-'
       \ \         | \_______          |
        \ \        V    __   V     __  |
         \ '---->(R1)<-/##]-(R2)<-/##]-'
          \        |_  \--'       \--'
           \      |##|
            \      \/
             \     |
              \    V
               \  .-.
                >( C )
                  '-'
```

This is done through an `Invocation` on the proclamation, along with
additional parameters in the body:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/ocap/v1",
                  "http://schema.org"],
     "id": "did:example:2bdf6273-a52e-4cdf-991f-b5f000008829",
     "type": "Invocation",

     // Dummy Bot is invoking the proclamation it has,
     // but the whole chain will be checked for attenuation and
     // verification of access
     "cert": "did:example:d2c83c43-878a-4c01-984f-b2f57932ce5f",

     // The key Dummy Bot is using in this invocation
     "usingKey": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4#key-1",

     // Finally here's the base64 encoded file as part of the payload
     "file": "nEOSQ7jbzBNg0Glup/FfeGDDzvLDvgEL36wcNpmbvKDgPy6+...",

     // Finally we sign this object with Dummy Bot's key
     "signature": {
        "type": "RsaSignature2016",
        "created": "2016-02-08T17:13:48Z",
        "creator": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4#key-1",
        "signatureValue": "..."}}
```

## Related work

### SPKI/SDSI

[SPKI](http://world.std.com/~cme/html/spki.html) (and previously SDSI)
is a key management project which aimed to resolve many of the issues
(including around centralization) that the X.509 infrastructure
introduced and developed into over time.  SPKI is
[almost but not quite an object capability system](http://www.erights.org/elib/capability/ode/ode-pki.html).
SPKI uses "certificates" (akin to "proclamations"[fn:1](#proclamation-terminology) here)
to express authority, similar to how we are doing so in this document,
but did not exist in a linked data system as our proposal here does.
Importantly, SPKI's authority is a broader form of access control, and for
that reason carries some of the traditional problems of ACLs.

### CapCert

[CapCert](http://wiki.erights.org/wiki/Capability-based_Active_Invocation_Proclamations)
is a (currently unimplemented) plan for a proclamation/certificate
chain based structure which looks a lot like what we have discussed in
this paper.  One major difference is that CapCert was targeting the
[E language](http://erights.org/) primarily, whereas our Proclamation
Chain design for Link Data Signatures targets linked data on the web
more generally.  Otherwise the two systems are mostly similar.

One pleasant feature that both CapCert and LDS Proclamation Chains
share is that the only secret that needs to be maintained in the
system is that each entity must be able to keep their private keys
private.  However, the invocations/proclamations/certificates
themselves can be passed over an insecure transport at no risk of
leaking usablity of the capability, since only granted entities
are able to invoke, delegate, and further attenuate capabilities.


### Macaroons

[Macaroons](https://research.google.com/pubs/pub41892.html) are a
credentials system that uphold most of the properties of capabilities.
They support delegation and attenuation (with some constraints as to
who can attenuate) also via a chain of signed messages, but there are
some key differences.

The biggest feature of Macaroons over our design is that messages are
smaller (a desirable property!) since rather than using public key
cryptography for signatures, a simple HMAC is used.  Macaroons are
thus passed around as bearer instruments over secure channels.  This
leads to a tradeoff: macaroons are smaller in size than LDS
Proclamation Chains, but unlike LDS Proclamation Chains, cannot be
sent or invoked over an insecure channel.  Unlike LDS Proclamation
chains, macaroons cannot be stored on a blockchain or be publicly
retrievable from the web.

One further difference is that while any entity that holds on to a
macaroon may delegate that macaroon to any other entity, not all
entities can attenuate macaroons.  To see why, let us look at our
final configuration between Alice, Bob, Dummy Bot, and Cloud Store:

```
     .-.          .-.           .-.
    ( A )------->( B )-------->( D )
     '-'\         '-'           '-'
       \ \         | \           |
        \ \        V  '---v      |
         \ '---->(R1)<---(R2)<---'
          \        |
           \       V
            \     .-.
             '-->( C )
                  '-'
```

In this configuration, Alice was able to attenuate her capability to
Cloud Store before delegating to Bob without any specific permission to
do so; Bob was likewise able to attenuate the attenuated capability he
held before passing to Dummy Bot without any specific permission.

In Macaroons, Cloud Store and Alice must pre-arrange the shared key
that Alice will use to attenuate the macaroon she holds before she can
do so and successfully delegate to Bob (likewise for Bob to Dummy
Bot).  The reason for this is that in verifying HMAC signatures Cloud
Store must check the macaroon's signatures against a key that Alice
and Cloud Store must both have... Alice to sign it, and Cloud Store to
verify it.  Even if Alice and Cloud Store had prearranged a shared key
to be used for attenuating macaroons, if Bob and Cloud Store had not
done so there would be no way for Bob to further attenuate the
capability before passing to Dummy Bot.  Bob may not prefer this to be
the case since Bob wanted to only give Dummy Bot access for thirty
days.

(Notably, the
[Macaroons paper](https://research.google.com/pubs/pub41892.html)
contains a short but underspecified section that outlines how
Macaroons could be used with public keys instead of HMAC signed bearer
instruments, and the design describe, while in very scant detail,
sounds very similar to how LDS Proclamation Chains work.)

Overall Macaroons and LDS Proclamation Chains are both reasonable
systems with different tradeoffs.  Implementers should be informed
of these tradeoffs and make decisions accordingly.


### Lexical Scope as Capabilities

In this section we introduce a capability system that is in many ways
fairly dramatically different than any of the other systems discussed
in this paper.  Readers who do not wish to go "into the weeds" may
prefer to skip this section.

In the
[W7 Security Kernel](http://mumble.net/~jar/pubs/secureos/secureos.html),
Jonathan Rees introduces an implementation of object capabilities on
nothing other than a strict lexically scoped environment, enforced by
the runtime of the system.
The language shown uses a cut-down variant of Scheme, though it can be
implemented in any language that provides the same strict lexical scoping
properties in a carefully bounded initial environment.
(Indeed the [E language](http://erights.org/) uses strict lexical
scoping as one key part of its capability system.)
The paper demonstrates all the same properties of capabilities we have
shown here: delegation, attenuation, and so on.

However, there is one thing which is possible in W7 that is not
possible in any of the other systems we have discussed in this paper,
including the LDS Proclamation Chains system we have proposed.
This is attenuation by composition in an enclosed environment.
To see what this means and why it is desirable, let us consider an
example.

We have the following initial state:

 - A: Alice
 - C: Cloud Store
 - H: Home Directory
 - T: Timer Service

```
           .-.
          ( H )
           '-'
          ^
         /
     .-./         .-.
    ( A )------->( T )
     '-'\         '-'
         \
          v
           .-.
          ( C )
           '-'
```

(A)lice keeps her data in (H)ome Directory.  She would like to back it
up to (C)loud Service, but she is afraid she will forget to back up
regularly, so she would like to grant a capability to (T)imer Service to
run the backup for her.  However, she would prefer that Timer Service
not have access to actually read any of the contents of her data on Home
Directory, and she does not want Timer Service to be able to write just
anything to Cloud Store, only backups.  Effectively she would like to
send Timer Service a new capability that *composes together* reading
from Home Directory and writing to Cloud Store without giving access to
either independently.  Here R represents the
restricted-through-composition capability in this somewhat messy
diagram:

```
           .-.
          ( H )
           '-'<.
          ^    |
         / _->(R)<-.
     .-./.'    |  .-.
    ( A )------->( T )
     '-'\      ;  '-'
         \    .
          v  v
           .-.
          ( C )
           '-'
```


In Rees' W7 / the lambda-calculus-ocap system, we could represent this
like so:

``` scheme
;; Run in A's environment
(timer-run-every            ; T
  (lambda ()                ; R
    (write-cloud-image      ; C
      (get-homedir-image))) ; H
  (* 60 60 24 7)) ; run every 604800 seconds, or once a week
```

The advantage here is that the runtime is able to enclose the
capabilities and handle the composition of passing the returned value
of one of the enclosed capabilities to the other, without exposing
either individually outside of the enclosure.

It does not appear we can do the same thing in LDS Proclamation
Chains.  Here is a highly cut down invocation which attempts to embed
the capabilities, for the sake of demonstration:

``` javascript
  {"type": "Invocation",
   "usingKey": <alice-key-1>,
   "method": "RunEvery",
   "cert": <cert-id>,
   "secs": 30,
   /* But we would also need to clearly express how to combine these */
   "runTheseCombinedSomehow": [
     <alice-grants-timer-capability-to-homedir>,
     <alice-grants-timer-capability-to-cloudstore>],
   "signature": <signed-by-alice-key-1>}
```

There are two troubles here: making it clear how Timer Service is
supposed to compose these capabilities in runTheseCombinedSomehow is
not obvious, and even worse, there is nothing preventing Timer Service
from running these individually since they are not properly enclosed,
unlike in our W7/Scheme example earlier.  (It could be possible to
embed a properly constrained W7-like language into the linked data
document itself which could do the composition, and indeed
[Smarm](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/draft-documents/smarm.md)
may just be the system for that.  How to combine those systems is left
as a hopefully not too brain-twisting exercise for the reader, or
possibly the subject of a future paper.)

The majority of needs for a capability system are likely served by
attenuation and delegation on their own.  Nonetheless, full
composability within a capability's enclosure, as explored above, is
still a desirable property for the systems that can provide it.


## Conclusions

Linked Data Systems are powerful ways of building collaborative,
expressive systems.  Today we are seeing Linked Data Systems crossing
not only the traditional web but even into systems like distributed
ledger technologies and so on.  Unfortunately, security is frequently
difficult on Linked Data Systems.

For example, [SoLiD](https://solid.mit.edu/) directly uses and
[ActivityPub](https://www.w3.org/TR/activitypub/) indirectly implies
Access Control Lists.  Unfortunately these are are known to
[plague systems with problems](http://www.hpl.hp.com/techreports/2009/HPL-2009-20.html),
particularly:

 - excess authority leading to needless vulnerability
 - ambient authority leading to confused deputy problems
 - lack of composability (including attenuation)

We can avoid these risks by using an object capability system such as
the one described above.  Even more exciting is that by combining
this system with [DIDs](https://w3c-ccg.github.io/did-spec/) we can
build a fully decentralized object capability system for the web that
is safe to use.

<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.proclamation-terminology" name="fn.proclamation-terminology" class="footnum" href="#fnr.proclamation-terminology">1</a></sup>
<p><i><b>TODO:</b> Well it turns out we haven't settled on this term yet!  Remember to switch out the term once we do! :)</p>
<p>
Note: what we are calling "proclamations" have also been called
"certificates" in previous work such as SPKI and CapCert, we have
chosen the name "proclamation chain" to make clear that the structure
we are proposing holds none of the centralization traditionally
associated with "certificate authorities".
</p>
</div>

</div>
</div>
