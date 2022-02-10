<script>
  /**
   * @slot {{
   * codes: any;
   * actions: {
   *  reload: () => Promise<object>;
   * }}}
   * @slot {{ error: object }} error
   */
   import Appwrite from "$lib/appwrite";

  const fetchPhoneCodes = () => Appwrite.locale.getCountriesPhones();

  const actions = {
    reload: () => (phoneCodes = fetchPhoneCodes()),
  };

  let phoneCodes = fetchPhoneCodes();
</script>

{#await phoneCodes}
  <slot name="loading" />
{:then response}
  <slot codes={response} {actions} />
{:catch error}
  <slot name="error" {error} />
{/await}
