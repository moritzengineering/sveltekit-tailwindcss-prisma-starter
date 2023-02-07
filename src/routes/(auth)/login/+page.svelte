<script lang="ts">
  import { applyAction, enhance } from "$app/forms";
  import { invalidateAll } from "$app/navigation";

  import type { ActionData } from "./$types";

  export let form: ActionData;
</script>

<div class="mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8 pt-[10%]">
  <div class="mx-auto max-w-lg text-center">
    <h1 class="text-2xl font-bold sm:text-3xl">Login</h1>
  </div>

  <div class="mx-auto mt-12 mb-0 max-w-md">
    {#if form?.invalid}
      <div role="alert" class="rounded border border-red-200 bg-red-50 p-4">
        <p class="text-sm text-red-700">Username and password is required.</p>
      </div>
    {/if}

    {#if form?.credentials}
      <div role="alert" class="rounded border border-red-200 bg-red-50 p-4">
        <p class="text-sm text-red-700">Invalid credentials</p>
      </div>
    {/if}
  </div>

  <form
    action="?/login"
    method="POST"
    class="mx-auto mt-8 mb-0 max-w-md space-y-4"
    use:enhance={() => {
      return async ({ result }) => {
        // rerun the `load` function for the page
        // https://kit.svelte.dev/docs/modules#$app-navigation-invalidateall
        invalidateAll();

        // since we're customizing the default behaviour
        // we don't want to reimplement what `use:enhance` does
        // so we can use `applyResult` and pass the `result`
        await applyAction(result);
      };
    }}
  >
    <div>
      <label for="username" class="sr-only">Username</label>

      <div class="relative">
        <input
          required
          type="text"
          name="username"
          id="username"
          class="w-full rounded-lg border-gray-300 p-4 pr-12 text-sm"
          placeholder="Enter username"
        />
      </div>
    </div>

    <div>
      <label for="password" class="sr-only">Password</label>
      <div class="relative">
        <input
          required
          type="password"
          id="password"
          name="password"
          class="w-full rounded-lg border-gray-300 p-4 pr-12 text-sm"
          placeholder="Enter password"
        />
      </div>
    </div>

    <div class="flex items-center justify-between">
      <p class="text-sm text-gray-500">
        No account?
        <a class="underline" href="/register">Sign up</a>
      </p>

      <button
        type="submit"
        class="inline-flex items-center rounded border border-cyan-600 bg-cyan-600 px-6 py-3 text-white focus:outline-none "
      >
        <span class="text-sm font-medium"> Log In </span>

        <svg
          class="ml-3 h-5 w-5"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
        </svg>
      </button>
    </div>
  </form>
</div>
