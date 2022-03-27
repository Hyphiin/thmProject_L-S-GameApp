<template>
  <main
    class="d-flex flex-column justify-content-center align-items-center"
  >
    <div class="container">
      <div class="justify-content-center mt-3">
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
    <div class="scorefield">Score: {{ score }}</div>
  </main>
</template>

<script lang="ts">
import { defineComponent, toRef } from 'vue';

export default defineComponent({
  name: 'viewBoard',
  components: {},
  props: {
    currentBoard: {
      type: Array,
      required: true,
    },
    score: {
      type: Number,
      required: true,
    }
  },
  setup(props) {
    let board = toRef(props, 'currentBoard');

    return {
      board,
    };
  },
});
</script>

<style lang="scss" scoped>
main {
  //height: 10vh;
  //width: 10vh;
  margin-left: 5px;
  margin-bottom: 10px;
  border: solid 1px #201c24;
  border-radius: 12px;
  padding: 4px;

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
      width: 10px;

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
    width: 8px;
    height: 8px;
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
    grid-template-columns: repeat(5, auto);
  }

  .cell {
    width: 25px;
    height: 25px;
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
</style>
