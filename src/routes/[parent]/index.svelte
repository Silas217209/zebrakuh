<script context="module">
  export async function load({ params, fetch }) {
    const url = `https://wp.zebrakuh.com/wp-json/wp/v2/pages?slug=${params.parent}`;
    const response = await fetch(url);

    return {
      status: response.status,
      props: {
        page: response.ok && (await response.json()),
      },
    };
  }
</script>
<script>
    export let page
</script>
<p>{@html page[0].content.rendered}</p>