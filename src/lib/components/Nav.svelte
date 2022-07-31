<script>
  import { page } from "$app/stores";
  import arrow from "$lib/assets/img/expand.webp";

  export let nav;
  const url = `https://wp.zebrakuh.com/wp-json/menus/v1/menus/main/`;
  fetch(url)
    .then((response) => response.json())
    .then((res) => {
      nav = res
    });
    $: open = nav.items.map((item) => {
      return false
    });
    function toggleopen(i) {
      open[i] = !open[i]
    }
</script>

{#if nav}
  <ul id="menulist">
    <li class="parent">
      <a
        class="sidebar-nav-item"
        class:active={$page.url.pathname === "/"}
        href="/">Home</a
      >
    </li>
    {#each nav.items as item, index}
      <li class="parent">
        <a
          class="sidebar-nav-item"
          class:active={$page.url.pathname.includes(item.slug)}
          href={`/${item.slug}/`}>{item.title}</a
        >
        {#if item.child_items}
          <img on:click={() => toggleopen(index)} alt="expand menu" src={arrow} class="expand sidebar-nav-item" class:open={$page.url.pathname.includes(item.slug) || open[index]} />
          <ul class="submenu" style={`height: ${$page.url.pathname.includes(item.slug) || open[index] ? (item.child_items.length * 19) : 0}px`} class:open={$page.url.pathname.includes(item.slug) || open[index]}>
            {#each item.child_items as subitem}
              <li class="child">
                <a
                  class="sidebar-nav-item" class:active={$page.url.pathname.includes(subitem.slug)}
                  href={`/${item.slug}/${subitem.slug}/`}>{subitem.title}</a
                >
              </li>
            {/each}
          </ul>
        {/if}
      </li>
    {/each}
  </ul>
{/if}
