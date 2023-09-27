# Research 
- [ ] Payments, settlements, and trust in distributed systems
- [ ] Registry infrastructure
- [ ] Dispute resolution in distributed systems / Decentralized arbitration processes (Kleros, Aragon Court)
- [ ] Universal Identities and persistent paymethods across Mobile Clients. 
    - Stripe Payment Intents originate in `SSN`. Customers can be attached to the PaymentIntent in order to pre-populate prior paymethods and default addresses. This works in a centralized system because a single entity has both Merchant and Customer data available. How to have identities that are universally available? Stripe connect allows for [cloning](https://stripe.com/docs/connect/cloning-customers-across-accounts) customers with stripe connect but this would mean a central org would need to host a global parent account. Stripe documents a similar but meaningfully different issue in the link above: "For some business models, it’s helpful to reuse your customers’ payment information across connected accounts. For example, a customer who makes a purchase from one of your connected sellers shouldn’t need to re-enter their credit card or bank account details to purchase from another seller."
        - [`merchantIdentifiers`](https://stripe.com/docs/payments/accept-a-payment?platform=react-native&ui=payment-sheet#stripe-initialization) are required for for Apple Pay. This means that no `BSN` will be able to enable Apple Pay because they will not have access to the `SSN`'s `merchantIdentifier` configuration unless it is displayed in the registry. If this is going to be listed in a public ledger, this has implications for security and onboarding requirements for Server/Node administrators.
 - [ ] How to display a single Payment Sheet (supporting a single credit card charge) to a Customer if the `SSN` does not provide courier services?
    - The `SSN` could request a courier from another `SSN` and include the affiliated fees and TTL in the fees array of the Cart response body - updating their node in the registry to provide both Merchant and Courier services.
    - The `BSN` could query both a merchant supporting `SSN` and a courier supporting `SSN` and handle the payments, the `SSN` could then send an invoice for the services. In this case, we would need a "negotiation" settlment gateway to facilitate payments and payouts. 
    - The `SSN` 
    - Completely rethink payment infrastructure or implement a payment gateway service that handles payments and payouts to involved parties.
    - If this is left up to the `BSN` it could introduce complexities. The `BSN` would have to self-manage Orders and their affiliated fulfillment orders on their own server. 
- [ ] Decentralized reputation. If reviews are sent to an `SSN`, the `SSN` may manipulate the data to increase order frequency to their server.
 - [ ] Decentralized Identity. It would be nice to have something like [ENS](https://app.ens.domains/) but that would be bad to have addresses stored on ENS in public.

# API Design
- [ ] Draft Order / Purchase APIs.
- [ ] Draft Fulfillment APIs.
- [ ] Draft Post-Fulfillment APIs.
- [ ] Draft Dispatch APIs.
- [ ] Discount / Offer methods in Cart
- [ ] A Notion of Tips in Cart (may vary depending on services provided). 
- [ ] Connect a customer to an `SSN`
- [ ] Draft `BSN` Customer specification. Must be defined by protocol spec b/c email and phone are required inputs for many shipment / delivery services for tracking, etc.
- [ ] Draft `BSN` CustomerAddress specification. Must be defined by protocol spec b/c addresses are required inputs for many shipment / delivery services.
- [ ] Draft a /GET product media endpoint. 
- [ ] Add multi-media support for `Catalog`s, `CatalogItem`s, etc. Multi-media allows for a more diverse and immersive set of Mobile Clients. Once done, design advanced `CatalogSearch` that can query for `CatalogItem`s with specific mediaTypes.
- [ ] Draft terms and policies concepts.
- [ ] Draft customer support concepts / APIs.

 
# Engineering
- [ ] V1 reference applications
- [ ] Square-like API explorer
- [ ] Multi-language support for generated SDKs (node, go, python.)