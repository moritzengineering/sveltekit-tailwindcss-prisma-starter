<script lang="ts">
  import Navbar from "$lib/components/Navbar.svelte";

  import { beforeNavigate } from "$app/navigation";
  import { metadata } from "$lib/app/stores";
  import { site } from "$lib/config";

  export let data: App.PageData & Record<string, any>;

  $: title = $metadata.title ? $metadata.title + " | " + site.name : site.name;
  $: description = $metadata.description ?? site.description;

  // reset metadata on navigation so that the new page inherits nothing from the old page
  beforeNavigate(() => {
    $metadata = {};
  });
</script>

<svelte:head>
  <title>{title}</title>
  <meta name="description" content={description} />
</svelte:head>

<div class="mx-auto max-w-6xl px-6">
  <Navbar user={data.user} />

  <slot />
</div>
