<template>
  <q-page class="row items-center justify-evenly">
    <tic-tac-toe/>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TicTacToe from './TicTacToe.vue';

export default defineComponent({
  name: 'PageIndex',
  components: { TicTacToe},
  setup() {
    
    return
  }
});
</script>
