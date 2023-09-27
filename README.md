# The Open Commerce Protocol (OCP)
OCP is a shared set of communication standards for commercial transactions. OCP is an industry-agnostic, interoperable, open protocol connecting any buyer and any seller across any industry to engage in permissionless, location-aware transactions. 

## Developers
The OCP specification defines a standard, technology-agnostic API description that allows any application to discover new commercial services without requiring api keys, source code access, additional documentation, or integrations with ad-hoc services. When properly defined, a software application can interpret and transact with remote services with a very minimal amount of implementation overhead.

Developers can use OCP to build new consumer marketplace applications without having to think about acquiring customers, hiring a sales team, or talking to a sales rep to acquire access to necessary infrastructure.

## Contributing
- A community-curated list of OCP-related projects, core working groups, and collaborators lives [here](./docs/CONTRIBUTORS.md).
- To make contributions to the protocol, please see our [guidlines](./docs/GUIDLINES.md).

## OCP - Core Specification
Every commercial transaction follows the same standard series of order lifecycle API requests. This specification standardizes this lifecylce through a series of 4 stages:

#### Discovery APIs
This is the stage where a Buyer searches or explores the 
product(s) or service(s) they intend to purchase from a Seller. 

The Buyers intent is typically defined by a Client application performing a 
specific function, like food delivery. The Explore API enables a Buyer to 
query the network with their Intent. The Explore API has a callback mechanism 
that returns a Catalog which includes a selection of Sellers offering the 
intended product(s) or service(s). 

The discovery process requires both a query to the registry contract and an 
API request to at least 1 server.

#### Order APIs
This is the stage where the Buyer creates an order for the 
selected product(s) or service(s). The Buyer selects the Item(s) and/or Offer(s)
they plan to purchase from the Seller, establishing a direct connection with 
an `SSN`, and broadcasting their intent to purchase.

#### Fulfillment APIs
This is the stage where the Seller processes the order, 
packages the product(s), and, if applicable, ships them to the Buyer’s specified
delivery address. Order fulfillment broadly represents the event when a 
Buyer receives the Item(s) from a Seller.

#### Post-fulfillment APIs
This is the stage where the Buyer receives the 
Item(s), and inspects the Item(s). In this stage, the Buyer may provide 
feedback, require customer support, or initiate a return/refund if 
dissatisfied.

## Testing 
When editing, test to ensure schemas are validd by running the following command in your terminal:
```sh
swagger-cli bundle postman/schemas/index.yaml --outfile api/api.yaml --type yaml
```
