<template>
  <main class="d-flex flex-column justify-content-center align-items-center bg-dark">
    <div class="container">
      <div class="row justify-content-center mt-3">
        <div class="col col-6">
          <div class="text-center">
            <div v-if="!winMessage">
              <h2 class="text-info" v-if="isCross">
                Cross True
              </h2>
              <h2 class="text-info" v-if="!isCross">
                Circle True
              </h2>
            </div>
            <div v-else>
              <h1 class="text-warning">
                {{ winMessage.toUpperCase() }}
              </h1>
            </div>
          </div>
          <div class="grid">
            <div 
            v-for="(item, i) in itemArray"
            :key="i"
            @click="handleClick(i)"
            class="card card-body box justify-content-center align-items-center bg-light">
                <Grid :iconname="item"></Grid>
            </div>
          </div>
        </div>
      </div>
      <div class = "d-grid gap-2 col-6 mx-auto">
      <button 
      @click="reloadGame()"
      class="btn btn-info btn-lg mt-5 pl-5 pr-5">
        Reset the game
      </button>
    </div>
    </div>
  </main>
</template>

<script>
import Grid from '../components/grid.vue'
import { defineComponent, computed , watch} from 'vue';

export default defineComponent({
  name: 'GameTicTacToe',
  components: { Grid },
  setup () {

    let winMessage = '';
    let isCross = true;
    
    const itemArray = computed(() => {
       return ['a','b','c','a','b','c','a','b','c'];
    })

    let temp = false;

    watch (() => (itemArray.value), 
    () => { 
      temp = !temp
    });

    for (let i = 0; i < itemArray.value.length; i++){
        itemArray.value[i] = 'empty'
    }
    console.log(itemArray.value)

    const showDialog = () => {
      alert(winMessage)
    }

    const handleClick = (itemNumber) => {
      if(winMessage) {
        return showDialog()
      }
      if (typeof itemNumber === 'number'){
        if(itemArray.value[itemNumber] === 'empty') {
            itemArray.value[itemNumber] = isCross ? 'cross' : 'circle'
            isCross = !isCross
        }else{
            alert('Already Filled!')
        }

        checkWinner()
      }
       console.log(itemArray.value)
    }

    const checkWinner = () => {
      //  checking  winner of the game
      if (
        itemArray.value[0] === itemArray.value[1] &&
        itemArray.value[0] === itemArray.value[2] &&
        itemArray.value[0] !== 'empty'
      ) {
        winMessage = `${itemArray.value[0]} won`;
      } else if (
        itemArray.value[3] !== 'empty' &&
        itemArray.value[3] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[5]
      ) {
        winMessage = `${itemArray.value[3]} won`;
      } else if (
        itemArray.value[6] !== 'empty' &&
        itemArray.value[6] === itemArray.value[7] &&
        itemArray.value[7] === itemArray.value[8]
      ) {
        winMessage = `${itemArray.value[6]} won`;
      } else if (
        itemArray.value[0] !== 'empty' &&
        itemArray.value[0] === itemArray.value[3] &&
        itemArray.value[3] === itemArray.value[6]
      ) {
        winMessage = `${itemArray.value[0]} won`;
      } else if (
        itemArray.value[1] !== 'empty' &&
        itemArray.value[1] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[7]
      ) {
        winMessage = `${itemArray.value[1]} won`;
      } else if (
        itemArray.value[2] !== 'empty' &&
        itemArray.value[2] === itemArray.value[5] &&
        itemArray.value[5] === itemArray.value[8]
      ) {
        winMessage = `${itemArray.value[2]} won`;
      } else if (
        itemArray.value[0] !== 'empty' &&
        itemArray.value[0] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[8]
      ) {
        winMessage = `${itemArray.value[0]} won`;
      } else if (
        itemArray.value[2] !== 'empty' &&
        itemArray.value[2] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[6]
      ) {
        winMessage = `${itemArray.value[2]} won`;
      }
       console.log(itemArray.value)
    }

    const reloadGame = () => {
      winMessage = '';
      isCross = true;
      for (let i = 0; i < itemArray.value.length; i ++){
          itemArray.value[i] = 'empty'
      }
       console.log(itemArray.value)
    }


    return {
      winMessage,
      isCross,
      itemArray,
      reloadGame,
      handleClick
    }
  } 

})
</script>



<style lang="scss" scoped>
main {
  height: 100vh;
}
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 5px;
}

.box {
  height: 150px;
}
</style>