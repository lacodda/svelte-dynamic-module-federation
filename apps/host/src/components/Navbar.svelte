<script lang="ts">
  import { createEventDispatcher } from "svelte";

  export let apps: string[];
  export let host: string;
  export let selected: string;
  const dispatch = createEventDispatcher();

  function loadServers(): void {
    dispatch("loadServers", true);
  }

  function setComponent(event: Event): void {
    dispatch("setComponent", (event.target as HTMLSelectElement).value);
  }

  function onInput(event: Event): void {
    dispatch("onInput", (event.target as HTMLInputElement).value);
  }
</script>

<div class="navbar__container">
  <div class="navbar__menu">
    <input value={host} style="width: 100%" on:input={onInput} />
    <button class="btn" on:click={loadServers}>Download</button>
    <select value={selected} on:change={setComponent}>
      <option value="">Please select one</option>
      {#each apps as app}
        <option value={app}>{app}</option>
      {/each}
    </select>
  </div>
</div>

<style lang="scss">
  .navbar {
    &__container {
      position: absolute;
      width: 100%;
    }
    &__menu {
      display: flex;
      justify-content: center;
      padding: 1rem;
      gap: 1rem;
    }
  }
</style>
