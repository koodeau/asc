<script>
  /**
   * @slot {{
   * actions: {
   *  create: (file: any, read?: string[], write?: string[]) => Promise<object>;
   * }}}
   * @slot {{ error: object }} error
   */
   import { Appwrite } from "$lib/appwrite";

  import { createEventDispatcher } from "svelte";
  import { currentUser } from "../stores";

  const dispatch = createEventDispatcher();

  const actions = {
    create: async (
      file,
      read = [`user:${$currentUser.$id}`],
      write = [`user:${$currentUser.$id}`]
    ) => {
      try {
        dispatch("upload");
        const response = await Appwrite.storage.createFile(
          file,
          read,
          write
        );
        dispatch("success", response);
        return response;
      } catch (error) {
        dispatch("failure", error);
      }
    },
  };
</script>

<slot {actions} />
