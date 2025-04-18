<script lang="ts">
  import type { Size, Status } from "$lib/index.js";

  export let size: Size = undefined;
  export let aspect: string = "";
  export let status: Status = undefined;
  export let disabled: boolean = false;
  export let hover: boolean = false;
  export let selected: boolean = false;

  $: ar = aspect.split("/");
  $: style = aspect.length > 0 ? `--arw:${ar[0]}; --arh:${ar[1]}` : "auto";
</script>

<div
  class="box {size ? size : ''}"
  class:disabled
  class:hover
  class:selected
  style="--bd-color:{status
    ? `var(--${status})`
    : 'var(--border-color)'}; {style}"
>
  {#if $$slots.legend}
    <div class="legend-wrapper">
      <div class="legend">
        <slot name="legend" />
      </div>
    </div>
  {/if}

  {#if $$slots.title}
    <header>
      <slot name="title" />
    </header>
  {/if}
  {#if $$slots.default}
    <div class="content">
      <slot />
    </div>
  {/if}
  {#if $$slots.footer}
    <footer>
      <slot name="footer" />
    </footer>
  {/if}
</div>

<style>
  .box.hover:hover {
    --bd-color: var(--focus-color) !important;
  }

  .box.selected {
    --bd-color: var(--focus-color) !important;
  }

  .box {
    border: 1px solid var(--bd-color);
    border-radius: var(--border-radius);
    display: flex;
    flex-direction: column;
    aspect-ratio: var(--arw) / var(--arh);
    font-size: var(--font-size-md);
    position: relative;
  }

  .box.selected {
    box-shadow: 0 0 0 2px var(--selected-color);
  }

  .legend-wrapper {
    position: absolute;
    top: -0.5em;
    left: 0.4rem;
    right: 0.5em;
    display: flex;
  }

  .legend {
    background: var(--bg-color, white);
    padding: 0 0.1em;
    font-size: 0.875em;
    color: var(--text-color, inherit);
  }

  .sm {
    width: 300px;
  }
  .md {
    width: 500px;
  }
  .lg {
    width: 700px;
  }

  header {
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
    padding: 0.5rem;
    font-weight: bold;
    font-size: var(--font-size-lg);
  }

  .content {
    padding: 0.5rem;
    flex: 1;
  }

  header + .content {
    border-top: 1px solid var(--bd-color);
  }

  header:empty + .content {
    border-top: none;
  }

  header:empty {
    padding: 0;
  }

  footer {
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
    border-top: 1px solid var(--bd-color);
    padding: 0.5rem;
  }

  header + .content:empty,
  footer:empty {
    display: none;
    border-top: none;
    border-bottom: none;
  }

  .disabled {
    opacity: 0.5;
    pointer-events: none;
    cursor: not-allowed;
  }
</style>
