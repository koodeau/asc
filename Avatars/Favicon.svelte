<script>
  import { Appwrite } from "$lib/appwrite";

  export let url;

  let src = Appwrite.avatars.getFavicon(url);
</script>

<slot {src} />
