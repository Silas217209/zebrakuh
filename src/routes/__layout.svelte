<script context="module">
    export async function load({ params, fetch }) {
      const url = `https://wp.zebrakuh.com/wp-json/menus/v1/menus/main`;
      const response = await fetch(url);
  
      return {
        status: response.status,
        props: {
          navdata: response.ok && (await response.json()),
        },
      };
    }
  </script>

<script>
  import "$lib/assets/css/burgers.scss";
  import "$lib/assets/css/style.scss";
  import Header from "$lib/components/Header.svelte";
  import Nav from "$lib/components/Nav.svelte";
  import Footer from "../lib/components/Footer.svelte";

  export let navdata
  let open = false
  function toggleopen() {
    open = !open
  }
</script>

<Header />
<div id="content" class="body">
  <button
    class="hamburger hamburger--collapse"
    class:is-active={open}
    id="hamburger"
    type="button"
    aria-controls="menu"
    aria-label="menu toggle"
    on:click={toggleopen}
  >
    <span class="hamburger-box">
      <span class="hamburger-inner" />
    </span>
  </button>
  <div class="menu" class:is-open={open} id="menu">
    <Nav nav={navdata}/>
  </div>
  <div class="content" id="main-content">
    <main>
      <slot />
    </main>
  </div>
</div>
<Footer />
