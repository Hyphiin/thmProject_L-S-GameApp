<template>
  <main
    class="d-flex flex-column justify-content-center align-items-center bg-dark"
  >
    <div class="container__top">
      <div class="row justify-content-center mt-3">
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
        <div class="col"></div>
      </div>
    </div>

    <div class="container">
      <div class="justify-content-center mt-3">
        <div class="text-message text-center">
          <div v-if="!winMessage">
            <h4 class="text-info" v-if="isCross">X ist dran!</h4>
            <h4 class="text-info" v-if="!isCross">O ist dran!</h4>
          </div>
          <div v-else>
            <h3 class="text-warning">
              {{ winMessage.toUpperCase() }}
            </h3>
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
        </div>

        <div class="col col-6">
          <q-btn
            class="resetBtn"
            outline
            style="color: goldenrod"
            label="Reset the game"
            @click="reloadGame()"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue';
import {aiMove} from './aiMove';

interface aMove {
  i: number,
  j: number
}

interface boardState {
  state: Array<Array<string>>,
  round: number
}

export default defineComponent({
  name: 'GameTicTacToe',
  components: {},
  setup(props, context) {
    
    let winMessage = ref<string>('');
    let isCross = ref<boolean>(true);

    let board: Array<Array<string>> = [
      ['', '', ''],
      ['', '', ''],
      ['', '', ''],
    ];

    const possibleMoves = ref<aiMove[]>([])

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
      console.log('ComputerMove');
      // AI to make its turn
      let bestScore = -Infinity;
      let move: aMove = {i: 0, j: 0};

      possibleMoves.value = []

      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          // Is the spot available?
          if (board[i][j] == '') {
            board[i][j] = ai;

            // exact copy of the gameboard
            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            const gameState = JSON.parse(JSON.stringify(board));
            //console.log(gameState)
            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            const boardStatus: boardState = {state: gameState, round: round.value}
            context.emit('boardState', boardStatus);
            
            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            let score: number = minimax(board, 0, false, -Infinity, Infinity);
 
            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            let scoreCopy: number = JSON.parse(JSON.stringify(score));

            // eslint-disable-next-line @typescript-eslint/no-unsafe-call
            possibleMoves.value.push({x: i, y: j, score: scoreCopy})

            board[i][j] = '';
            if (score > bestScore) {    
              bestScore = score;
              move = { j, i };
            }
          }
        }
      }

      round.value ++;
      
      board[move.i][move.j] = ai;
      isCross.value = !isCross.value;

      //console.log(possibleMoves.value)
      context.emit('possibleMoves', possibleMoves.value)
      context.emit('board', board)

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

    const minimax = (board: Array<Array<string>>, depth: number, isMaximizing: boolean, alpha: number, beta: number) => {
      let result = checkWinner();
      if (result !== null) {
        switch(result) {
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

      if (isMaximizing) {
        let bestScore = -Infinity;
        for (let i = 0; i < 3; i++) {
          for (let j = 0; j < 3; j++) {
            // Is the spot available?
            if (board[i][j] == '' && typeof depth === 'number') {
              board[i][j] = ai;
              
              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              let score = minimax(board, depth + 1, false, alpha, beta);
              //console.log('Maximizing:::', 'Spalte: ', i, 'Reihe: ',j, 'Tiefe: ',  depth, 'score: ', score);
              board[i][j] = '';
              // console.log(score)
              bestScore = Math.max(score, bestScore);
              // check for alpha
              alpha = Math.max(alpha, bestScore);
              // Check for alpha beta pruning
              if (beta <= alpha) {
                //console.log('Maximizing Prune:::', 'Spalte: ', i, 'Reihe: ',j, 'Tiefe: ',  depth, 'score: ', score);
                break;
              }
            }
          }
        }
        return bestScore;
      } else {
        let bestScore = Infinity;
        for (let i = 0; i < 3; i++) {
          for (let j = 0; j < 3; j++) {
            // Is the spot available?
            if (board[i][j] == '' && typeof depth === 'number') {
              board[i][j] = human;
              
              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              let score = minimax(board, depth + 1, true, alpha, beta);
              //console.log('Minimizing:::', 'Spalte: ', i, 'Reihe: ',j, 'Tiefe: ',  depth, 'score: ', score);
              board[i][j] = '';
              // console.log(score)
              bestScore = Math.min(score, bestScore);
              // check for beta
              beta = Math.min(beta, bestScore);
              // Check for alpha beta pruning
              if (beta <= alpha) {
                //console.log('Minimizing Prune:::', 'Spalte: ', i, 'Reihe: ',j, 'Tiefe: ',  depth, 'score: ', score);
                break;
              }
            }
          }
        }
        return bestScore;
      }
    };

    function equals3(a: string, b: string, c: string) {
      return a == b && b == c && a != '';
    }

    const checkWinner = () => {
      //  checking  winner of the game
      let winner = null;

      // horizontal
      for (let i = 0; i < 3; i++) {
        if (equals3(board[i][0], board[i][1], board[i][2])) {
          winner = board[i][0];
        }
      }

      // Vertical
      for (let i = 0; i < 3; i++) {
        if (equals3(board[0][i], board[1][i], board[2][i])) {
          winner = board[0][i];
        }
      }

      // Diagonal
      if (equals3(board[0][0], board[1][1], board[2][2])) {
        winner = board[0][0];
      }
      if (equals3(board[2][0], board[1][1], board[0][2])) {
        winner = board[2][0];
      }

      let openSpots = 0;
      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
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
      if(!signToggle.value){
        isCross.value = true;
        signToggleName.value = 'X';
      } else {
        isCross.value = false;
        signToggleName.value = 'O';
      }
      if(!modiToggle.value){
        modiToggleName.value = 'Mensch';
      } else {
        modiToggleName.value = 'KI';
      }

      if(modiToggleName.value == 'KI'){
         makeComputerMove();
      }

      /*modiToggle.value = false;
      signToggle.value = false;
      modiToggleName.value = 'Mensch';
      signToggleName.value = 'X';
      */

      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          board[i][j] = '';
        }
      }
    };

    watch(
      () => modiToggle.value,
      () => {        
        if (modiToggleName.value === 'Mensch') {
          modiToggleName.value = 'KI';
          //signToggleName.value = 'O';
          reloadGame()
          makeComputerMove();
        } else {
          modiToggleName.value = 'Mensch';
          reloadGame()
          //signToggleName.value = 'X';
        }
        console.log(modiToggle.value, modiToggleName.value);
      }
    );

    watch(
      () => signToggle.value,
      () => {
        if (signToggleName.value === 'X') {
          signToggleName.value = 'O';
          isCross.value = false
          ai = 'O';
          human = 'X';
        } else {
          signToggleName.value = 'X';
          isCross.value = true
          ai = 'X';
          human = 'O';
        }
        console.log(signToggle.value, signToggleName.value);
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
      makeMove,
    };
  },
});
</script>

<style lang="scss" scoped>
main {
  height: 100vh;

  .container__top {
    color: white;
  }

  .container {
    display: flex;
    margin-top: 10px;
    justify-content: center;

    .text-message {
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
      .grid-div:nth-child(3n - 2) {
        border-left: none;
      }
      .grid-div:nth-child(n + 7) {
        border-bottom: none;
      }
    }

    .box {
      height: 150px;
    }

    .resetBtn {
      margin-top: 50px;
    }
  }

  img {
    width: 80px;
    height: 80px;
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
    grid-template-columns: repeat(3, auto);
  }

  .cell {
    width: 100px;
    height: 100px;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    cursor: pointer;
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
    width: calc(calc(var(100px) * 0.9) * 0.15);
    height: calc(var(100px) * 0.9);
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
    width: calc(var(100px) * 0.9);
    height: calc(var(100px) * 0.9);
  }

  .cell.circle::after,
  .board.circle .cell:not(.x):not(.circle):hover::after {
    width: calc(calc(var(100px) * 0.9) * 0.7);
    height: calc(calc(var(100px) * 0.9) * 0.7);
    background-color: white;
  }
}
</style>
