<script lang="ts">
  import { Heading } from 'flowbite-svelte';
  import BoardCard from './BoardCard.svelte';

  let board1: bigint;
  let board2: bigint;
</script>

<div class="flex flex-col items-center mx-4">
  <Heading tag="h1" class="w-fit my-8">BitBoard Builder</Heading>

  <BoardCard bind:boardValue={board1} />
</div>
