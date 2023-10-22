<script lang="ts">
  import { Input, Card, Button, ButtonGroup } from 'flowbite-svelte';
  import BitBoard from './BitBoard.svelte';

  export let boardValue = 0n;
  export let xSize = 8;
  export let ySize = 8;

  let decValue = '0';
  let hexValue = '0x0';
  let binValue = '0b0';

  // Mask to same size as grid
  $: if (xSize !== null && ySize !== null) {
    boardValue = boardValue & ((1n << (BigInt(xSize) * BigInt(ySize))) - 1n);
  }

  $: {
    decValue = boardValue.toString(10);
    hexValue = '0x' + boardValue.toString(16);
    binValue = '0b' + boardValue.toString(2);
  }
</script>

<Card class="max-w-max w-full sm:w-fit gap-4 items-center">
  <BitBoard disabled={false} {xSize} {ySize} bind:value={boardValue} />

  <ButtonGroup>
    <Button
      on:click={() => {
        boardValue = ~0n;
      }}>Fill</Button
    >
    <Button
      on:click={() => {
        boardValue = 0n;
      }}>Clear</Button
    >
    <Button
      on:click={() => {
        boardValue = boardValue << 1n;
      }}>Left</Button
    >
    <Button
      on:click={() => {
        boardValue = boardValue >> 1n;
      }}>Right</Button
    >
    <Button
      on:click={() => {
        boardValue = ~boardValue;
      }}>Not</Button
    >
  </ButtonGroup>

  <div class="flex flex-col w-full">
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
    />
    <Input
      bind:value={hexValue}
      on:input={() => {
        let pieces = hexValue.split('x', 2);
        let nums;
        if (pieces.length === 1) {
          nums = '0';
        } else {
          nums = pieces[1].replace(/[^0-9a-fA-F]/g, '');
          if (nums === '') {
            nums = '0';
          }
        }
        hexValue = '0x' + nums;
        boardValue = BigInt(hexValue);
      }}
    />
    <Input
      bind:value={binValue}
      on:input={() => {
        let pieces = binValue.split('b', 2);
        let nums;
        if (pieces.length === 1) {
          nums = '0';
        } else {
          nums = pieces[1].replace(/[^01]/g, '');
          if (nums === '') {
            nums = '0';
          }
        }
        binValue = '0b' + nums;
        boardValue = BigInt(binValue);
      }}
    />
  </div>
</Card>
