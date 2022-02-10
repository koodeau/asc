<script>
  /**
   * @slot {{
   * actions: {
   *  delete: () => Promise<object>;
   * }
   * }}
   */
  import { createEventDispatcher } from "svelte";
  import { active } from "../stores";
  import { Appwrite } from "$lib/appwrite";

  const dispatch = createEventDispatcher();
  const actions = {
    delete: async () => {
      try {
        const response = await Appwrite.account.delete();
        dispatch("success", response);
        return response;
      } catch (error) {
        dispatch("failure", error);
        throw error;
      }
    },
  };
</script>

{#if $active}
  <slot {actions} />
{/if}
