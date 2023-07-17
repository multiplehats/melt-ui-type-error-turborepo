<script lang="ts">
  import { createPinInput } from '@melt-ui/svelte';
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher<{
    change: { value: string; valueRaw: string[] };
  }>();

  /**
   * A default value for the pin input.
   */
  export let value: string | undefined = undefined;
  export let required = false;
  export let disabled = false;

  const {
    root,
    input,
    valueStr,
    value: valueRaw
  } = createPinInput({
    disabled,
    value: value ? value.split('') : undefined
  });

  $: dispatch('change', { value: $valueStr, valueRaw: $valueRaw });
</script>

<div melt={$root} class="flex items-center gap-2">
  {#each Array.from({ length: 6 }) as _, i}
    <input
      class="rounded-md bg-white text-center text-lg text-black font-bold shadow-sm square-12"
      melt={$input}
      {required}
      {...$$restProps}
    />
  {/each}
</div>
