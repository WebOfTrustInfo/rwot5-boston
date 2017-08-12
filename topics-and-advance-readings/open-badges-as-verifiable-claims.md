# Open Badges as Verifiable Claims

By Kim Duffy and Nate Otto

IM PROGRESS

Open Badges are awarded to describe skills and accomplishments. The learner-centric approach allows individuals to collect and curate their badges through their lifelong learning. Open Badges is used by thousands of organizations, and has developed a rich ecosystem in the educational credentialing/awards space.

The Open Badges contributors above (listed as authors) have also been involved in the Verifiable Claims community. Open Badges already incorporates Verifiable Claims as the Endorsement mode. We would like to explore ways to combine Open Badges and Verifiable Claims to increase interoperability, and to leverage the benefits of both systems.

## Draft of an Open Badge Verifiable Claim

TODO: compare to current OB/Blockcerts example


```json
{
  "id": "https://some.university.edu/credentials/9732",
  "type": [
    "Credential",
    "OpenBadgeCredential"
  ],
  "issuer": "did:example:issuer_did",
  "issued": "2017-06-29T14:58:57.461422+00:00",
  "claim": [
    {
      "id": "did:example:recipient_did",
      "earnedAssertion": {
        "type": "Assertion",
        "badge": {
          "type": "BadgeClass",
          "id": "https://some.university.edu/badges/6415",
          "name": "Certificate of Accomplishment",
          "image": "data:image/png;base64,...",
          "description": "Lorem ipsum dolor sit amet, mei docendi concludaturque ad, cu nec   partem graece. Est aperiam consetetur cu, expetenda moderatius neglegentur ei nam, suas dolor laudem eam an.",
          "criteria": {
            "narrative": "Nibh iriure ei nam, modo ridens neglegentur mel eu. At his cibo mucius."
          }
        }
      }
    }
  ],
  "revocation": {
    "id": "http://example.gov/revocations/738",
    "type": "SimpleRevocationList2017"
  },
  "signature": {}
}
```

## Discussion, tradeoffs
 
TODO: describe tradeoffs above. Some choices I made above (to reduce redundancy) may not be acceptable to the Open Badges community. We'll have to find the right balance.

## Signature schemes, Blockcerts

TODO
