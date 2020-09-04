---
title: Simplify Your Ember App with Domain Components
date: '2020-09-03T22:12:03.284Z'
---

As one of the elder statemen in the JavaScript framework landscape, Ember has been around for a long time. While it has fallen out of favor somewhat over the last few years with rise of React, Vue and Svelte, Ember is still very much alive and has been completely overhauled with the recent release of Ember Octane. If you find yourself coming to Ember from another framework, it can be a bit daunting at first. But, by leveraging Octane to create an architecture built on _domain components_, things start to feel much more familiar. Let's dig in.

<!-- more -->

As one of the elder statemen in the JavaScript framework landscape, Ember has been around for a long time. While it has fallen out of favor somewhat over the last few years with rise of React, Vue and Svelte, Ember is still very much alive and has been completely overhauled with the recent release of Ember Octane. If you find yourself coming to Ember from another framework, it can be a bit daunting at first. But, by leveraging Octane to create an architecture built on _domain components_, things start to feel much more familiar. Let's dig in.

Before we go any farther, let's define what we're talking about when we use the term "domain components". If you are coming from another framework like React, you're probably familiar with the concept of smart components versus dumb components. Typically, all of your business logic would take place in the "smart" components - data filtering, conditional content, etc. while the "dumb" components would have the sole responsibility of displaying content and rendering the "smart" components. In my current role, our organization refers to these "smart" components in Ember as "domain components".

If you've been an Ember developer for a while, you may have grown accustomed to setting up this business logic within a controller. While this is still an effective way to work, many developers less versed in Ember-isms may find the added layer of complexity a bit confusing. With domain components, we can move that functionality directly into the component and come much closer to replicating the behavior of other frameworks. Let's look at an example.

First, we're going to need to grab some data from our API. In Ember, this typically takes place in the `model()` hook of a route file.

```js
async model() {
  const { store } = this;
  const promotionProducts = await store.query('promotion-product', {
    // whatever params you need go here
  });
  const promotionProduct = promotionProducts.firstObject;
  return {
    promotionProduct,
  };
}
```

Now that we have all the data associated with our single `promotionProduct`, we need to make it available to our template.

```HTML
<!-- app/templates/index.hbs -->
<div class="page-wrapper">
  <PaymentStatus @promotionProduct={{@model.promotionProduct}}/>
</div>
```

Here is where the domain component comes into play. The template file for this route exists only to invoke the domain component. The domain component has a `@promotionProduct` argument that receives the data fetched in the route's `model()` hook. The argument can be named anything, but I find a little less mental overhead if the argument name matches what's returned from the `model()`.

With the data now passed in to the component, let's define some properties in the component's JS file that we'll use in it's template.

```js
export default class PaymentStatusComponent extends Component {
  get price() {
    return this.args.promotionProduct.price;
  }
  get paymentPeriodHasEnded() {
    return Date.now() > this.args.promotionProduct.purchaseEndDate;
  }
  get paymentPeriodIsActive() {
    return (
      this.args.promotionProduct.purchaseStartDate < Date.now() &&
      Date.now() < this.args.promotionProduct.purchaseEndDate
    );
  }
}
```

As a quick aside, if you're coming from React, think of `args` just like `props`.

Now that we've filtered the data in the JS to get what we need, we can make use of the properties to conditionally display content within the component's template.

```HBS
{{if this.paymentPeriodIsActive}}
  <h2>$ {{this.price}}</h2>
  <button type="button" class="ssButton ssButtonPrimary template-color-primary-background-color">Pay Now</button>
{{/if}}
{{#if this.paymentPeriodHasEnded}}
  <h2>{{i18n-t "unavailable"}}</h2>
  <div class="payment-status--inactive">
    <p>No longer accepting payments.</p>
  </div>
{{/if}}
```

And with that, we've moved our business logic into a component that handles the display of data, leaving our route template the simple task of rendering components. By leveraging the power of domain components, we've made sure that we've separated the concerns of our app and removed one step in the hot potato'ing of the data we need to render our content. Even better, we've taken a much needed step toward aligning Ember's implementation more with newer frameworks, meaning that it will be much more straightforward to onboard new developers come to Ember and get them up and running quickly.
