<script>
  import header from "$lib/assets/img/header.webp";
  import header_mobile from "$lib/assets/img/header_mobile.webp";
</script>

<div class="header">
  <picture>
    <source media="(max-width:700px)" srcset={header_mobile} />
    <img class="header-image" alt="header image" src={header} />
  </picture>
</div>
