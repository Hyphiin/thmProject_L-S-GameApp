<template>
  <main class="d-flex flex-column justify-content-center align-items-center">
    <div class="container">
      <div class="justify-content-center mt-3 container__container">
        <div class="container__top">
          <div class="row justify-content-center mt-3">
            <div class="col">
              <q-toggle
                class="toggle"
                :label="`${modiToggleName}`"
                color="blue"
                size="xl"
                checked-icon="computer"
                unchecked-icon="person"
                v-model="modiToggle"
              />
            </div>
            <div class="col">
              <q-toggle
                class="toggle"
                :label="`${signToggleName}`"
                :disable="modiToggle"
                color="blue"
                size="xl"
                checked-icon="radio_button_unchecked"
                unchecked-icon="close"
                v-model="signToggle"
              />
            </div>
            <div class="col">
              <q-btn
                class="resetBtn"
                round 
                color="primary" 
                icon="restart_alt"
                @click="reloadGame()"
              >
               <q-tooltip>
                Neues Spiel
              </q-tooltip>
            </q-btn>
            </div>
            <!-- <div class="col">
              <q-btn
                class="undoBtn"
                 round 
                 color="secondary" 
                 icon="undo" 
                @click="undoMove()"
              >
              <q-tooltip>
                Zug zurücksetzen
              </q-tooltip>
            </q-btn>
            </div> -->
          </div>
        </div>
        <div class="text-message text-center">
          <div v-if="!winMessage">
            <h4 class="headline" v-if="isCross">X ist dran!</h4>
            <h4 class="headline" v-if="!isCross">O ist dran!</h4>
          </div>
          <div v-else>
            <h4 class="text-warning">
              {{ winMessage.toUpperCase() }}
            </h4>
          </div>
        </div>

        <div class="board" id="board">
          <div class="cell" @click="makeMove(0, 0)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[0][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[0][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 0)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[0][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[0][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 0)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[0][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[0][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 0)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[0][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[0][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 0)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[0][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[0][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 1)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[1][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[1][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 1)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[1][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[1][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 1)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[1][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[1][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 1)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[1][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[1][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 1)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[1][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[1][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 2)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[2][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[2][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 2)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[2][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[2][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 2)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[2][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[2][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 2)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[2][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[2][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 2)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[2][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[2][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 3)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[3][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[3][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 3)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[3][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[3][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 3)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[3][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[3][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 3)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[3][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[3][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 3)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[3][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[3][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 4)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[4][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[4][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 4)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[4][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[4][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 4)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[4][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[4][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 4)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[4][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[4][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 4)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[4][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[4][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 5)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[5][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[5][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 5)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[5][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[5][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 5)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[5][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[5][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 5)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[5][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[5][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 5)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[5][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[5][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 6)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[6][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[6][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 6)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[6][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[6][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 6)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[6][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[6][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 6)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[6][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[6][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 6)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[6][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[6][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 7)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[7][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[7][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 7)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[7][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[7][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 7)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[7][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[7][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 7)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[7][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[7][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 7)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[7][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[7][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 8)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[8][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[8][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 8)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[8][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[8][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 8)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[8][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[8][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 8)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[8][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[8][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 8)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[8][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[8][4] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(0, 9)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[9][0] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[9][0] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(1, 9)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[9][1] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[9][1] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(2, 9)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[9][2] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[9][2] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(3, 9)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[9][3] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[9][3] === 'X'"
            />
          </div>
          <div class="cell" @click="makeMove(4, 9)">
            <img
              src="../assets/circleWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-if="board[9][4] === 'O'"
            />
            <img
              src="../assets/crossWhite.png"
              alt=""
              class="img-fluid zoomIn"
              v-else-if="board[9][4] === 'X'"
            />
          </div>
        </div>        
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue';

interface aMove {
  i: number;
  j: number;
}

