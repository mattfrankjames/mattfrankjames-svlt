---
title: Connected Stripe Accounts with Ember Octane
date: '2020-08-28T09:12:03.284Z'
---

Taking payments on the web can be tricky. Both the need to consider the security of the end user and the complexities of implementation as a developer mean that commerce can present a particular challenge when building web apps. Luckily, Stripe has made the process as close to painless as possible. While it's easy to find resources on how to accept direct payments, and even payments on behalf of a single third party account, it's much less straightforward when accepting payments on behalf of multiple accounts. Even less so if your development stack is based on Ember Octane. Let's dig in and look at how to get this done.

<!-- more -->

Taking payments on the web can be tricky. Both the need to consider the security of the end user and the complexities of implementation as a developer mean that commerce can present a particular challenge when building web apps. Luckily, Stripe has made the process as close to painless as possible. While it's easy to find resources on how to accept direct payments, and even payments on behalf of a single third party account, it's much less straightforward when accepting payments on behalf of multiple accounts. Even less so if your development stack is based on Ember Octane. Let's dig in and look at how to get this done.

## The Payment Intents API

The first step is to get an endpoint set up on your server that maps to the Stripe [payment intents API](https://stripe.com/docs/payments/payment-intents). Once that crucial piece of infrastructure is in place, you will be able to use Ember data to look up records containing the connected account IDs of the accounts you will be accepting payments on behalf of. This will also allow you to pass along card and charge amount information to Stripe.

Now that the foundation is in place, let's take a look at what needs to happen on the front-end.

Before getting our components set up, we first need to initialize Stripe in our `config/environment.js` file by adding this to the `APP` property.

```js
stripe: {
  lazyLoad: true,
},
```

If you are only accepting payments on behalf of one account, you can set your Stripe `publishableKey` and `stripeOptions.stripeAccount` number here. However, with multiple accounts to consider, lazyloading stripe will give us the flexibility to dynamically lookup connected account numbers at the point of purchase.

Now that we have our initial Stripe configuration in place, we're going to need a component to handle the payments themselves. Luckily, Stripe has a collection of [Stripe Elements](https://stripe.com/docs/stripe-js) to do most of the heavy lifting for us with validation and processing. Even better, there is an [adopted Ember addon](https://github.com/adopted-ember-addons/ember-stripe-elements) that wraps those elements for use within Ember. Once we install the Ember addon using `ember-cli`, we can invoke it in our template.

```html
<form class="form--payment" id="payment-form" {{on 'submit' (fn this.submitPayment stripeElement)}}>
  <StripeCard @onChange={{this.setStripeElement}}/>
  <button type="submit" class="btn--primary" id="stripe-payment">Submit Payment</button>
</form>
```

So, what's the deal with that `this.setStripeElement` action we're passing in to the component? When submitting the payment to Stripe, it's important to indicate which specific Stripe element the payment information is being collected from, as demonstrated by the `{{on 'submit'}}` action on the `<form>` element. We can do that in our component class using an Ember `@tracked` property.

```js
import { tracked } from '@glimmer/tracking';
@tracked stripeElement;
@action
  setStripeElement(stripeElement) {
    this.stripeElement = stripeElement;
  }
```

All this is well and good, but we also need to set up the `@action` to submit our payment to Stripe. Let's take a look at the entire component class.

```js
import { action } from '@ember/object';
import { inject as service } from '@ember/service';
import Component from '@glimmer/component';
import { tracked } from '@glimmer/tracking';

export default class PaymentFormComponent extends Component {
  @tracked stripeElement;
  @service stripev3;
  @service store;

  @action
  setStripeElement(stripeElement) {
    this.stripeElement = stripeElement;
  }
  @action
  async submitPayment(stripeElement, event) {
    event.preventDefault();
    const stripe = this.stripev3;
    const paymentIntent = this.store.createRecord('stripe-payment-intent', { amount: 60 });
    // The amount will be dynamic and come from the Stripe element
    await paymentIntent.save();
    const { clientSecret } = paymentIntent;
    const result = await stripe.confirmCardPayment(clientSecret, {
      payment_method: {
        card: stripeElement,
        billing_details: {
          name: 'Customer Name', // This will be collected from the form
        },
      },
    });
  }
}
```

Here, we're saving a record to our `stripe_payment_intent` endpoint with the amount we intend to charge. From there, we're destructuring the `clientSecret` off the record we create and calling `.confirmCardPayment` on the `stripe` service we've injected from the addon. Stripe handles the rest for us.

Of course, we'll need access to the account number for our connected account so we can pass it along when we initialize Stripe with `stripe.load`. This will be done in the `beforeModel()` hook of our route file as we've set Stripe to lazy load in our `config/environment.js` file.

```js
import Route from '@ember/routing/route';
import { inject as service } from '@ember/service';
export default class StripePaymentRoute extends Route {
  @service stripev3;
  async beforeModel() {
    const stripe = this.stripev3;
    const { id } = await store.queryRecord('user', {
      /*whatever your api provides*/
    });
    return stripe.load('your stripe account number', {
      locale: 'en',
      stripeAccount: id,
    });
  }
}
```

With all of that in place, we're now in a position to retrieve whichever connected Stripe account we need to charge and are in a position to support however many connected accounts that we need in our parent organization. With this kind of flexibility and built in functionality from both Stripe and Ember, our platform can grow and evolve into a thriving marketplace on the web.

<a onclick="document.location.hash='top';" href="javascript:;">[Top]</a>
