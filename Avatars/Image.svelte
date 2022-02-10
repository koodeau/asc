<script>
  import Appwrite from "$lib/appwrite";

  export let url;
  export let width = "";
  export let height = "";

  let src = Appwrite.avatars.getImage(url, width, height);
</script>

<slot {src} />
