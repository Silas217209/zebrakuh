<script context="module">
    export async function load({ params, fetch }) {
      const url = `https://wp.zebrakuh.com/wp-json/wp/v2/pages/13`;
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
  <p>{@html page.content.rendered}</p>