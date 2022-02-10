<script>
  import { onMount } from "svelte";
  import { active } from "./stores";
  import { Appwrite } from "appwrite";

  const sdk = new Appwrite();

  /** @type {string} */
  export let endpoint;
  /** @type {string} */
  export let project;
  export let locale = "en";

  onMount(() => {
    if (endpoint == "") {
      console.error("Endpoint must be set.");
      return;
    }
    if (project == "") {
      console.error("Project ID must be set.");
      return;
    }

    sdk 
.setEndpoint(endpoint) // Your API Endpoint 
.setProject(project) // Your project ID ;
.setLocale(locale)
    active.set(true);
  });
</script>

{#if $active}
  <slot />
{/if}
