<script lang="ts">
  export let xSize: number;
  export let ySize: number;
  export let value: bigint;
  export let disabled: boolean;

  let bits: bigint[] = [];

  $: {
    let valueCopy = value;
    bits = [];
    for (let i = 0; i < xSize * ySize; i++) {
      bits.push(valueCopy & 1n);
      valueCopy = valueCopy >> 1n;
    }
  }
</script>

<div class="flex flex-col text-black">
  {#each Array(ySize) as _, y}
    <div class="flex flex-row">
      {#each Array(xSize) as _, x}
        <button
          {disabled}
          class="w-6 h-6 text-center"
          on:click={() => {
            value = value ^ (1n << (BigInt(y) * BigInt(xSize) + BigInt(x)));
          }}
        >
          {bits[(x % xSize) + y * xSize]}
        </button>
      {/each}
    </div>
  {/each}
</div>
