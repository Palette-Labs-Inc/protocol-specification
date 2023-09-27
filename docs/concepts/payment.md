# Payment terms, and Payment settlement in server-to-server communications

The `SSN` should implement an endpoint.

```js
const stripe = require('stripe')('sk_test_xxxxxxxxxxxxx');
// This example sets up an endpoint using the Express framework.
// Watch this video to get started: https://youtu.be/rPR2aJ6XnAc.
app.post('/payment_sheet', (req, res) => {
  const cartId = req.body.cartId;
  const customer = req.body.customer;
  //

  // Use an existing Customer ID if this is a returning customer.
  const customer = await stripe.customers.create();
  const ephemeralKey = await stripe.ephemeralKeys.create(
    {customer: customer.id},
    {apiVersion: '2023-08-16'}
  );


    //The SSN should find the cart total based on the cartId in the query params.
    // For example, using a cart service in an example backend.
    const cart = await this.cartService.findCart({
      where: {
        id: cartId,
      },
      select:{
        total_amount: true // total_amount in cents
        currency: true
      }
    })

  const paymentIntent = await stripe.paymentIntents.create({
    amount: cart.total_amount,
    currency: cart.currency,
    customer: customer.id,
    // In the latest version of the API, specifying the `automatic_payment_methods` parameter is optional because Stripe enables its functionality by default.
    automatic_payment_methods: {
      enabled: true,
    },
  });

  //The SSN should connect the payment intent id to the cart. When the `payment_intent.succeeded` webhook event occurs from Stripe, this identifier will be used to query the relevant cart. When the cart is found, the contents will be used to create an order object that is forwarded to the `BSN` via webhook.
    await this.cartService.connectPaymentIntent({
      where: {
        id: cartId,
      },
      connect: {
        paymentIntentId: paymentIntent.id
      }
    })

  res.json({
    paymentIntent: paymentIntent.client_secret,
    ephemeralKey: ephemeralKey.secret,
    customer: customer.id,
    publishableKey: 'pk_test_xxxxxxxxxxxxxxx'
  });
});
```

The `BSN` should inform the customer when the payment is done (for example, by displaying an order confirmation screen).

```js
export default function CheckoutScreen() {
  const openPaymentSheet = async () => {
    const { error } = await presentPaymentSheet();

    if (error) {
      Alert.alert(`Error code: ${error.code}`, error.message);
    } else {
      Alert.alert('Success', 'Your order is confirmed!');
    }
  };

  return (
    <Screen>
      <Button
        variant="primary"
        disabled={!loading}
        title="Checkout"
        onPress={openPaymentSheet}
      />
    </Screen>
  );
}
```

The `SSN` will recieve a `payment_intent.succeeded` event when the payment completes. Upon receiving this webhook, The `SSN` should send the `BSN` a confirmation via a webhook and begin fulfillment of the order.