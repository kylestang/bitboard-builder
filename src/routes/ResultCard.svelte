<script lang="ts">
  import { Button, ButtonGroup, Card, Input } from 'flowbite-svelte';
  import BitBoard from './BitBoard.svelte';

  export let board1: bigint = 0n;
  export let board2: bigint = 0n;
  export let xSize = 8;
  export let ySize = 8;

  let boardValue = 0n;
  let operation: 'OR' | 'AND' | 'XOR' = 'OR';
  let decValue = boardValue.toString(10);
  let hexValue = '0x' + boardValue.toString(16);
  let binValue = '0b' + boardValue.toString(2);

  $: {
    if (operation === 'OR') {
      boardValue = board1 | board2;
    } else if (operation === 'AND') {
      boardValue = board1 & board2;
    } else if (operation === 'XOR') {
      boardValue = board1 ^ board2;
    }

    decValue = boardValue.toString(10);
    hexValue = '0x' + boardValue.toString(16);
    binValue = '0b' + boardValue.toString(2);
  }
</script>

<Card class="max-w-max w-full sm:w-fit gap-4 items-center h-min">
  <BitBoard disabled={true} bind:value={boardValue} {xSize} {ySize} />
  <ButtonGroup>
    <Button
      class={operation === 'AND' ? 'text-primary-700' : ''}
      on:click={() => {
        operation = 'AND';
      }}>AND</Button
    >
    <Button
      class={operation === 'OR' ? 'text-primary-700' : ''}
      on:click={() => {
        operation = 'OR';
      }}>OR</Button
    >
    <Button
      class={operation === 'XOR' ? 'text-primary-700' : ''}
      on:click={() => {
        operation = 'XOR';
      }}>XOR</Button
    >
  </ButtonGroup>

  <div class="flex flex-col w-full">
    Value:
    <Input disabled={true} bind:value={decValue} />
    <Input disabled={true} bind:value={hexValue} />
    <Input disabled={true} bind:value={binValue} />
  </div>
</Card>
