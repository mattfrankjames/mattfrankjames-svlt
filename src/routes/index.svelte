<script context="module">
  export function preload({ params, query }) {
    return this.fetch(`blog.json`)
      .then((r) => r.json())
      .then((posts) => {
        return { posts };
      });
  }
</script>

<script>
  export let posts;
</script>

<style>
  .home-container {
    align-items: center;
    justify-content: center;
    margin: 2em 0;
    min-height: 400px;
  }

  h1 {
    font-weight: 700;
    margin-bottom: 0.5em;
  }

  p {
    font-size: 1.4em;
    line-height: 1.5;
  }

  figure {
    margin: 0;
    text-align: center;
    align-self: flex-start;
  }

  figcaption {
    font-size: 0.8em;
    font-style: italic;
  }

  img {
    width: 100%;
    background: #aeaaaa;
    border-radius: 10px;
  }
  h2,
  .post-item-footer {
    font-family: 'Kanit', sans-serif;
    font-weight: 700;
  }
  h2 {
    margin-top: 0.75em;
  }
  .post-item-date {
    color: var(--color-tertiary);
    text-align: left;
    text-transform: uppercase;
    margin-right: 16px;
  }

  hr {
    margin: 30px auto;
  }

  .home-container__posts--top-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 1em;
  }
  .home-container__posts--top-row h2 {
    margin-top: 0;
    font-size: 2.4em;
  }
  .home-container__btn {
    padding: 0.75em 1.5em;
    color: var(--color-primary);
    background-color: var(--color-secondary);
    border: 1px solid #34e4f6;
    box-shadow: 2px 3px var(--color-primary);
    text-decoration: none;
    transition: color 0.2s, background-color 0.2s, box-shadow 0.2s;
    transform: translate(0, 0);
  }
  .home-container__btn:hover {
    background-color: var(--color-primary);
    color: var(--color-secondary);
    border: 1px solid var(--color-secondary);
    box-shadow: 2px 3px #34e4f6;
  }
  .home-container__btn:active {
    box-shadow: 0 0 var(--color-secondary);
    transform: translate(1px, 3px);
  }

  .post-item {
    grid-column: 1/3;
  }
  @media (max-width: 1020px) {
    p {
      font-size: 1.2em;
    }

    /* img {
      max-width: 300px;
    } */
  }

  /* @media (max-width: 0px) {
    .home-container {
      flex-direction: column;
    }

    .home-copy {
      flex: 0;
      padding-bottom: 2em;
    }
  } */
  @media (min-width: 760px) {
    .home-container {
      display: grid;
      gap: 1.5em;
      grid-template-columns: 1.5fr 2fr;
    }
    .home-container__posts {
      display: grid;
      grid-column: 1/3;
      grid-template-columns: 1.5fr 2fr;
      grid-template-columns: subgrid;
    }
    img {
      padding: 1em;
    }
  }
  span {
    font-weight: bold;
  }
</style>

<svelte:head>
  <title>Matt Frank James</title>
</svelte:head>

<div class="home-container">
  <figure>
    <img alt="Person typing on laptop" src="undraw_biking_kc4f.svg" loading="lazy" />
    <figcaption>
      Illustration thanks to
      <a href="https://undraw.co" rel="noopener noreferrer" target="_blank">Undraw</a>
    </figcaption>
  </figure>
  <div class="home-copy">
    <h1>Hi. I'm Matt James, a front-end engineer, teacher and family man.</h1>

  </div>

  <div class="home-container__posts">
    <div class="home-container__posts--top-row">
      <h2>Latest</h2>
      <a class="home-container__btn" rel="prefetch" href="blog">
        Archive&nbsp;
        <span aria-hidden="true">&#x3e;</span>
      </a>
    </div>
    {#each posts as post, index}
      <div class="post-item">
        {#if index}
          <hr />
        {/if}
        <h2>
          <a rel="prefetch" href="blog/{post.slug}">{post.title}</a>
        </h2>
        <p>{post.excerpt}</p>
        <div class="post-item-footer">
          <span class="post-item-date">— {post.printDate}</span>
        </div>
      </div>
    {/each}
  </div>
</div>
