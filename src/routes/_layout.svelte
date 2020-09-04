<script>
  import Header from '../components/Header.svelte';

  export let segment;
</script>

<style>
:root {
  --color-primary: #36393b;
  --color-secondary: white;
}
@media (prefers-color-scheme: dark) {
  :root {
    --color-primary: white;
    --color-secondary: #36393b;
  }
}
  .layout {
    display: flex;
    flex-direction: column;
    min-height: 100%;
    min-height: 100vh;
  }

  main {
    flex: 1;
    position: relative;
    margin: 0 auto;
    max-width: 1080px;
    background-color: var(--color-secondary);
    padding: 1em 2em;
    box-sizing: border-box;
    width: 100%;
    display: flex;
    flex-direction: column;
  }

  footer {
    color: var(--color-primary);
    font-size: 1em;
    font-family: 'Kanit', sans-serif;
    margin: 1em auto;
    max-width: 1400px;
    padding: 1em 2em;
    text-align: center;
    width: 100%;
  }
</style>

<div class="layout">
  <Header {segment}/>

  <main>
    <slot></slot>
  </main>

  <footer>
    <span>
      &copy; {new Date().getFullYear()} Matt Frank James.
      Powered by <a href="https://sapper.svelte.dev" target="_blank" rel="noopener noreferrer">Sapper</a>.
      Template by <a href="https://www.twitter.com/Charca" target="_blank" rel="noopener noreferrer">Maxi Ferreira</a>.
    </span>
  </footer>
</div>
