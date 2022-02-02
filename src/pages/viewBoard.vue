<template>
  <main class="d-flex flex-column justify-content-center align-items-center">
    <div class="container">
      <div class="justify-content-center mt-3">
        <div class="board" id="board">
          <div class="cell">
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
          <div class="cell">
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
          <div class="cell">
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
          <div class="cell">
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
          <div class="cell">
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
          <div class="cell">
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
          <div class="cell">
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
          <div class="cell">
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
          <div class="cell">
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
    },
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
    grid-template-columns: repeat(3, auto);
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
