<script lang="ts">
  import User from "carbon-icons-svelte/lib/User.svelte";
  import TextMiningApplier from "carbon-icons-svelte/lib/TextMiningApplier.svelte";

  export let user: App.Locals["user"];
</script>

<nav aria-label="Site Nav" class="flex items-center justify-between py-8 ">
  <a href="/" class="inline-flex items-center justify-center gap-3">
    <span class="sr-only">Logo</span>
    <TextMiningApplier size={20} class="text-cyan-700" />
    <span class="text-lg font-semibold">Brand</span>
  </a>

  <ul class="flex items-center gap-2 text-sm text-gray-500">
    <li>
      <div class="inline-flex justify-center items-center gap-3 rounded-full bg-gray-100 px-4 py-1.5">
        <User size={16} class="text-gray-700" />
        <span class="">{user.username}</span>
      </div>
    </li>
    <li />
    <li class="mr-2 text-gray-300">•</li>
    <li>
      <a
        class="relative text-cyan-600 before:absolute before:-bottom-1 before:h-0.5 before:w-full before:origin-left before:scale-x-0 before:bg-cyan-600 before:transition hover:before:scale-100"
        href="/logout"
      >
        Logout
      </a>
    </li>
  </ul>
</nav>
