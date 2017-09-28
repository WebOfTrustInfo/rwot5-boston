# Trust Objects: Enabling advanced reputation services on the Web of Trust

### Presented by Moses Ma and Dr. Rutu Mulkar-Mehta, FutureLab

### Submitted to the 5th Rebooting the Web of Trust Technical Workshop as a discussion paper

### Boston, October 3-5, 2017

***Keywords:*** reputation, trust, verified claims, collaboration,
innovation, framework, blockchain, decentralized, self-sovereign

## PROPOSAL

We propose to facilitate the collaborative drafting of a technical paper
that describes the principles and key design considerations for an
online framework to manage fully functional reputation services within a
web of trust. The approach uses both transactional and non-transactional
reputation data. Non-transactional reputation data includes both trust
primitives such as verified claims as well as indeterminate trust
assertions. We will also describe the potential use of incentive tokens
for incremental optimization of the eco-system, in a manner that is
especially suited for decentralized, self-sovereign eco-systems.
Finally, we propose to discuss the complexities of online disagreements
and how to resolve and adjudicate them in a pareto-optimal manner.

We base much of our work on key design considerations for decentralized
reputation, developed by C. Allen and by A.C. de Crespigny et al (see
references), at the Spring 2017 RWOT design conference in Paris.

Reputation is social concept that is an essential component of social
and business networks, because it serves as an optimizing influence on
such systems. However, while there have been numerous analyses of how
reputation may be computed and managed, there has to date been no
systematic approach for implementing reputation systems, nor strategies
for self-optimizing reputation management, proposed for decentralized
networks. Our goal is to develop an inter-disciplinary, game-theoretic
model for computational trust and reputation based on psychology and
micro-economics.

The proposed approach utilizes both transactional and non-transactional
trust data. Transactional data includes a record of failed vs successful
transactions, such as the history of successful vs unsuccessful
transactions at eBay. Non-transactional data includes trust primitives
such as verified claims, as well as indeterminate trust assertions. This
paper also shows that it is possible use incentive tokens to drive
incremental optimization of the eco-system, in a manner that is
especially suited for decentralized, self-sovereign eco-systems.
Finally, we propose to discuss the complexities of online disagreements
and propose key design considerations for systems that could more
effectively resolve and adjudicate disputes, in a pareto-optimal manner.

We believe there are several important principles that apply to
non-transactional reputation systems, which could be used to help govern
their design and operation within enterprises and organizations. These
are:

-   Reputation is complex.

-   Trust and reputation are transitive.

-   Reputation is a convolution of trust primitives.

-   Reputation is a narrative, a dynamic social process, not a static
    credit score.

-   Reputation is a currency.

-   Reputation is all about people.

Using these principles, we offer a model for computational reputation
that is functional and useful, adaptive and self-optimizing. In our
model, reputation is defined to be a convolution of transactional and
non-transactional data, with associated weighting based on the
trustability of the rater. We will also discuss the requirements for
continuous reputation tracking, adaptive weighting with artificial
intelligence based adaptive learning, neural networks for behavioral
pattern detector, and automatic normalization of voting weights.

Finally, the most important goal for this working draft is to map the
emergent model to the proposed DID and Verified Claims standards. Our
proposal is simply to add a field to the basic verified claim system, in
the form of a “protocol cookie”. Cookies were designed to be a reliable
mechanism for websites to remember stateful information or to record the
user's browsing activity. Therefore, this field would enable the claim
to remember stateful information – such as a URI for the claim offerer’s
reputation rating, or to record the history of entities that have
accessed the claim, or to manage visibility settings for the claim, so
that disclosure of the claim could be selectively permissioned. The most
valuable function of the field would be to provide a URI to an ontology
or classification system for the claim to provide metadata about the
size or scope of the claim.

The paper will include a design philosophy for the implementation of
reputation engines that are “self-optimizing” using “optimization
tokens” that promote more effective and truthful rating and reporting by
people. These tokens can also be earned by artificial intelligence
systems that act in a manner similar to miners, but providing
optimization services. For example, neural network based fraud detection
systems could be developed to look for “ratings extortionists”, who
threaten negative reviews if not provided a discount.

## Next Steps

We would like to collaborate with the participants of the Rebooting Web
of Trust Workshop to refine the concepts and use cases. Our goal is to
produce both an improved, more easily extensible standard, as well as a
demo that demonstrates a compelling use case directly after the
workshop.

## References

[http://www.lifewithalacrity.com/2016/04/the-path-to-self-soverereign-identity.html](http://www.lifewithalacrity.com/2016/04/the-path-to-self-soverereign-identity.html
)

[https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/ProjectVouch\_Peer-attestation-and-reputation-based-identity.md](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/ProjectVouch\_Peer-attestation-and-reputation-based-identity.md)
