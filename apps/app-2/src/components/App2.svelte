<div class="app2__container">
  <div class="app2__title">
    <h1>App 2</h1>
  </div>
</div>

<style lang="scss">
  .app2 {
    &__container {
      display: grid;
      justify-content: center;
      align-content: center;
      background: var(--gr-lime-blue);
      width: 100%;
      height: 100%;
    }
    &__title {
      display: flex;
      h1 {
        font-size: var(--font-size-h1);
        width: max-content;
        text-transform: uppercase;
        background: var(--teal);
        background: var(--gr-teal-blue);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
      }
    }
  }
</style>
