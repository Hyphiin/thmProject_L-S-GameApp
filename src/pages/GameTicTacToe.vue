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
            <div class="col">
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
            </div>
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
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue';
import { aiMove } from './aiMove';

interface aMove {
  i: number;
  j: number;
}

interface boardState {
  state: Array<Array<string>>;
  round: number;
  score: number;
}

export default defineComponent({
  name: 'GameTicTacToe',
  components: {},
  setup(props, context) {
    let winMessage = ref<string>('');
    let isCross = ref<boolean>(true);

    let board = ref<Array<Array<string>>>([
      ['', '', ''],
      ['', '', ''],
      ['', '', ''],
    ]);

    const possibleMoves = ref<aiMove[]>([]);

    const round = ref<number>(0);

    let modiToggle = ref<boolean>(false);
    let modiToggleName = ref<string>('Mensch');
    let signToggle = ref<boolean>(false);
    let signToggleName = ref<string>('X');

    let ai = 'X';
    let human = 'O';
    let currentPlayer = human;

    const lastMovesArray = ref<Array<aMove>>([])

    const makeMove = (itemNumberCol: number, itemNumberRow: number) => {   
      if (
        typeof itemNumberCol === 'number' &&
        typeof itemNumberRow === 'number'
      ) {
        if (board.value[itemNumberRow][itemNumberCol] === '') {
          board.value[itemNumberRow][itemNumberCol] = isCross.value ? 'X' : 'O';
          isCross.value = !isCross.value;
          lastMovesArray.value.push( { i: itemNumberRow, j: itemNumberCol})
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
      let bestScore = -Infinity;
      let move: aMove = { i: 0, j: 0};
      let bestMovesArray = Array<aMove>()

      possibleMoves.value = [];

      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          // Is the spot available?
          if (board.value[i][j] == '') {
            board.value[i][j] = ai;

            // exact copy of the gameboard

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            const gameState = JSON.parse(JSON.stringify(board.value));
            //console.log(gameState)

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            let score: number = minimax(board.value, 0, false, -Infinity, Infinity);

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            const boardStatus: boardState = {
              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              state: gameState,
              round: round.value,
              score: score,
            };
            context.emit('boardState', boardStatus);

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            let scoreCopy: number = JSON.parse(JSON.stringify(score));

            // eslint-disable-next-line @typescript-eslint/no-unsafe-call
            possibleMoves.value.push({ x: i, y: j, score: scoreCopy });

            board.value[i][j] = '';
            if (score >= bestScore) {   
              // console.log('bestScore:', score)           
              if (score == bestScore){                
                move = {j, i};
                bestMovesArray.push(move)
              } else if (score > bestScore){
                bestScore = score;
                move = {j, i};
                bestMovesArray = []    
                bestMovesArray.push(move)
              }
              // console.log('bestScoreArray:', bestMovesArray) 
            }
          }
        }
      }

      round.value++;

      let tempVar = Math.floor(Math.random() * bestMovesArray.length ) 
      move = {j: bestMovesArray[tempVar].j, i: bestMovesArray[tempVar].i};

      board.value[move.i][move.j] = ai;
      isCross.value = !isCross.value;
      lastMovesArray.value.push({ i: move.i, j: move.j})
      
      //console.log(possibleMoves.value)
      context.emit('possibleMoves', possibleMoves.value);
      context.emit('board.value', board.value);

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

    const undoMove = () => {      
      if (lastMovesArray.value != undefined) {
        if(modiToggle.value === true){
          let tempMove = lastMovesArray.value[lastMovesArray.value.length-1]
          board.value[tempMove.i][tempMove.j] = '';
          lastMovesArray.value?.pop()
          tempMove = lastMovesArray.value[lastMovesArray.value.length-1]
          board.value[tempMove.i][tempMove.j] = '';
          lastMovesArray.value?.pop()
        } else{
          let tempMove = lastMovesArray.value[lastMovesArray.value.length-1]
          board.value[tempMove.i][tempMove.j] = '';
          lastMovesArray.value?.pop()
        }        
      }
      context.emit('possibleMoves', possibleMoves.value);
      context.emit('board', board);
    };

    const checkWinner = () => {
      //  checking  winner of the game
      let winner = null;

      // horizontal
      for (let i = 0; i < 3; i++) {
        if (equals3(board.value[i][0], board.value[i][1], board.value[i][2])) {
          winner = board.value[i][0];
        }
      }

      // Vertical
      for (let i = 0; i < 3; i++) {
        if (equals3(board.value[0][i], board.value[1][i], board.value[2][i])) {
          winner = board.value[0][i];
        }
      }

      // Diagonal
      if (equals3(board.value[0][0], board.value[1][1], board.value[2][2])) {
        winner = board.value[0][0];
      }
      if (equals3(board.value[2][0], board.value[1][1], board.value[0][2])) {
        winner = board.value[2][0];
      }

      let openSpots = 0;
      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          if (board.value[i][j] == '') {
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
      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          board.value[i][j] = '';
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
      makeMove,
      undoMove
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

  .col {
    margin: 5px;
    min-width: 100px;
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
    grid-template-columns: repeat(3, auto);
    border-radius: 8px;
  }

  .cell {
    width: 100px;
    height: 100px;
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
