<template>
  <main class="d-flex flex-column justify-content-center align-items-center bg-dark">
    <div class="container__top">
       <div class="row justify-content-center mt-3">
          
          <div class="col">
            <q-toggle              
              :label="`Spiel als ${signToggleName}`"
              color="blue"
              size="xl"    
              checked-icon="radio_button_unchecked"
              unchecked-icon="close"        
              v-model="signToggle"              
            />
          </div>
         
          <div class="col">
            <q-toggle              
              :label="`Spiel gegen ${modiToggleName}`"
              color="blue"
              size="xl"    
              checked-icon="computer"
              unchecked-icon="person"        
              v-model="modiToggle"              
            />
          </div>
           <div class="col"></div>
          
       </div>
    </div>

    <div class="container">
      <div class="justify-content-center mt-3">
          <div class="text-message text-center">
            <div v-if="!winMessage">
              <h4 class="text-info" v-if="isCross">
                Kreuz ist dran!
              </h4>
              <h4 class="text-info" v-if="!isCross">
                Kreis ist dran!
              </h4>
            </div>
            <div v-else>
              <h3 class="text-warning">
                {{ winMessage.toUpperCase() }}
              </h3>
            </div>
          </div>
          <div class="grid">
            <div 
            v-for="(item, i) in itemArray"
            :key="i"
            @click="handleClick(i)"
            class="grid-div card card-body box justify-content-center align-items-center bg-light">
                <Grid :iconname="item"></Grid>
            </div>
          </div>
        
        <div class = "col col-6">      
          <q-btn class="resetBtn" outline style="color: goldenrod;" label="Reset the game" @click="reloadGame()"/>
        </div>
        </div>
     
      
    </div>
  </main>
</template>

<script>
import Grid from '../components/grid.vue'
import { defineComponent, ref, watch} from 'vue';

export default defineComponent({
  name: 'GameTicTacToe',
  components: { Grid },
  setup () {

    let winMessage = ref('');
    let isCross = ref(true);
    
    const itemArray = ref(['a','b','c','a','b','c','a','b','c'])    

    let modiToggle = ref(false)
    let modiToggleName = ref('Mensch')
    let signToggle = ref(false)
    let signToggleName = ref('Kreuz')

    for (let i = 0; i < itemArray.value.length; i++){
        itemArray.value[i] = 'empty'
    }
    console.log(itemArray.value)

    const showDialog = () => {
      alert(winMessage.value)
    }

    const handleClick = (itemNumber) => {
      if(winMessage.value) {
        return showDialog()
      }
      if (typeof itemNumber === 'number'){
        if(itemArray.value[itemNumber] === 'empty') {
            itemArray.value[itemNumber] = isCross.value ? 'kreuz' : 'kreis'
            isCross.value = !isCross.value
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
        winMessage.value = `${itemArray.value[0]} hat gewonnen!`;
      } else if (
        itemArray.value[3] !== 'empty' &&
        itemArray.value[3] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[5]
      ) {
        winMessage.value = `${itemArray.value[3]} hat gewonnen!`;
      } else if (
        itemArray.value[6] !== 'empty' &&
        itemArray.value[6] === itemArray.value[7] &&
        itemArray.value[7] === itemArray.value[8]
      ) {
        winMessage.value = `${itemArray.value[6]} hat gewonnen!`;
      } else if (
        itemArray.value[0] !== 'empty' &&
        itemArray.value[0] === itemArray.value[3] &&
        itemArray.value[3] === itemArray.value[6]
      ) {
        winMessage.value = `${itemArray.value[0]} hat gewonnen!`;
      } else if (
        itemArray.value[1] !== 'empty' &&
        itemArray.value[1] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[7]
      ) {
        winMessage.value = `${itemArray.value[1]} hat gewonnen!`;
      } else if (
        itemArray.value[2] !== 'empty' &&
        itemArray.value[2] === itemArray.value[5] &&
        itemArray.value[5] === itemArray.value[8]
      ) {
        winMessage.value = `${itemArray.value[2]} hat gewonnen!`;
      } else if (
        itemArray.value[0] !== 'empty' &&
        itemArray.value[0] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[8]
      ) {
        winMessage.value = `${itemArray.value[0]} hat gewonnen!`;
      } else if (
        itemArray.value[2] !== 'empty' &&
        itemArray.value[2] === itemArray.value[4] &&
        itemArray.value[4] === itemArray.value[6]
      ) {
        winMessage.value = `${itemArray.value[2]} hat gewonnen!`;
      }
       console.log(itemArray.value)
    }

    const reloadGame = () => {
      winMessage.value = '';
      isCross.value = true;
      for (let i = 0; i < itemArray.value.length; i ++){
          itemArray.value[i] = 'empty'
      }
       console.log(itemArray.value)
    } 


    watch (() => (modiToggle.value), 
    () => { 
      if (modiToggleName.value ==='Mensch') {
        modiToggleName.value = 'KI'
      } else {
         modiToggleName.value = 'Mensch'
      }
      console.log(modiToggle.value, modiToggleName.value)
    });

     watch (() => (signToggle.value), 
    () => { 
      if (signToggleName.value ==='Kreuz') {
        signToggleName.value = 'Kreis'
      } else {
         signToggleName.value = 'Kreuz'
      }
      console.log(signToggle.value, signToggleName.value)
    });


    return {
      winMessage,
      isCross,
      itemArray,
      modiToggle,
      modiToggleName,
      signToggle,
      signToggleName,
      reloadGame,
      handleClick
    }
  } 

})
</script>



<style lang="scss" scoped>
main {
  height: 100vh;

  .container__top{
    color: white

  }

  .container{
    display: flex;
    margin-top: 10px;    
    justify-content:center;

    .text-message{
      margin-bottom: 50px;
    }
    .grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-gap: 0px;
      width: 550px;
      
      .grid-div {
        border: 3px solid white;
      }
      
      :nth-child(3n) {
        border-right: none;
      }
      .grid-div:nth-child(-n + 3) {
        border-top: none;
      } 
      .grid-div:nth-child(3n  - 2) {
        border-left: none;
      } 
      .grid-div:nth-child(n + 7) {
        border-bottom: none;
      }
    
    }

    .box {
      height: 150px;
    }

    .resetBtn{
      margin-top: 50px;
    }
  }

  
}


</style>