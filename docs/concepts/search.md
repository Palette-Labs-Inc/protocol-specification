## Search Intent

This document pertains to the intent of purchasing or utilizing a product or service. The Buyer Supporting Node (BSN) allows consumers to declare their intentions, which include:

- What they desire (product, service, offer)
- Whom they require (seller, service provider, delivery agent, etc.)
- Where they wish to obtain or fulfill the purchase order
- When they need it (start and end times for dispatched orders)

This encompasses properties such as a search string, provider, fulfillment, category, item, etc. Typically, the BSN uses this information to communicate the user's search intent to the SSN. Subsequently, the SSN uses this information to identify products or services within its offerings that align with the user's intent.

For instance, in a ridshare application, a consumer declares their intent, specifying various aspects of their intended journey:

- Starting location for their journey (intent.fulfillment.start.location)
- Ending location for their journey (intent.fulfillment.end.location)
- Desired start time (intent.fulfillment.start.time)
- Desired end time (intent.fulfillment.end.time)
- Passenger information (intent.fulfillment.customer)