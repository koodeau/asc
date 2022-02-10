<script>
  /**
   * @slot {{
   * actions: {
   *  create: (url: string) => Promise<object>;
   *  complete: (user: string, secret: string) => Promise<object>;
   * }
   * }}
   */
  import { createEventDispatcher } from "svelte";
  import { active } from "../stores";
  import { Appwrite } from "$lib/appwrite";

  const dispatch = createEventDispatcher();
  const actions = {
    create: async url => {
      try {
        const response = await Appwrite.account.createVerification(url);
        dispatch("successCreate", response);
        return response;
      } catch (error) {
        dispatch("failureCreate", error);
        throw error;
      }
    },
    complete: async (user, secret) => {
      try {
        const response = await Appwrite.account.updateVerification(
          user,
          secret
        );
        dispatch("successComplete", response);
        return response;
      } catch (error) {
        dispatch("failureComplete", error);
        throw error;
      }
    },
  };
</script>

{#if $active}
  <slot {actions} />
{/if}
