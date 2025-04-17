<script lang="ts">
  import type { Size, Status } from "$lib/index.js";
  import { Card } from "../box/index.js";
  import Button from "./Button.svelte";

  let {
    file = $bindable<File | File[] | null>(null),
    name,
    id = Math.random().toString(36).substring(2, 15),
    accept,
    multiple = false,
    status = undefined,
    disabled = false,
    size = undefined,
    hover = false,
    selected = false,
  } = $props<{
    label?: string;
    file?: File | File[] | null;
    name?: string;
    id?: string;
    accept?: string;
    multiple?: boolean;
    status?: Status;
    disabled?: boolean;
    size?: Size | undefined;
    hover?: boolean;
    selected?: boolean;
  }>();

  const onChange = (event: Event) => {
    const input = event.target as HTMLInputElement;
    const files = input.files;
    if (files && files.length > 0) {
      if (multiple) {
        file = Array.from(files);
      } else {
        file = files[0];
      }
    }
  };

  const onDrop = (event: DragEvent) => {
    event.preventDefault();
    event.stopPropagation();
    const droppedFiles = event.dataTransfer?.files;
    if (droppedFiles && droppedFiles.length > 0) {
      if (multiple) {
        const currentFiles = Array.isArray(file) ? file : [];
        file = [...currentFiles, ...Array.from(droppedFiles)];
      } else {
        file = droppedFiles[0];
      }
    }
  };

  const onDragOver = (event: DragEvent) => {
    event.preventDefault();
    event.stopPropagation();
  };

  const onDragEnter = (event: DragEvent) => {
    event.preventDefault();
    event.stopPropagation();
  };

  const deleteFile = (index: number) => {
    if (Array.isArray(file)) {
      if (file.length === 1) {
        file = null;
      } else {
        file = file.filter((_, i) => i !== index);
      }
    } else {
      file = null;
    }
  };

  $effect(() => {
    if (!file.length) file = null;
  });
</script>

<div
  class="file-input {size}"
  class:disabled
  role="region"
  ondrop={onDrop}
  ondragover={onDragOver}
  ondragenter={onDragEnter}
>
  <Card bind:status {disabled} {hover} {selected}>
    <div class="cont" class:disabled>
      {#if file}
        <div class="name">
          {#if Array.isArray(file)}
            {#each file as f, i}
              <div class="file-item">
                <Button type="danger" onClick={() => deleteFile(i)}>
                  <span class="remove">✕</span>
                </Button>
                <p>{f.name}</p>
              </div>
            {/each}
          {:else}
            <div class="file-item">
              <p>{file.name}</p>
            </div>
          {/if}
        </div>
        <Button type="danger" onClick={() => (file = null)} {size}>
          Clear
          {#if multiple}
            All
          {/if}
        </Button>
      {:else}
        <p>Drop the file in the box</p>
        <p>or</p>
        <Button type="info" {size}><label for={id}>Browse file</label></Button>
      {/if}
    </div>
  </Card>
</div>
<input
  type="file"
  {id}
  {name}
  {accept}
  bind:files={file}
  onchange={onChange}
  hidden
  {multiple}
  {disabled}
/>

<style>
  .file-input.sm :global(.box){
    font-size: var(--font-size-sm) !important;
  }
  .file-input.md :global(.box){
    font-size: var(--font-size-md) !important;
  }
  .file-input.lg :global(.box){
    font-size: var(--font-size-lg) !important;
  }
  .cont {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 0.6rem;
    width: 100%;
    height: 100%;
  }
  .cont label {
    white-space: nowrap;
    cursor: pointer;
  }
  .cont p {
    margin: 0;
  }
  .file-item {
    display: flex;
    align-items: center;
    gap: 0.3rem;
  }
  .name {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
  }
  .disabled {
    cursor: not-allowed;
  }
</style>
