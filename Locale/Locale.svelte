<script>
  /**
   * @slot {{
   * code: any;
   * actions: {
   *  reload: () => Promise<object>;
   * }}}
   * @slot {{ error: object }} error
   */
   import Appwrite from "$lib/appwrite";

  const fetchUserLocale = () => Appwrite.locale.get();

  const actions = {
    reload: () => (locale = fetchUserLocale()),
  };

  let locale = fetchUserLocale();
</script>

{#await locale}
  <slot name="loading" />
{:then response}
  <slot code={response} {actions} />
{:catch error}
  <slot name="error" {error} />
{/await}
