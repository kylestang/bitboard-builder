<script lang="ts">
  import { Input, NumberInput, Card, Button, ButtonGroup } from 'flowbite-svelte';
  import BitBoard from './BitBoard.svelte';

  export let boardValue = 0n;
  export let xSize = 8;
  export let ySize = 8;

  let decValue = '0';
  let hexValue = '0x0';
  let binValue = '0b0';

  // Mask to same size as grid
  $: if (xSize !== null && ySize !== null) {
    boardValue = boardValue & ((1n << (BigInt(xSize) * BigInt(ySize))) - 1n)
  } 

  $: {
    decValue = boardValue.toString(10);
    hexValue = '0x' + boardValue.toString(16);
    binValue = '0b' + boardValue.toString(2);
  }
</script>

<Card class="max-w-full w-full sm:w-fit gap-4 items-center">
  <BitBoard xSize={Number(xSize)} ySize={Number(ySize)} value={boardValue} />

  <div class="flex flex-row gap-2">
    <div class="flex flex-row items-center">
      X size:
      <NumberInput bind:value={xSize} class="w-14" />
    </div>
    <div class="flex flex-row items-center">
      Y size:
      <NumberInput bind:value={ySize} class="w-14" />
    </div>
  </div>

  <ButtonGroup>
    <Button on:click={() => {boardValue = ~0n}}>Fill</Button>
    <Button on:click={() => {boardValue = 0n}}>Clear</Button>
    <Button on:click={() => {boardValue = boardValue << 1n}}>Left</Button>
    <Button on:click={() => {boardValue = boardValue >> 1n}}>Right</Button>
  </ButtonGroup>

  <div class="flex flex-col">
    Value:
    <Input
      bind:value={decValue}
      on:input={() => {
        decValue = decValue.replace(/\D/g, '');
        if (decValue === '') {
          decValue = '0';
        }
        boardValue = BigInt(decValue);
      }}
      class="w-50"
    />
    <Input
      bind:value={hexValue}
      on:input={() => {
        let pieces = hexValue.split('x', 2);
        let nums = pieces[1].replace(/[^0-9a-fA-F]/g, '');
        if (nums === '') {
          nums = '0';
        }
        hexValue = '0x' + nums;
        boardValue = BigInt(hexValue);
      }}
      class="w-50"
    />
    <Input
      bind:value={binValue}
      on:input={() => {
        let pieces = binValue.split('b', 2);
        let nums = pieces[1].replace(/[^01]/g, '');
        if (nums === '') {
          nums = '0';
        }
        binValue = '0b' + nums;
        boardValue = BigInt(binValue);
      }}
      class="w-50"
    />
  </div>
</Card>
