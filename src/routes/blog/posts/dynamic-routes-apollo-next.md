---
title: Dynamic Routing with Next JS and Apollo
date: "2020-03-02T22:12:03.284Z"
---

Let's say your working on a headless ecommerce site and you need to put together a flexble component that can reference different product ids to populate a specific product page. Your store has thousands of products, so you're going to need something flexible to handle the volume.

<!-- more -->

Luckily, Next JS makes this process pretty straight forward. First, set up your links using both the `as` and `href` props.

```JS
<Link href='/collections/[...id]' as='/collections/401'>
  <a>Women</a>
</Link>
```

Here, this `<Link>` is pointing to a page that lives in the `/pages/collections/[id].js` path in your Next JS project. The `[id].js` naming convention is what enables dynamic routing within Next JS.

Within the `[id].js` file, were going to need to define a query using Apollo that takes an id as a variable. That way, when the time comes, we'll be able to reference the id from our URL to retrieve the specific product or collection.

```JS
const PRODUCTS_QUERY = gql`
  query PRODUCTS_QUERY($id: String!) {
    products(filter: { category_id: { eq: $id } }) {
      total_count
      items {
        name
        sku
        image {
          url
          label
        }
        description {
          html
        }
        price {
          regularPrice {
            amount {
              value
            }
          }
        }
      }
    }
  }
`;
```

This query is going to pull in all the info that we want to display in our product collection, specifically, the name, sku, image, desciption and price.

Next, we're going to need to define a component that can make use of the data returned from the query, utilizing the new `useQuery` hook from the `react-apollo` package. In this component, we'll pass in our ID as a variable to the query, so the one query and one collection component can display whatever product collection we want based on the route.

```JSX
function PLP({ id }) {
  const { data = {}, loading, error } = useQuery(PRODUCTS_QUERY, {
    variables: { id },
  });
  if (loading || data === 'undefined') return <div />;
  return (
    <Layout>
      <h1>All Women&rsquo;s</h1>
      <div className="page__wrap--twoCol">
        <ul className="page__grid">
          <ErrorBoundary>
            {Object.keys(data.products.items).map(key => (
              <li key={key} className="card">
                <Link
                  key={key}
                  href="/products/[id]"
                  as={`/products/${data.products.items[key].sku}`}
                >
                  <a>
                    <h4>Brand Collection Title</h4>
                    <strong>{data.products.items[key].name}</strong>
                    <span className="cat__subTitle">Category Title</span>
                    <span>
                      {data.products.items[key].price.regularPrice.amount.value}
                    </span>
                  </a>
                </Link>
              </li>
            ))}
          </ErrorBoundary>
        </ul>
      </div>
    </Layout>
  );
}
```

But how does the component access the `id` prop? When someone follows our `<Link>` to a product page, we'll use the `getInitialProps` method and destructure the `id` off the query object that comes from the URL like so:

```JS
PLP.getInitialProps = function(ctx) {
  const { id } = ctx.query;
  return { id };
};
```
Now, we're all set to reference any collection `id` within the `as` prop on `<Link>` components throughout the site to seamlessly create product listing pages for any collection defined in our backend's schema.

With Next JS and Apollo, we now have the ability to leverage any headless CMS to put together dynamically capable, server rendered apps to provide a modern UX for our customers.
