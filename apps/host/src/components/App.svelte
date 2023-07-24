<script lang="ts">
  import Navbar from "./Navbar.svelte";
  import { LoadRemoteModule } from "../load-remote-module";
  let remoteAppTarget: any;
  let dynamicComponent: any = null;
  let host: string = process.env.APPS_URL ?? "";
  let apps: string[] = [];
  let selected: string = "";
  const loadRemoteModule = new LoadRemoteModule();

  function setHost(value: CustomEvent): void {
    host = value.detail;
  }

  async function setComponent(value: CustomEvent): Promise<void> {
    selected = value.detail;
    remoteAppTarget.innerHTML = "";
    if (!selected) {
      dynamicComponent = null;
      return;
    }
    dynamicComponent = (
      await loadRemoteModule.loadComponent(selected, "./Module")
    ).default;

    new dynamicComponent({
      target: remoteAppTarget,
    });
  }

  async function loadServers(): Promise<void> {
    await loadRemoteModule.setHost(host).loadServers();
    apps = loadRemoteModule.apps;
  }
</script>

<div class="host">
  <Navbar
    {apps}
    {selected}
    {host}
    on:onInput={setHost}
    on:loadServers={loadServers}
    on:setComponent={setComponent}
  />
  <div class="dynamic__component" bind:this={remoteAppTarget} />
  {#if !dynamicComponent}
    <div class="host__content">
      <div class="host__title">
        <h1>Host</h1>
      </div>
    </div>
  {/if}
</div>

<style scoped lang="scss">
  .host {
    background: var(--gr-azure-pink);
    width: 100%;
    height: 100%;
    &__content {
      display: grid;
      justify-content: center;
      align-content: center;
      width: 100%;
      height: 100%;
      h1 {
        width: max-content;
        text-transform: uppercase;
        background: var(--teal);
        background: var(--gr-teal-blue);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
      }
    }
  }
  .dynamic {
    &__component {
      display: contents;
    }
  }
</style>
