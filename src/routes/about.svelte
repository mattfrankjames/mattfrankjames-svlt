<style>
  img {
    border-radius: 8px;
    grid-column: 2/3;
  }
  .content-wrapper {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1em;
  }
  .content-wrapper__text-block {
    grid-column: 1/2;
    grid-row: 1/2;
  }
  @media (max-width: 1020px) {
    .content-wrapper {
      grid-template-columns: 1fr;
    }
    img {
      grid-column: 1/2;
    }
  }
</style>

<svelte:head>
  <title>Matt Frank James | About</title>
</svelte:head>

<div class="container">
  <h1>About Me</h1>
  <h2>Hi There.</h2>
  <div class="content-wrapper">
    <img src="/profile-pic.jpg" loading="lazy" alt="Matt James" />
    <div class="content-wrapper__text-block">
      <p>My name is Matt James and I make things on the web.</p>
      <p>
        I've followed a long and circuitous path to come to the point that I am at today. I have
        been involved in media communications for over twenty years and began my foray into
        interactive media and design roughly a decade ago. When I'm not developing for the web or
        designing and photographing for local startups, I can be found chasing kids, riding bikes
        and playing outside. Get in touch:
        <a href="mailto:mattjamesmedia@gmail.com">mattjamesmedia@gmail.com</a>
      </p>
    </div>
  </div>
</div>
