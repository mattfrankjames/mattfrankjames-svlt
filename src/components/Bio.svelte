<script>

import { dataset_dev } from "svelte/internal";

</script>
<style>
  div {
    align-items: center;
    display: flex;
  }

  img {
    width: 100px;
    height: 100px;
    border-radius: 100px;
    /* border: 3px solid #fd6378; */
    display: block;
    margin-right: 20px;
  }

  p {
    font-size: 1.125rem;
  }
</style>

<div>
  <img src="profile-pic.jpg" alt="Matt James">
  <p>
    Hi, I'm <strong>Matt</strong>. I'm a husband, dad, cyclist and front-end developer from St. Louis, MO.
    You can follow me on <a href="https://www.twitter.com/mattfrankjames" target="_blank">Twitter</a>,
    see some of my work on <a href="https://www.github.com/mattfrankjames" ortarget="_blank">GitHub</a>.
  </p>
</div>