export default defineComponent({
  name: 'GameSpecialTTT',
  components: {},
  setup() {
    let winMessage = ref<string>('');
    let isCross = ref<boolean>(true);

    let board : Array<Array<string>> = [
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', '']
    ];

    const round = ref<number>(0);

    let modiToggle = ref<boolean>(false);
    let modiToggleName = ref<string>('Mensch');
    let signToggle = ref<boolean>(false);
    let signToggleName = ref<string>('X');

    let ai = 'X';
    let human = 'O';
    let currentPlayer = human;


    const makeMove = (itemNumberCol: number, itemNumberRow: number) => {   
      if (
        typeof itemNumberCol === 'number' &&
        typeof itemNumberRow === 'number'
      ) {
        if (board[itemNumberRow][itemNumberCol] === '') {
          board[itemNumberRow][itemNumberCol] = isCross.value ? 'X' : 'O';
          isCross.value = !isCross.value;
        } else {
          alert('Already Filled!');
        }

        let result = checkWinner();

        if (result === 'X' || result === 'O') {
          console.log('Sieger ist: ', result);
          winMessage.value = `${result} hat gewonnen!`;
        } else if (result === 'tie') {
          console.log('Unentschieden!');
          winMessage.value = 'Unentschieden!';
        }

        if (currentPlayer === human) {
          currentPlayer = ai;
        } else {
          currentPlayer = human;
        }
      }

      if (modiToggle.value === true) {
        makeComputerMove();
      }
    };

    const makeComputerMove = () => {
      // AI to make its turn
      let bestScore = -1000;
      let move: aMove = { i: 0, j: 0};

      for (let i = 0; i < 10; i++) {
        for (let j = 0; j < 5; j++) {
          // Is the spot available?
          if (board[i][j] == '') {
            // exact copy of the gameboard
            board[i][j] = ai;
            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            let score: number = minimax(board, 3, false, -Infinity, Infinity);

            board[i][j] = '';
            if (score >= bestScore) {   
              // console.log('bestScore:', score)           
              if (score == bestScore){                
                move = {j, i};
              } else if (score > bestScore){
                bestScore = score;
                move = {j, i};
              }
            }
          }
        }
      }

      round.value++;

      board[move.i][move.j] = ai;
      isCross.value = !isCross.value;
      
      let result = checkWinner();

      if (result === 'X' || result === 'O') {
        console.log('Sieger ist: ', result);
        winMessage.value = `${result} hat gewonnen!`;
      } else if (result === 'tie') {
        console.log('Unentschieden!');
        winMessage.value = 'Unentschieden!';
      }

      if (currentPlayer === human) {
        currentPlayer = ai;
      } else {
        currentPlayer = human;
      }
    };

    const minimax = (
      board: Array<Array<string>>,
      depth: number,
      isMaximizing: boolean,
      alpha: number,
      beta: number
    ) => {
      let result = checkWinner();
      if (result !== null) {
        switch (result) {
          case 'X': {
            return 10;
          }
          case 'O': {
            return -10;
          }
          case 'tie': {
            return 0;
          }
        }
      }

      if(depth === 0) {
        return 0;
      }

      if (isMaximizing) {
        let bestScore = -1000;
        for (let i = 0; i < 10; i++) {
          for (let j = 0; j < 5; j++) {
            // Is the spot available?
            if (board[i][j] == '' && typeof depth === 'number') {
              board[i][j] = ai;

              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              let score = minimax(board, depth - 1, false, alpha, beta);
              
              board[i][j] = '';
              
              bestScore = Math.max(score, bestScore);
              // check for alpha
              alpha = Math.max(alpha, bestScore);
              // Check for alpha beta pruning
              if (beta <= alpha) {
               
                break;
              }
            }
          }
        }
        return bestScore;
      } else {
        let bestScore = 1000;
        for (let i = 0; i < 10; i++) {
          for (let j = 0; j < 5; j++) {
            // Is the spot available?
            if (board[i][j] == '' && typeof depth === 'number') {
              board[i][j] = human;

              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              let score = minimax(board, depth - 1, true, alpha, beta);
              
              board[i][j] = '';
              
              bestScore = Math.min(score, bestScore);
              // check for beta
              beta = Math.min(beta, bestScore);
              // Check for alpha beta pruning
              if (beta <= alpha) {
                
                break;
              }
            }
          }
        }
        return bestScore;
      }
    };

    function equals5(a: string, b: string, c: string, d: string, e: string) {
      return a == b && b == c && c == d && d == e && a != '';
    }

    const checkWinner = () => {
      //  checking  winner of the game
      let winner = null;

      // horizontal
      for (let i = 0; i < 10; i++) {
        if (equals5(board[i][0], board[i][1], board[i][2],  board[i][3], board[i][4])) {
          winner = board[i][0];
          console.log(winner, 'horizontal')
        }
      }

      // Vertical
      for (let j = 0; j < 5; j++) {
        for (let i = 0; i < 6; i ++) {
          if (equals5(board[i][j], board[i+1][j], board[i+2][j], board[i+3][j], board[i+4][j])) {
              winner = board[i][j];
              console.log(winner, 'vertical')
            }
        }
      }
    
      // Diagonal
      //left
      for (let j = 0; j < 5; j++) {
        if (equals5(board[j][0], board[j+1][1], board[j+2][2], board[j+3][3], board[j+4][4])) {
          winner = board[j][0];
          console.log(winner, 'links oben')
        }
      }
      for (let j = 9; j > 3; j--) {
        if (equals5(board[j][0], board[j-1][1], board[j-2][2], board[j-3][3], board[j-4][4])) {
          winner = board[j][9];
          console.log(winner, 'links unten')
        }
      }
      //right
      for (let j = 0; j < 5; j++) {
        if (equals5(board[4][j], board[3][j+1], board[2][j+2], board[1][j+3], board[0][j+4])) {
          winner = board[4][j];
          console.log(winner, 'rechts oben')
        }
      }
      for (let j = 9; j > 5; j--) {
        if (equals5(board[j][4], board[j-1][3], board[j-2][2], board[j-3][1], board[j-4][0])) {
          winner = board[j][4];
          console.log(winner, 'rechts unten')
        }
      }
      
      let openSpots = 0;
      for (let i = 0; i < 10; i++) {
        for (let j = 0; j < 5; j++) {
          if (board[i][j] == '') {
            openSpots++;
          }
        }
      }

      if (winner === null && openSpots === 0) {
        return 'tie';
      } else {
        return winner;
      }
    };

   
    const reloadGame = () => {  
      winMessage.value = '';
      for (let i = 0; i < 10; i++) {
        for (let j = 0; j < 5; j++) {
          board[i][j] = '';
        }
      }

      if(signToggle.value === false){
        isCross.value = true;
      } else {
        isCross.value = false;       
      }      

      if(modiToggle.value === false){
          modiToggleName.value = 'Mensch';         
      } else {
        modiToggleName.value = 'KI'; 
        signToggle.value = true;
        
        makeComputerMove()      
        isCross.value = false;   
      }
      
    };


    watch(
      () => modiToggle.value,
      () => {      
        if (modiToggle.value === false) {
          modiToggleName.value = 'Mensch';          
          reloadGame()          
        } else {
          modiToggleName.value = 'KI';          
          signToggle.value === true
          isCross.value = false
          signToggleName.value = 'O';
          ai = 'X';
          human = 'O';  
          reloadGame()       
        }
      }
    );

    watch(
      () => signToggle.value,
      () => {
        if (signToggle.value === true) {
          signToggleName.value = 'O';
          isCross.value = false
          ai = 'X';
          human = 'O';
        } else {
          signToggleName.value = 'X';
          isCross.value = true
          ai = 'O';
          human = 'X';
        }
        reloadGame()
      }
    );

    return {
      board,
      winMessage,
      isCross,
      modiToggle,
      modiToggleName,
      signToggle,
      signToggleName,
      reloadGame,
      makeMove
    };
  },
});
</script>

