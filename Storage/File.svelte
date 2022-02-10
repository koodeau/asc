<script>
  /**
   * @slot {{
   * file: any;
   * actions: {
   *  download: () => string;
   *  view: (as?: string) => string;
   *  preview: (width?: string, height?: string, quality?: string, background?: string, output?: string) => string;
   *  update: (read?: any, write?: any) => Promise<object>;
   *  delete: () => Promise<object>;
   * }}}
   * @slot {{ error: object }} error
   */
   import { Appwrite } from "$lib/appwrite";

  export let file;
  const actions = {
    download: () => Appwrite.storage.getFileDownload(file.$id),
    view: (as = "") => Appwrite.storage.getFileView(file.$id, as),
    preview: (
      width = "",
      height = "",
      quality = "",
      background = "",
      output = ""
    ) =>
      Appwrite.storage.getFilePreview(
        file.$id,
        width,
        height,
        quality,
        background,
        output
      ),
    update: async (
      read = file.$permissions.read,
      write = file.$permissions.write
    ) => await Appwrite.storage.updateFile(file.$id, read, write),
    delete: async () => await Appwrite.storage.deleteFile(file.$id),
  };
</script>

<slot {actions} />
