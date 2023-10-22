<script lang="ts">
  import { Heading, NumberInput } from 'flowbite-svelte';
  import BoardCard from './BoardCard.svelte';
  import ResultCard from './ResultCard.svelte';

  let board1: bigint;
  let board2: bigint;

  let xSize = 8;
  let ySize = 8;
</script>

<div class="flex flex-col items-center mx-4">
  <Heading tag="h1" class="w-fit my-8">BitBoard Builder</Heading>

  <div class="flex flex-row gap-2 mb-8">
    <div class="flex flex-row items-center">
      X size:
      <NumberInput bind:value={xSize} class="w-14" />
    </div>
    <div class="flex flex-row items-center">
      Y size:
      <NumberInput bind:value={ySize} class="w-14" />
    </div>
  </div>

  <div class="flex flex-row gap-4 flex-wrap justify-center mb-8">
    <BoardCard bind:boardValue={board1} xSize={Number(xSize)} ySize={Number(ySize)} />
    <BoardCard bind:boardValue={board2} xSize={Number(xSize)} ySize={Number(ySize)} />
    <ResultCard {board1} {board2} xSize={Number(xSize)} ySize={Number(ySize)} />
  </div>
</div>
