<script>
  import Appwrite from "$lib/appwrite";

  export let text;
  export let size = 400;
  export let margin = 1;
  export let download = false;

  let src = Appwrite.avatars.getQR(text, size, margin, download ? 1 : 0);
</script>

<slot {src} />
