<script lang="ts">
  import type { Size, Status } from "$lib/index.js";
  import UpDown from "./UpDown.svelte";

  let {
    name = "",
    status,
    min = "A",
    max = "ZZZ",
    disabled = $bindable(false),
    size = "md",
    value = $bindable("A"),
  } = $props<{
    name?: string;
    status?: Status;
    min?: string;
    max?: string;
    disabled?: boolean;
    size?: Size;
    value?: string;
  }>();

  let internalValue = $state(charToNumber(value || "A"));
  let minInternal = charToNumber(min);
  let maxInternal = charToNumber(max);

  function numberToChar(n: number) {
    let result = "";
    while (n >= 0) {
      result = String.fromCharCode((n % 26) + 65) + result;
      n = Math.floor(n / 26) - 1;
    }
    return result;
  }

  function charToNumber(c: string) {
    let result = 0;
    for (let i = 0; i < c.length; i++) {
      result = result * 26 + (c.charCodeAt(i) - 65 + 1);
    }
    return result - 1;
  }

  function onChange(d: boolean) {
    if (disabled || value === null) return null;
    internalValue = charToNumber(value);
    if (d) {
      if (internalValue < maxInternal) internalValue++;
    } else {
      if (internalValue > minInternal) internalValue--;
    }
    value = numberToChar(internalValue);
  }

  function check(value: string | null) {
    if (disabled || value === null) return null;
    internalValue = charToNumber(value);
    if (internalValue < minInternal) internalValue = minInternal;
    if (internalValue > maxInternal) internalValue = maxInternal;
    const nValue = numberToChar(internalValue);
    if (nValue !== value) return nValue;
    return value.toUpperCase();
  }
</script>

<UpDown {disabled} {size} {status} {onChange} maxLength={max.toString().length}>
  <input
    type="text"
    bind:value
    class={size}
    {disabled}
    {name}
    onchange={() => check(value)}
  />
</UpDown>
