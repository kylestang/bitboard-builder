<script lang="ts">
  export let xSize: number;
  export let ySize: number;
  export let value: bigint;

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

<div class="flex flex-col">
  {#each Array(ySize) as _, y}
    <div class="flex flex-row">
      {#each Array(xSize) as _, x}
        <div class="w-6 h-6 text-center">
          {bits[(x % xSize) + y * xSize]}
        </div>
      {/each}
    </div>
  {/each}
</div>
