<template>
    <q-layout view="hHh lpR fFf " class="row">
    <q-page-container class="game col">
      <game-tic-tac-toe/>
    </q-page-container>
    <q-page-container class="tree col text-center">
      <h2>TREE</h2>
      <h2>...</h2>
    </q-page-container>
  </q-layout>
</template>



<script lang="ts">
import { defineComponent } from 'vue';
import GameTicTacToe from './GameTicTacToe.vue';

export default defineComponent({
  name: 'TicTacToe',
  components: { GameTicTacToe },
  setup() {
    
    return
  }
});
</script>
