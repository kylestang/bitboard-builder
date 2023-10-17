<script lang="ts">
  import { Input, Heading, Card } from 'flowbite-svelte';
  import BitBoard from './BitBoard.svelte';

  let boardValue = 0n;

  let decValue = '0';
  let hexValue = '0x0';
  let binValue = '0b0';
  let xSize = '8';
  let ySize = '8';

  $: {
    decValue = boardValue.toString(10);
    hexValue = '0x' + boardValue.toString(16);
    binValue = '0b' + boardValue.toString(2);
  }
</script>

<Card class="max-w-full gap-4 items-center">
  <BitBoard xSize={Number(xSize)} ySize={Number(ySize)} value={boardValue} />

  <div class="flex flex-row gap-2">
    <div class="flex flex-row items-center">
      X size:
      <Input bind:value={xSize} class="w-12" />
    </div>
    <div class="flex flex-row items-center">
      Y size:
      <Input bind:value={ySize} class="w-12" />
    </div>
  </div>

  <div class="flex flex-col">
    Value:
    <Input
      bind:value={decValue}
      on:input={() => {
        boardValue = BigInt(decValue);
      }}
      class="w-50"
    />
    <Input
      bind:value={hexValue}
      on:input={() => {
        boardValue = BigInt(hexValue);
      }}
      class="w-50"
    />
    <Input
      bind:value={binValue}
      on:input={() => {
        boardValue = BigInt(binValue);
      }}
      class="w-50"
    />
  </div>
</Card>
