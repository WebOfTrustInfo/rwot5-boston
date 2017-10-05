# Capabilities built on Linked Data Signatures via Certificate Chaining

By Christopher Allan Webber and Mark S. Miller

## Overview

[Linked Data Signatures](https://w3c-dvcg.github.io/ld-signatures/) bring
a method of asserting integrity of linked data documents passed throughout
the web.  The [object capability model](https://en.wikipedia.org/wiki/Object-capability_model)
is a powerful system for ensuring the security of computing systems.
In this paper, we explore layering an object capability model on top
of Linked Data Signatures.

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
     at crypto level, use envelope, certificate, messenger -->

(A)lice has a file upload capability to the (C)loud storage system.
(A)lice also has a capability to send a message to (B)ob, and (B)ob
has a capability to send a message to (D)ummy Bot.

We've met our characters narratively, but let's see what they look
like as linked data documents.

Here is Alice:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/obcap/v1",
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
                  "https://example.org/obcap/v1",
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
                  "https://example.org/obcap/v1",
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
                  "https://example.org/obcap/v1",
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
certificate.  Let's look at what that certificate looks like:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/obcap/v1",
                  "http://schema.org"],
     "id": "did:example:0b36c7844941b61b-c763-4617-94de-cf5c539041f1",
     "type": "Certificate",
     
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
                  "https://example.org/obcap/v1",
                  "http://schema.org"],
     "id": "did:example:f7412b9a-854b-47ab-806b-3ac736cc7cda",
     "type": "Certificate",
     
     // This new attenuated certificate points to the prevoius one
     "parent": "did:example:0b36c7844941b61b-c763-4617-94de-cf5c539041f1",

     // Now we grant access to one of Bob's keys
     "grantedKey": "did:example:ee568de7-2970-4925-ad09-c685ab367b66#key-1",

     // This certificate *does* have a caveat: each upload can only be
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
But he would prefer that DummyBot do uploads for him... well, for a
month.  He'll see how it goes.  Luckily these capabilities are
composable, and so DummyBot can create an attenuated capability out of
the attenuated capability he already has!

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/obcap/v1",
                  "http://schema.org"],
     "id": "did:example:d2c83c43-878a-4c01-984f-b2f57932ce5f",
     "type": "Certificate",

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

Now DummyBot has a capability to upload files to CloudStore, but only
files that are within 50 megabytes, and only for the next month. This
is possible because DummyBot is authorized on the final certificate,
but the certificate "chains upward" including both the immediate
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

Soon DummyBot takes a picture and uploads it:

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

This is done through an `Invocation` on the certificate, along with
additional parameters in the body:

``` javascript
    {"@context": ["https://example.org/did/v1",
                  "https://example.org/obcap/v1",
                  "http://schema.org"],
     "id": "did:example:2bdf6273-a52e-4cdf-991f-b5f000008829",
     "type": "Invocation",

     // Dummy Bot is invoking the certificate they have,
     // but the whole chain will be checked for attenuation and
     // verification of access
     "cert": "did:example:d2c83c43-878a-4c01-984f-b2f57932ce5f",

     // The key Dummy Bot is using in this invocation
     "grantedKey": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4#key-1",

     // Finally we sign this object with Dummy Bot's key
     "signature": {
        "type": "RsaSignature2016",
        "created": "2016-02-08T17:13:48Z",
        "creator": "did:example:5e0fe086-3dd7-4b9b-a25f-023a567951a4#key-1",
        "signatureValue": "..."}}
```

# Conclusions

Linked Data Systems are powerful ways of building collaborative,
expressive systems.  Today we are seeing Linked Data Systems crossing
not only the traditional web but even into systems like distributed
ledger technologies and so on.  Unfortunately, security is frequently
difficult on Linked Data Systems.

For example, [SoLiD](https://solid.mit.edu/) is overall a well structured system but
unfortunately plagued by the use of access control lists, which are
known to have such longstanding problems as:

 - excess authority leading to needless vulnerability
 - ambient authority leading to confused deputy problems
 - lack of composability

We can avoid these risks by using an object capability system such as
the one described above.  Even more exciting is that by combining
this system with [DIDs](https://w3c-ccg.github.io/did-spec/) we can
build a fully decentralized object capability system to the web that
is safe to use.
