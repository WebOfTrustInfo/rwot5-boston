<div id="respecHeader" class="head" role="contentinfo">

[![W3C](https://www.w3.org/StyleSheets/TR/2016/logos/W3C)](https://www.w3.org/)

Veres One DID Method 1.0
========================

A decentralized identifier method for the Veres One Ledger
----------------------------------------------------------

Draft Community Group Report 01 October 2017
--------------------------------------------

Latest editor's draft:
:   <https://w3c-ccg.github.io/didm-veres-one/>

Editors:
:   [Manu Sporny](http://manu.sporny.org/), [Digital
    Bazaar](https://digitalbazaar.com/)
:   [Dave Longley](https://github.com/dlongley), [Digital
    Bazaar](https://digitalbazaar.com/)

Authors:
:   [Manu Sporny](http://manu.sporny.org/), [Digital
    Bazaar](https://digitalbazaar.com/)
:   [Dave Longley](https://github.com/dlongley), [Digital
    Bazaar](https://digitalbazaar.com/)

Participate:
:   [GitHub
    w3c-ccg/didm-veres-one](https://github.com/w3c-ccg/didm-veres-one)
:   [File a bug](https://github.com/w3c-ccg/didm-veres-one/issues/)
:   [Commit
    history](https://github.com/w3c-ccg/didm-veres-one/commits/gh-pages)

[Copyright](https://www.w3.org/Consortium/Legal/ipr-notice#Copyright) ©
2017 the Contributors to the Veres One DID Method 1.0 Specification,
published by the [Credentials Community
Group](https://www.w3.org/community/credentials/) under the [W3C
Community Contributor License Agreement
(CLA)](https://www.w3.org/community/about/agreements/cla/). A
human-readable
[summary](https://www.w3.org/community/about/agreements/cla-deed/) is
available.

------------------------------------------------------------------------

</div>

<div id="abstract" class="section introductory">

Abstract
--------

The Veres One Ledger is a permissionless public ledger designed
specifically for the creation and management of [decentralized
identifiers](https://w3c-ccg.github.io/did-spec/) (DIDs). Veres One DIDs
are [self-sovereign
identifiers](https://www.coindesk.com/path-self-sovereign-identity/)
that may be used by people, organizations, and digital devices to
establish an identifier that is under their control. Veres One DIDs are
useful in ecosystems where one needs to issue, store, and use
[Verifiable Claims](https://w3c.github.io/vc-data-model/). This
specification defines how a developer may create and update DIDs in the
Veres One Ledger.

</div>

<div id="sotd" class="section introductory">

Status of This Document
-----------------------

This specification was published by the [Credentials Community
Group](https://www.w3.org/community/credentials/). It is not a W3C
Standard nor is it on the W3C Standards Track. Please note that under
the [W3C Community Contributor License Agreement
(CLA)](https://www.w3.org/community/about/agreements/cla/) there is a
limited opt-out and other conditions apply. Learn more about [W3C
Community and Business Groups](https://www.w3.org/community/).

Comments regarding this document are welcome. Please file issues
directly on [GitHub](https://github.com/w3c-ccg/didm-veres-one/issues/),
or send them to <public-credentials@w3.org>
([subscribe](mailto:public-credentials-request@w3.org?subject=subscribe),
[archives](https://lists.w3.org/Archives/Public/public-credentials/)).

Work on this specification has been funded in part by the United States
Department of Homeland Security's Science and Technology Directorate
under contract HSHQDC-17-C-00019. The content of this specification does
not necessarily reflect the position or the policy of the U.S.
Government and no official endorsement should be inferred.

Work on this specification has also been supported by the Rebooting the
Web of Trust group facilitated by Christopher Allen, Shannon Appelcline,
Kiara Robles, Kaliya Young, Brian Weller, and Betty Dhamers.

If you wish to make comments regarding this document, please send them
to <public-credentials@w3.org>
([subscribe](mailto:public-credentials-request@w3.org?subject=subscribe),
[archives](https://lists.w3.org/Archives/Public/public-credentials/)).

</div>

Table of Contents
-----------------

1.  [<span class="secno">1. </span>Introduction](#introduction)
2.  [<span class="secno">2. </span>Core Data Model](#core-data-model)
3.  [<span class="secno">3. </span>Basic Concepts](#basic-concepts)
    1.  [<span class="secno">3.1 </span>Authentication](#authentication)
    2.  [<span class="secno">3.2 </span>Authorization](#authorization)
    3.  [<span class="secno">3.3 </span>Service
        Descriptions](#service-descriptions)

4.  [<span class="secno">4. </span>Operations](#operations)
    1.  [<span class="secno">4.1 </span>Discovering Service
        Endpoints](#discovering-service-endpoints)
    2.  [<span class="secno">4.2 </span>Creating a DID](#creating-a-did)
    3.  [<span class="secno">4.3 </span>Updating a DID
        Document](#updating-a-did-document)
    4.  [<span class="secno">4.4 </span>Delegating
        Control](#delegating-control)
    5.  [<span class="secno">4.5 </span>Key Rotation and Transferring
        Control](#key-rotation-and-transferring-control)
    6.  [<span class="secno">4.6 </span>Recovering a
        DID](#recovering-a-did)

5.  [<span class="secno">5. </span>Appendix A:
    Examples](#appendix-a:-examples)
    1.  [<span class="secno">5.1 </span>Typical DID
        Document](#typical-did-document)
    2.  [<span class="secno">5.2 </span>Legacy DID
        Document](#legacy-did-document)

<div id="introduction" class="section">

<span class="secno">1. </span>Introduction
------------------------------------------

<div id="issue-1" class="issue">

<div id="h-issue1" class="issue-title marker" aria-level="3"
role="heading">

<span>Issue 1</span>

</div>

TBD: This section will provide a gentle introduction to the purpose of
the Veres One Ledger, expanding upon the abstract of the document.

</div>

</div>

<div id="core-data-model" class="section">

<span class="secno">2. </span>Core Data Model
---------------------------------------------

<div id="issue-2" class="issue">

<div id="h-issue2" class="issue-title marker" aria-level="3"
role="heading">

<span>Issue 2</span>

</div>

TBD: This section will describe the use of the Web Ledger, JSON-LD, and
the DID spec to build the Veres One Ledger.

</div>

</div>

<div id="basic-concepts" class="section">

<span class="secno">3. </span>Basic Concepts
--------------------------------------------

<div id="authentication" class="section">

### <span class="secno">3.1 </span>Authentication

Authentication is the process the ledger uses to determine if an entity
is associated with a DID.

<div class="example">

<div class="example-title marker">

<span>Example 1</span><span style="text-transform: none">: Expressing
authentication credentials</span>

</div>

``` {.nohighlight}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938",
  "authenticationCredential": [... array of acceptable authentication credentials ...]
}
```

</div>

A detailed example of a valid set of authentication credentials follows:

<div class="example">

<div class="example-title marker">

<span>Example 2</span><span style="text-transform: none">: Detailed
example of authentication credentials entry</span>

</div>

``` {.nohighlight}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938",
  "authenticationCredential": [{
    "type": "RsaSignature2017",
    "publicKey": {
      "id": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938/keys/2",
      "type": "CryptographicKey",
      "owner": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938",
      "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n",
    }
  }]
}
```

</div>

</div>

<div id="authorization" class="section">

### <span class="secno">3.2 </span>Authorization

Authorization is the process the ledger uses to determine what an entity
may to do the DID Document.

<div class="example">

<div class="example-title marker">

<span>Example 3</span>

</div>

``` {.nohighlight title=""}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938",
  "authorizationCapability": [... array of capability descriptions ...]
}
```

</div>

A detailed example of a valid set of authorization capability
descriptions follows:

<div class="example">

<div class="example-title marker">

<span>Example 4</span>

</div>

``` {.nohighlight title=""}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938",
  // proof of update authorization may be provided by digital wallet + friend OR
  // by mobile phone
  "authorizationCapability": [{
    // this entity may update any field in this DID Document using any
    // authentication mechanism understood by the ledger
    "permission": "UpdateDidDocument",
    "entity": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938"
  }, {
    // this entity may update the authenticationCredential field in this
    // DID Document as long as they authenticate with RsaSignature2017
    "entity": "did:v1:b5f8c320-f7ca-4869-85e6-a1bcbf825b2a",
    "permission": "UpdateDidDocument",
    "field": ["authenticationCredential"],
    "permittedProofType": [{
      "proofType": "RsaSignature2017"
    }]
  }, {
    // anyone may update the authenticationCredential and writeAuthorization
    // fields as long as they provide a specific multi-signature proof
    "permission": "UpdateDidDocument",
    "field": ["authenticationCredential", "authorizationCapability"],
    "permittedProofType": [{
      "proofType": "RsaSignature2017",
      "minimumSignatures": 3,
      "authenticationCredential": [{
        "id": "did:v1:304ebc3e-7997-4bf4-a915-dd87e8455941/keys/123",
        "type": "RsaCryptographicKey",
        "owner": "did:v1:304ebc3e-7997-4bf4-a915-dd87e8455941",
        "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
      }, {
        "id": "did:v1:0f22346a-a360-4f3e-9b42-3366e348e941/keys/foo",
        "type": "RsaCryptographicKey",
        "owner": "did:v1:0f22346a-a360-4f3e-9b42-3366e348e941",
        "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
      }, {
        "id": "did:v1:a8d00377-e9f1-44df-a1b9-55072e13262a/keys/abc",
        "type": "RsaCryptographicKey",
        "owner": "did:v1:a8d00377-e9f1-44df-a1b9-55072e13262a",
        "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
      }]
    }]
}
```

</div>

</div>

<div id="service-descriptions" class="section">

### <span class="secno">3.3 </span>Service Descriptions

Services may be listed by including them at the top-level of the DID
Document.

<div class="example">

<div class="example-title marker">

<span>Example 5</span><span style="text-transform: none">: Simple
example of a service description</span>

</div>

``` {.nohighlight}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938",
   "credentialRepositoryService": "https://wallet.veres.io/"
}
```

</div>

A detailed example of the expression of a service description follows:

<div class="example">

<div class="example-title marker">

<span>Example 6</span>

</div>

``` {.nohighlight title=""}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "did:v1:215cb1dc-1f44-4695-a07f-97649cad9938",
  "credentialRepositoryService": [{
    // the verifiable credential repository service
    "id": "did:v1:5d6c3b20-56a9-42e1-bfc8-ed7e685c9039",
    "type": "VerifiableCredentialRepository",
    "url": "https://wallet.veres.io/",
    "description": "Pat Doe's Digital Wallet"
  }]
}
```

</div>

</div>

</div>

<div id="operations" class="section">

<span class="secno">4. </span>Operations
----------------------------------------

Every conforming Veres Ledger node *MUST* expose at least the following
HTTP endpoints:

  Service                 Example URL        Description
  ----------------------- ------------------ ----------------------------------
  veresOneCreateService   POST /dids         Create a new DID.
  veresOneReadService     GET /dids/{did}    Gets an existing DID Document.
  veresOneUpdateService   POST /dids/{did}   Update an existing DID Document.

<div id="discovering-service-endpoints" class="section">

### <span class="secno">4.1 </span>Discovering Service Endpoints {#x4.1-discovering-service-endpoints}

A website may provide service endpoint discovery by embedding JSON-LD in
their top-most HTML web page (e.g. at `https://example.com/`):

<div class="example">

<div class="example-title marker">

<span>Example 7</span><span style="text-transform: none">: Example of
HTML-based service description</span>

</div>

``` {.highlight .hljs .xml aria-busy="false" aria-live="polite"}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Example Website</title>
    <link rel="stylesheet" href="style.css">
    <script src="script.js"></script>
    <script type="application/ld+json">
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "https://example.com/",
  "name": "Example Website",
  "veresOneCreateService": "https://example.com/veres-one/dids",
  "veresOneReadService": "https://example.com/veres-one/dids/",
  "veresOneUpdateService": "https://example.com/veres-one/dids/"
}
    </script>
  </head>
  <body>
    <!-- page content -->
  </body>
</html>
```

</div>

Service descriptions may also be requested via content negotiation. In
the following example a JSON-compatible service description is provided
(e.g. `curl -H "Accept: application/json" https://example.com/`):

<div class="example">

<div class="example-title marker">

<span>Example 8</span><span style="text-transform: none">: Example of a
JSON-based service description</span>

</div>

``` {.highlight .hljs .json aria-busy="false" aria-live="polite"}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "https://example.com/",
  "name": "Example Website",
  "veresOneCreateService": "https://example.com/veres-one/dids",
  "veresOneReadService": "https://example.com/veres-one/dids/",
  "veresOneUpdateService": "https://example.com/veres-one/dids/"
}
```

</div>

</div>

<div id="creating-a-did" class="section">

### <span class="secno">4.2 </span>Creating a DID

A DID is created by performing an HTTP POST of a signed DID Document to
the `veresOneCreateService`. The following HTTP status codes are defined
for this service:

  HTTP Status   Description
  ------------- --------------------------------------------------------------------------------------------------------------------------
  201           DID creation request was successful. The HTTP `Location` header will contain the URL for the newly created DID Document.
  400           DID creation request failed.
  409           A duplicate DID exists.

An example exchange of DID creation request is shown below:

<div class="example">

<div class="example-title marker">

<span>Example 9</span><span style="text-transform: none">: DID creation
request</span>

</div>

``` {.highlight .hljs .http aria-busy="false" aria-live="polite"}
POST /dids HTTP/1.1
Host: example.com
Content-Type: application/ld+json
Content-Length: 1062
Accept: application/ld+json, application/json, text/plain, */*
Accept-Encoding: gzip, deflate

{
  "@context": "https://w3id.org/webledger/v1",
  "type": "WebLedgerEvent",
  "operation": "Create",
  "input": [{
    "@context": "https://w3id.org/veres-one/v1",
    "id": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
    "authorizationCapability": [{
      "permission": "UpdateDidDocument",
      "entity": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
      "permittedProofType": [{
        "proofType": "LinkedDataSignature2015"
      }, {
        "proofType": "EquihashProof2017",
        "equihashParameterAlgorithm": "VeresOne2017"
      }]
    }],
    "authenticationCredential": [{
      "id": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84/keys/1",
      "type": "CryptographicKey",
      "owner": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
      "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n
        MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAmbDqPu6IKHiiIQ4d0AQ6\r\n
        PBduDhUUVqyQirvxqsdcNdKgZ2L8whBml/nTyuB4cd+hHrsfMDiHiT5kX2pbZ7Yy\r\n
        2ctWkGw8e0J94CbwVh2H15gBQBUCjLiGvVIHO2pni693qmre+3Ya2NJ8gGwPLJ7h\r\n
        TLca2b2dX0y16qu0MT0osUGGEoPsdg6ibD2pxnADS3GNPObHT12GrAuxjYFMHecF\r\n
        A4hLZ8U+MIcVmHZuokqqbcyJyjOV+kmhFNeTKFP5P5U8HA3Y42/rE1UJp/wyy7Lc\r\n
        ZAvq0t75ddXKyvYh5dkzxxeeELNKNWVxJ2yvgAr0SatLEPzxJoeYdCyU5N5E22Fj\r\n
        jQIDAQAB\r\n-----END PUBLIC KEY-----\r\n"
    }]
  }],
  "signature": [{
    "type": "EquihashProof2017",
    "equihashParameterN": 64,
    "equihashParameterK": 3,
    "nonce": "AQAAAA==",
    "proofValue": "AAAaPwABxrIAAFOKAAGo4QAAVW0AAN7cAACXcgABjEI="
  }, {
    "type": "LinkedDataSignature2015",
    "created": "2017-09-30T02:54:31Z",
    "creator": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84/keys/1",
    "signatureValue": "SNMbsPqLnB+hJFhXzS6hcpZnm9cGvSZZg7o26UYnyGYTvKder/S+Xk
      hNhXisS5385Ljlf5CXTQT5j6qYZtP8ut1Benaae8TMH17txP0CfzHbUMJFnHA1+Nru+e/Pw
      yPwuQ+VZYlXOB7g/tKVVZsxAYTKCAOJvJMIE+nlHjpB+RsKs9z4ZzVtddntqqAcvbZxV/o7
      azBFDizeJu/gHVVMncCJ00SRoOzCOZUABRJV/k68bNSAfpELkrdWx8/xvMIF8r+LWhwdKCS
      iOw4DjSwIK40yD5rOvQn/GlC+unyB8zFe60jCToz/UOJNZBiIYwo+Pwwx28Wqd4Jkb3IeDr
      /L2Q=="
  }]
}
```

</div>

If the creation of the DID was successful, an HTTP 201 status code is
expected in return:

<div class="example">

<div class="example-title marker">

<span>Example 10</span><span style="text-transform: none">: Successful
DID creation response</span>

</div>

``` {.highlight .hljs .http aria-busy="false" aria-live="polite"}
HTTP/1.1 201 Created
Location: https://ledger.example.com/dids/did:v1:215cb1dc-1f44-4695-a07f-97649cad9938
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
Expires: 0
Date: Fri, 14 Oct 2016 18:35:33 GMT
Connection: keep-alive
Transfer-Encoding: chunked
```

</div>

</div>

<div id="updating-a-did-document" class="section">

### <span class="secno">4.3 </span>Updating a DID Document

A DID is updated by performing an HTTP POST of a signed DID Document to
the `veresOneUpdateService`. The following HTTP status codes are defined
for this service:

  HTTP Status   Description
  ------------- ------------------------------------
  200           DID update request was successful.
  400           DID update request failed.

An example exchange for a DID update request is shown below:

<div class="example">

<div class="example-title marker">

<span>Example 11</span><span style="text-transform: none">: DID Document
update request</span>

</div>

``` {.highlight .hljs .http aria-busy="false" aria-live="polite"}
POST /dids/did:v1:215cb1dc-1f44-4695-a07f-97649cad9938 HTTP/1.1
Host: example.com
Content-Type: application/ld+json
Content-Length: 1062
Accept: application/ld+json, application/json, text/plain, */*
Accept-Encoding: gzip, deflate

{
  "@context": "https://w3id.org/webledger/v1",
  "type": "WebLedgerEvent",
  "operation": "Update",
  "input": [{
    "@context": "https://w3id.org/veres-one/v1",
    "id": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
    "authorizationCapability": [{
      "permission": "UpdateDidDocument",
      "entity": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
      "permittedProofType": [{
        "proofType": "LinkedDataSignature2015"
      }, {
        "proofType": "EquihashProof2017",
        "equihashParameterAlgorithm": "VeresOne2017"
      }]
    }],
    "authenticationCredential": [{
      "id": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84/keys/1",
      "type": "CryptographicKey",
      "owner": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
      "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n
        MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAmbDqPu6IKHiiIQ4d0AQ6\r\n
        PBduDhUUVqyQirvxqsdcNdKgZ2L8whBml/nTyuB4cd+hHrsfMDiHiT5kX2pbZ7Yy\r\n
        2ctWkGw8e0J94CbwVh2H15gBQBUCjLiGvVIHO2pni693qmre+3Ya2NJ8gGwPLJ7h\r\n
        TLca2b2dX0y16qu0MT0osUGGEoPsdg6ibD2pxnADS3GNPObHT12GrAuxjYFMHecF\r\n
        A4hLZ8U+MIcVmHZuokqqbcyJyjOV+kmhFNeTKFP5P5U8HA3Y42/rE1UJp/wyy7Lc\r\n
        ZAvq0t75ddXKyvYh5dkzxxeeELNKNWVxJ2yvgAr0SatLEPzxJoeYdCyU5N5E22Fj\r\n
        jQIDAQAB\r\n-----END PUBLIC KEY-----\r\n"
    }, {
      "id": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84/keys/2",
      "type": "CryptographicKey",
      "owner": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
      "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n
        MIIBIj0BAQEFAKHiiIQ4d0AQ6ANBgkqhkiG9wAOCAQ8AMIIBCgKCAQEAmbDqPu6I\r\n
        xqsdcNdKgZ2L8whBml/nTyuBiHiPBduDhUUVqyQirvT5kX2pbZ7Yy4cd+hHrsfMD\r\n
        VhVIHO2pni693qmre+2ctWkGw8e0J94Cbw3Ya2NJ8gGwPLJ7hH15gBQBUCjLiGv\r\n
        0osUNPObHT12GrAuxjYFMHecFGTLca2b2dX0y16qu0MTGEoPsdg6ibD2pxnADS3G\r\n
        kqqbcyJyjOV+kmh8HA3Y42/rE1UJpA4hLZ8U+MIcVmHZuo/wyy7LcFNeTKFP5P5U\r\n
        5dkzxxezxJoeYdCyU5N5E2ZAvq0t75ddXKyvYh2FjeELNKNWVxJ2yvgAr0SatLEP\r\n
        AQABjQID\r\n-----END PUBLIC KEY-----\r\n"
    }]
  }],
  "signature": [{
    "type": "EquihashProof2017",
    "equihashParameterN": 64,
    "equihashParameterK": 3,
    "nonce": "AQAAAA==",
    "proofValue": "AAAaPwABxrIAAFOKAAGo4QAAVW0AAN7cAACXcgABjEI="
  }, {
    "type": "LinkedDataSignature2015",
    "created": "2017-09-30T02:54:31Z",
    "creator": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84/keys/2",
    "signatureValue": "Zg7o26UYnyGYTvKdSN6hcpZnm9cGvSZB+hJFhXzSer/S+XkMbsPqLn
      VMncCJ00SRoOzCOZUABRJV/azBFDizeJu/gHVk68bNSAfpELkrdWx8/xvMIF8r+LWhwdKCS
      XTQT5j6qYZtP8ut1BenahNhXisS5385Ljlf5Cae8TMH17txP0CfzHbUMJFnHA1+Nru+e/Pw
      K40yD5rOvQn/GlC+unyB8ziOw4DjSwIFe60jCToz/UOJNZBiIYwo+Pwwx28Wqd4Jkb3IeDr
      VVZsxAYTKCAOJvJMIE+nlHjpB+RyPwuQ+VZYlXOB7g/tKsKs9z4ZzVtddntqqAcvbZxV/o7
      /45H=="
  }]
}
```

</div>

If the update request for the DID was successful, an HTTP 200 status
code is expected in return:

<div class="example">

<div class="example-title marker">

<span>Example 12</span><span style="text-transform: none">: Successful
ledger creation response</span>

</div>

``` {.highlight .hljs .http aria-busy="false" aria-live="polite"}
HTTP/1.1 200 Success
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
Expires: 0
Date: Fri, 14 Oct 2016 18:35:33 GMT
Connection: keep-alive
Transfer-Encoding: chunked
```

</div>

</div>

<div id="delegating-control" class="section">

### <span class="secno">4.4 </span>Delegating Control

<div id="issue-3" class="issue">

<div id="h-issue3" class="issue-title marker" aria-level="4"
role="heading">

<span>Issue 3</span>

</div>

TBD: Explain that delegation of control is merely placing a digital
wallet provider in the proofOfControl field.

</div>

</div>

<div id="key-rotation-and-transferring-control" class="section">

### <span class="secno">4.5 </span>Key Rotation and Transferring Control

<div id="issue-4" class="issue">

<div id="h-issue4" class="issue-title marker" aria-level="4"
role="heading">

<span>Issue 4</span>

</div>

TBD: Explain that transferring control and rotating keys is a matter of
adding and removing the appropriate keys from proofofControl and
proofOfUpdateAuthorization.

</div>

</div>

<div id="recovering-a-did" class="section">

### <span class="secno">4.6 </span>Recovering a DID

<div id="issue-5" class="issue">

<div id="h-issue5" class="issue-title marker" aria-level="4"
role="heading">

<span>Issue 5</span>

</div>

TBD: Explain that recoverying a DID is a matter of meeting the
requirements under proofOfUpdateAuthorization.

</div>

</div>

</div>

<div id="appendix-a:-examples" class="section">

<span class="secno">5. </span>Appendix A: Examples
--------------------------------------------------

<div id="typical-did-document" class="section">

### <span class="secno">5.1 </span>Typical DID Document 

The following is a complete example of a typical Veres One DID Document:

<div class="example">

<div class="example-title marker">

<span>Example 13</span>

</div>

``` {.nohighlight}
{
  "@context": "https://w3id.org/veres-one/v1",
  "id": "did:v1:eaaf4df5-471d-404e-b143-652fe38cd2c7",
  "authorizationCapability": [{
    "permission": "UpdateDidDocument",
    "entity": "did:v1:eaaf4df5-471d-404e-b143-652fe38cd2c7",
    "permittedProofType": [{
      "proofType": "LinkedDataSignature2015"
    }, {
      "proofType": "EquihashProof2017",
      "equihashParameterAlgorithm": "VeresOne2017"
    }]
  }],
  "authenticationCredential": [{
    "id": "did:v1:eaaf4df5-471d-404e-b143-652fe38cd2c7/keys/1",
    "type": "CryptographicKey",
    "owner": "did:v1:eaaf4df5-471d-404e-b143-652fe38cd2c7",
    "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n
      MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvZXq8jX38lwndvzadCsT\r\n
      Xa2Zafdrg9I69gzfccH6XWY3Ddi/JoMuTSB1GwxKBfXpo9gjaPYsm6wCLv9Kku4x\r\n
      HL4LA1kmIalVTVDYgSO4sGK9k9oQNTY+hgUoTtdMxMShWrVy6+DIS/ZzIPyQBtbm\r\n
      9D7RojrvESmjq/OuMs6sTlC0JjEE1ijuuHY+iY7gDYcR7RGFAsi4WGbCVy6c8VqL\r\n
      29h8yGps2U+AxKr9f783VGMCk469ESHVwVyw6Jbxihn/h4TH3ZH8WTQW9rpS9GhO\r\n
      euSAA6iSH5UcmAzJZKSzaC+oghEJwMtOcgvr1F9iSn9tuHebgy9R6tHvEChhvdgz\r\n
      2wIDAQAB\r\n
      -----END PUBLIC KEY-----\r\n",
  }]
}
```

</div>

</div>

<div id="legacy-did-document" class="section">

### <span class="secno">5.2 </span>Legacy DID Document

The Veres One ledger was launched in 2015, predated this specification,
and as a result has a number of legacy objects that developers should be
aware of. The typical format for these objects are shown below:

<div class="example">

<div class="example-title marker">

<span>Example 14</span>

</div>

``` {.nohighlight}
{
  "@context": "https://w3id.org/identity/v1",
  "id": "did:8743453f-e45e-4ac6-b85f-4513ba4c1460",
  "idp": "did:d1d1d1d1-d1d1-d1d1-d1d1-d1d1d1d1d1d1",
  "accessControl": {
    "writePermission": [
      {
        "id": "did:8743453f-e45e-4ac6-b85f-4513ba4c1460/keys/1",
        "type": "CryptographicKey"
      },
      {
        "id": "did:d1d1d1d1-d1d1-d1d1-d1d1-d1d1d1d1d1d1",
        "type": "Identity"
      }
    ]
  },
  "publicKey": [
    {
      "id": "did:8743453f-e45e-4ac6-b85f-4513ba4c1460/keys/1",
      "type": "CryptographicKey",
      "owner": "did:8743453f-e45e-4ac6-b85f-4513ba4c1460",
      "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\nMIIBIjA...DAQAB\r\n-----END PUBLIC KEY-----\r\n",
      "@context": "https://w3id.org/identity/v1"
    }
  ],
  "signature": {
    "type": "LinkedDataSignature2015",
    "created": "2017-07-25T17:29:49Z",
    "creator": "did:8743453f-e45e-4ac6-b85f-4513ba4c1460/keys/1",
    "signatureValue": "LJoxpV...daOLHbA=="
  }
}
```

</div>

</div>

</div>

[↑](#toc)
