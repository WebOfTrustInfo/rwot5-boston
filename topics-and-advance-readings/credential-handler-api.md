# Decentralized Identifier Tooling
***by Dave Longley and Manu Sporny, Digital Bazaar***

## Introduction

The Verifiable Claims Ecosystem envisions a variety of ways that
credentials will be exchanged between Issuers, Holders, and Verifiers.

<a href="https://w3c.github.io/vc-data-model/">
  <img src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/master/topics-and-advance-readings/verifiable-claims-primer-diagrams/ecosystem.svg" width="100%" height="400">
</a>

Protocols that use Verifiable Claims to exchange data could be designed such
that they are compatible with existing SAML and OpenID Connect-based systems.
We also expect Verifiable Claims to be carried over protocols such as
HTTP, Bluetooth, and RFID.

Over the years, Digital Bazaar has proposed various mechanisms that could be
used to carry Verifiable Claims over browser-based protocols. This paper
focuses on a recent advance in this area.

## Credential Handler API

Digital Bazaar has created a browser-based polyfill called the Credential
Handler API that is designed to send and receive Verifiable Claims.

A polyfill is a browser fallback, made in JavaScript, that allows functionality
that a developer expects to work in modern browsers to work in older
browsers, e.g., support for new Javascript (ES6) features.

When incubating a technology intended for browsers, it is often useful to
polyfill the technology and deploy it into limited usage to ensure that it
works in the field. This data can later be used to convince browser
manufacturers that there is a measured need for the technology to be built
into the browser natively.

What follows is a video demonstrating the polyfill for Verifiable Claims that
Digital Bazaar has created:

[Credential Handler API Video](https://www.youtube.com/watch?v=bm3XBPB4cFY)

### Credential Handler Source Code

The Credential Handler source code is available on Github:

[Credential Handler Github Repository](https://github.com/digitalbazaar/credential-handler-polyfill)
[Credential Handler Demo Websites Github Repository](https://github.com/digitalbazaar/credential-handler-demo)

The source code can be used on the demonstration websites here:

[Credential Handler Demo Websites](https://credential-repository.demo.digitalbazaar.com/)

## Collaboration

We are seeking to collaborate with individuals at this Rebooting Web of Trust
event to review the user interaction flow for the Credential Handler API. We
are also looking for developers who think that this polyfill would be useful
to their organization when deploying Verifiable Claims to their customers.
Finally, we're looking for feedback from developers on the code examples to
determine if they would like to see any changes or modifications to the
polyfill.

