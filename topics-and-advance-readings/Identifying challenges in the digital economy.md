## Identifying stakeholders' challenges in the digital economy
By Irene Hernandez

Existing identity management systems do not work in the digital economy. Internet’s architecture mimicked the physical world, as issuers or central administrators were responsible for creating and managing large databases of validated user information. As a result, internet-based companies today require customers to a) fill out comprehensive online profiles with sensitive information and b) upload copies of physical documents to then spend millions of dollars in manual validation processes. For some companies, operating a large database of user data is an asset, but for many others is an expensive burden:
1. On-boarding user-facing processes are inefficient and cumbersome, resulting in poor customer experience.
2. New companies face high entry barriers, as they need to build trust on consumers for them to concede on providing sensitive attributes over the web.
3. Companies become an increasingly attractive target for security threats and, as such, have to invest in expensive security infrastructure.
4. Companies are unable to ensure that records are up to date. Thus, companies bear an obscure risk, as they cannot accurately assess the risk of doing business with their customers. 
5. Data must be curated to allow for vertical integration with suppliers and partners, leading to errors and inefficiencies.
6. Despite all possible efforts, incorrect user information, poor authentication or fraud cannot be fully eliminated

This is the case for many financial institutions like banks or investment management companies, insurance providers, governmental organizations, healthcare providers, P2P service platforms and eCommerce sites.

The problem is acute for end users too, who have to manually create dozens if not hundreds of user accounts. This model has consequences: 
1. Users are forced to give up on sensitive information repeated times, ultimately losing control of who is storing it. 
2. Security risks are unknown, as there is no information about the number of copies made out of each attribute or what security measures are in place. 
3. There are no standard procedures nor tools to audit the list of companies that store or have access to an individual’s private data. 
4. Data protection policies and regulations have borders. Hence, deleting customer records is not guaranteed nor is simple. 
5. Updating attributes is inconvenient and leads to operational problems for both the company and individuals –e.g. two-factor authentication problems due to dated phone number. 
6. Individuals are forced to resign the right to monetize their own information. Since information of one single individual is not worthy, companies retain the power to offer aggregated data. 

We should radically change the way we structure our identification and authentication systems in the digital world. The self-sovereign identity concept coined by Christopher Allen solves most if not all of the end users’ problems. Instead of multiple proprietary databases of users –one per each organization-, we can think of a far more efficient process if we pursue a distributed architecture where individuals would hold a unique digital ID with a unique identifier and associated attributes.

![Image of architecture](https://github.com/irene-h/Gataca/blob/master/img_rep/architecture.png)

However, structural changes like this require massive adoption. Therefore, we need to address the challenges of both market sides and aim at bootstrapping a network not only of users but also of service providers. I claim that trusted, distributed, and global identification services are needed by organizations and users alike. They have the potential to unlock instant access to services worldwide, while keeping information secure, private and under customer’s control. In return, companies can rely on trusted identification sources, overcome the advantage of traditional firms that enjoy broad confidence as guardians of information, lower entry barriers, and easily comply with regulatory requirements. 

Notwithstanding the benefits, many companies will have to overcome significant switching costs to capture the value created. So, how do we seamlessly transition to a decentralized model? I believe that the answer lies in a fully integrated solution that incorporates the full stack of needs:

- Data structure standards
- Authentication
- Authorization
- Interoperability
- Service delivery 
- Applications (e.g. data monetization, customer experience, credit scoring)

The idea is to provide organizations with an identity-as-a-service solution that leverages the concept of self-sovereign identity. The properties of this wholesome identity management solution should meet the 10 principles listed in Christopher Allen & Shannon Appelcline’s paper [A Primer on Self-Sovereign Identity](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/self-sovereign-identity-primer.md), so as to ensure users rights: 
> Existence. Users must have an independent existence. 
> Control. Users must control their identities. 
> Access. Users must have access to their own data. 
> Transparency. Systems and algorithms must be transparent. 
> Persistence. Identities must be long-lived. 
> Portability. Information and services about identity must be transportable. 
> Interoperability. Identities should be as widely usable as possible. 
> Consent. Users must agree to the use of their identity. 
> Minimalization. Disclosure of claims must be minimized. 
> Protection. The rights of users must be protected.

I suggest the addition of three design principles to incorporate organization’s needs:

- **Simplicity.** Companies must find it easy to integrate the service within their existing processes and legacy systems. 
- **Flexibility.** Different users may have different sets of attributes. Individuals may decide what attributes they want to append and companies what attributes they need to request. Moreover, some attribute classes may only make sense in specific regions or different regulations may apply. Allowing for local libraries of attributes can help expand access.
- **Validation.** Attributes should be verifiable by third parties. They may be user-provided and not validated, user-provided and externally validated or externally provided and user accepted. 

In summary, for a new identity management architecture to succeed in the rooted business model underlying the digital economy, we must first understand the challenges faced by all players in the market and incorporate these in our design principles. Next steps shall include validating priorities for organizations, identifying the properties of a full stack, and testing a vertical solution. 
