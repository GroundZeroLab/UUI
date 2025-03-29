<script lang="ts">
  export let href = "";
  export let active = false;
  export let preload: "hover" | "tap" | "off" = "hover";
</script>

<a {href} class:active>
  <slot />
  {#if $$slots.description}
    <p>
      <slot
        name="description"
        class="description"
        data-sveltekit-preload-data={preload}
      />
    </p>
  {/if}
</a>

<style>
  a {
    padding: 0.4rem 0.6rem;
    border-radius: 8px;
    display: inline-block;
    transition: 0.2s;
    text-decoration: none;
    color: inherit;
    font-weight: bold;
  }
  a:hover {
    background-color: rgba(126, 126, 126, 0.15);
  }
  a.active {
    background-color: rgba(126, 126, 126, 0.15);
  }
  p {
    font-size: 14px;
    color: var(--txt-secondary);
    margin: 0.3rem 0 0 0;
  }
</style>