<style lang="scss" scoped>
main {
  margin: 10px 5px;

  .container__top {
    color: white;
  }

  .container {
    display: flex;
    margin-top: 10px;
    margin-left: 10px;
    justify-content: flex-start;

    .container__container {
      border-radius: 12px;
      padding: 50px;
      .text-message {
        margin-bottom: 50px;
      }

      .box {
        height: 150px;
      }

      .resetBtn {
        margin-top: 15px;
      }
      .undoBtn {
        margin-top: 15px;
      }
    }
  }

  img {
    width: 20px;
    height: 20px;
  }

  @keyframes zoomIn {
    from {
      opacity: 0;
      transform: scale3d(0.3, 0.3, 0.3);
    }

    50% {
      opacity: 1;
    }
  }

  .col {
    margin: 5px;
    min-width: 40px;
    .toggle {
      color: #201c24;
    }
  }

  .headline {
    color: #2074d4;
  }

  .zoomIn {
    animation-name: zoomIn;
    animation-duration: 1s;
  }

  .board {
    display: grid;
    justify-content: center;
    align-content: center;
    justify-items: center;
    align-items: center;
    grid-template-columns: repeat(5, auto);
    border-radius: 8px;
  }

  .cell {
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    cursor: pointer;
    margin: 2px;
    background-color: #201c24;
    border-radius: 8px;

    .img-fluid {
      filter: invert(34%) sepia(99%) saturate(1121%) hue-rotate(191deg)
        brightness(88%) contrast(88%);
    }
  }

  .cell:first-child,
  .cell:nth-child(2),
  .cell:nth-child(3) {
    border-top: none;
  }

  .cell:nth-child(3n + 1) {
    border-left: none;
  }

  .cell:nth-child(3n + 3) {
    border-right: none;
  }

  .cell:last-child,
  .cell:nth-child(8),
  .cell:nth-child(7) {
    border-bottom: none;
  }

  .cell.x,
  .cell.circle {
    cursor: not-allowed;
  }

  .cell.x::before,
  .cell.x::after,
  .cell.circle::before {
    background-color: black;
  }

  .board.x .cell:not(.x):not(.circle):hover::before,
  .board.x .cell:not(.x):not(.circle):hover::after,
  .board.circle .cell:not(.x):not(.circle):hover::before {
    background-color: lightgrey;
  }

  .cell.x::before,
  .cell.x::after,
  .board.x .cell:not(.x):not(.circle):hover::before,
  .board.x .cell:not(.x):not(.circle):hover::after {
    content: '';
    position: absolute;
    width: calc(calc(var(40px) * 0.9) * 0.15);
    height: calc(var(40px) * 0.9);
  }

  .cell.x::before,
  .board.x .cell:not(.x):not(.circle):hover::before {
    transform: rotate(45deg);
  }

  .cell.x::after,
  .board.x .cell:not(.x):not(.circle):hover::after {
    transform: rotate(-45deg);
  }

  .cell.circle::before,
  .cell.circle::after,
  .board.circle .cell:not(.x):not(.circle):hover::before,
  .board.circle .cell:not(.x):not(.circle):hover::after {
    content: '';
    position: absolute;
    border-radius: 50%;
  }

  .cell.circle::before,
  .board.circle .cell:not(.x):not(.circle):hover::before {
    width: calc(var(40px) * 0.9);
    height: calc(var(40px) * 0.9);
  }

  .cell.circle::after,
  .board.circle .cell:not(.x):not(.circle):hover::after {
    width: calc(calc(var(40px) * 0.9) * 0.7);
    height: calc(calc(var(40px) * 0.9) * 0.7);
    background-color: white;
  }
}
</style>
