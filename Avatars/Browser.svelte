<script>
  import { Appwrite } from "$lib/appwrite";

  export let code;
  export let width = 100;
  export let height = 100;
  export let quality = 100;

  let src = Appwrite.avatars.getBrowser(code, width, height, quality);
</script>

<slot {src} />
