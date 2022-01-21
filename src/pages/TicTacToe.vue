<template>
  <q-layout view="hHh lpR fFf " class="row">
    <q-page-container class="game col">
      <game-tic-tac-toe
        @possible-moves="receivePossibleMoves($event)"
        @board="receiveBoard($event)"
        @boardState="receiveBoardState($event)"
        boardState
        :board-game="board"
      />
    </q-page-container>
    <q-page-container class="tree col text-center">
      <main class="d-flex flex-column justify-content-center align-items-center">
      <h5 v-if="possibleMoves.length > 1">Auswahl an Zügen:</h5>
      <div class="possibleMoves" v-if="boardStates.length > 1">
        <div v-for="(entry, index) in boardStates" :key="index">
          <view-board :current-board="entry.state" :id="index" />
        </div>
      </div>
      <div v-if="possibleMoves.length > 1" class="scoreBoard">
        <div v-for="(entry, index) in possibleMoves" :key="index" class="scorefield">
          Score: {{ entry.score }}
        </div>
      </div>
      <h5>Ausgewählter Zug:</h5>
      <div class="placeholder">
        <div class="container">
          <div class="justify-content-center mt-3">
            <div class="board" id="board">
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[0][0] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[0][0] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[0][1] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[0][1] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[0][2] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[0][2] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[1][0] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[1][0] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[1][1] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[1][1] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[1][2] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[1][2] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[2][0] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[2][0] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[2][1] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[2][1] === 'X'"
                />
              </div>
              <div class="cell">
                <img
                  src="../assets/circle-regular.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-if="currentBoard[2][2] === 'O'"
                />
                <img
                  src="../assets/Feather-core-triangle.svg"
                  alt=""
                  class="img-fluid zoomIn"
                  v-else-if="currentBoard[2][2] === 'X'"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
      </main>
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue';
import GameTicTacToe from './GameTicTacToe.vue';
import viewBoard from './viewBoard.vue';
import { aiMove } from './aiMove';

interface boardState {
  [index: string]: Array<Array<string>> | number;
  state: Array<Array<string>>;
  round: number;
}

export default defineComponent({
  name: 'TicTacToe',
  components: { GameTicTacToe, viewBoard },
  setup() {
    let board: Array<Array<string>> = [
      ['', '', ''],
      ['', '', ''],
      ['', '', ''],
    ];

    const possibleMoves = ref<aiMove[]>([]);
    const currentBoard = ref<Array<Array<string>>>(board);

    const boardStates = ref<boardState[]>([]);
    const round = ref<number>(0);

    const receivePossibleMoves = (gameState: aiMove[]) => {
      possibleMoves.value = gameState;
    };

    const receiveBoard = (board: Array<Array<string>>) => {
      //console.log(receiveBoard);
      currentBoard.value = board;
    };

    const receiveBoardState = (boardState: boardState) => {
      if (round.value === boardState.round) {
        boardStates.value.push(boardState);
        console.log(boardStates.value);
      } else {
        boardStates.value = [];
        round.value++;
        boardStates.value.push(boardState);
      }
    };

    const states = computed(() => {
      return boardStates;
    });

    return {
      board,
      possibleMoves,
      currentBoard,
      boardStates,
      receivePossibleMoves,
      receiveBoard,
      receiveBoardState,
      states,
    };
  },
});
</script>
<style lang="scss" scoped>
.placeholder {
  height: 20vh;
  width: 100%;
  display: flex;
  justify-content: center;

  .container__top {
    color: white;
  }

  .container {
    display: flex;
    justify-content: center;

    .grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-gap: 0px;
      width: 55px;

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
      height: 15px;
    }
  }

  img {
    width: 25px;
    height: 25px;
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

  .container.bg-dark {
    max-height: 80%;
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
    width: 50px;
    height: 50px;
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
    width: calc(calc(var(10px) * 0.9) * 0.15);
    height: calc(var(10px) * 0.9);
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
    width: calc(var(10px) * 0.9);
    height: calc(var(10px) * 0.9);
  }

  .cell.circle::after,
  .board.circle .cell:not(.x):not(.circle):hover::after {
    width: calc(calc(var(10px) * 0.9) * 0.7);
    height: calc(calc(var(10px) * 0.9) * 0.7);
    background-color: white;
  }
}
.possibleMoves {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.scoreBoard {
  display: flex;
  flex-direction: row;
  justify-content: space-around;

  .scorefield {
    min-width: 50px;
    margin-right: 20px;
    color: #201c24;
  }
}
</style>
