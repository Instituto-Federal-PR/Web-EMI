// https://dev.to/oieduardorabelo/svelte-3-guia-para-o-desenvolvedor-react-impaciente-52i5

<script>
  import { onMount } from "svelte";

  export let url = "https://academy.valentinog.com/api/link/";
  export let searchTerm = undefined;
  let jsonResponse = [];

  $: regex = new RegExp(searchTerm, "gi");

  $: data = searchTerm
    ? jsonResponse.filter(element => element.title.match(regex))
    : jsonResponse;

  onMount(async function() {
    const response = await fetch(url);
    const json = await response.json();
    jsonResponse = json;
  });
</script>

<slot {data} />
