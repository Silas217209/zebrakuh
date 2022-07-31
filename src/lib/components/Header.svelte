<script>
  import header from "$lib/assets/img/header.webp";
  import header_mobile from "$lib/assets/img/header_mobile.webp";
</script>

<div class="header">
  <picture>
    <source media="(max-width:700px)" srcset={header_mobile} />
    <!-- svelte-ignore a11y-img-redundant-alt -->
    <img class="header-image" src={header} alt="header-image"/>
  </picture>
</div>
