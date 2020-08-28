<script>
  import { dataset_dev } from 'svelte/internal';
</script>

<style>
  div {
    align-items: center;
    display: grid;
    grid-template-columns: 100px 1fr;
    gap: 16px;
  }

  img {
    width: 100px;
    height: 100px;
    border-radius: 100px;
    object-fit: cover;
    /* border: 3px solid #34e4f6; */
    display: block;
    margin-right: 20px;
  }

  p {
    font-size: 1.125rem;
  }
</style>

<div>
  <img src="profile-pic.jpg" loading="lazy" alt="Matt James" />
  <p>
    Hi, I'm
    <strong>Matt</strong>
    . I'm a husband, dad, cyclist and front-end developer from St. Louis, MO. You can follow me on
    <a href="https://www.twitter.com/mattfrankjames" target="_blank" rel="noopener norefferer">
      Twitter
    </a>
    or see some of my work on
    <a href="https://www.github.com/mattfrankjames" target="_blank" rel="noopener norefferer">
      GitHub
    </a>
    .
  </p>
</div>
