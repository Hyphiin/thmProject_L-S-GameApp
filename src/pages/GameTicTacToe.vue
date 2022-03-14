<template>
  <main class="main-box d-flex flex-column justify-content-center">
    <q-page-container class="game col">
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
                  <q-tooltip> Neues Spiel </q-tooltip>
                </q-btn>
              </div>
              <div class="col">
                <q-btn
                  class="undoBtn"
                  round
                  color="primary"
                  icon="undo"
                  @click="undoMove()"
                >
                  <q-tooltip> Zug zurücksetzen </q-tooltip>
                </q-btn>
              </div>
              <div class="col">
                <q-btn-toggle
                  v-model="searchDepth"
                  toggle-color="primary"
                  glossy
                  text-color="primary"
                  :options="[
                    { label: '1', value: 1 },
                    { label: '2', value: 2 },
                    { label: '3', value: 3 },
                  ]"
                />
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

          <div class="board" id="board" :class="winMessage ? 'disabled' : ''">
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
    </q-page-container>
    <q-page-container class="tree col text-center">
      <div class="possibleMoves__container">
        <div class="possibleMoves" v-if="boardStatesComp.value.length > 1">
          <div v-for="(entry, index) in boardStatesComp.value" :key="index">
            <view-board
              :current-board="entry.state"
              :id="index"
              :score="entry.score"
              :class="checkChoosenMove(entry.state) ? 'trueStyle' : ''"
            />
          </div>
        </div>
        <div class="possibleMovesTree">
          <div v-for="(entry, index) in treeArrayFinal" :key="index">
            <q-tree
              :nodes="entry.tree"
              node-key="key"
              :default-expand-all="entry.tree[0].icon === 'star' ? true : false"
            />
          </div>
        </div>
      </div>
    </q-page-container>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref, watch, computed } from 'vue';
import { aiMove } from './aiMove';
import viewBoard from './viewBoard.vue';
import _, { isUndefined } from 'lodash';
//import { nextTick } from 'process';

interface aMove {
  i: number;
  j: number;
}

interface boardState {
  state: Array<Array<string>>;
  round: number;
  score: number;
  key: number;
}

interface tree {
  label: string;
  key: string;
  tree: [
    {
      label: string;
      key: number;
      icon: string;
      children?: [
        {
          label: string;
          key: number;
          avatar: string;
          children?: treeChild[];
        }
      ];
    }
  ];
}

interface treeChild {
  label: string;
  key: number;
  children?: treeChild[];
}

export default defineComponent({
  name: 'GameTicTacToe',
  components: { viewBoard },
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

    let searchDepth = ref<number>(1);

    const lastMovesArray = ref<Array<aMove>>([]);

    let treeArray = ref<tree[]>([]);
    let treeArrayFinal = ref<tree[]>([]);

    const makeMove = (itemNumberCol: number, itemNumberRow: number) => {
      if (
        typeof itemNumberCol === 'number' &&
        typeof itemNumberRow === 'number'
      ) {
        if (board.value[itemNumberRow][itemNumberCol] === '') {
          board.value[itemNumberRow][itemNumberCol] = isCross.value ? 'X' : 'O';
          isCross.value = !isCross.value;
          lastMovesArray.value.push({ i: itemNumberRow, j: itemNumberCol });
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
          if (modiToggle.value) {
            makeComputerMove();
          }
        } else {
          currentPlayer = human;
        }
      }
    };

    const boardStates = ref<boardState[]>([]);

    const boardStatesComp = computed(() => {
      return boardStates;
    });
    let counter = 0;

    const makeComputerMove = () => {
      // AI to make its turn
      let bestScore = -Infinity;
      let move: aMove = { i: 0, j: 0 };
      let bestMovesArray = Array<aMove>();

      possibleMoves.value = [];

      treeArray.value = [];
      treeArrayFinal.value = [];

      boardStates.value = [];

      let tempTree: tree = {
        label: '',
        key: counter.toString(),
        tree: [
          {
            label: counter.toString(),
            key: counter,
            icon: 'share',
            children: [
              {
                label: 'test',
                key: 0,
                avatar: 'assets/bear.webp',
              },
            ],
          },
        ],
      };

      let tempNumber = 0;

      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          // Is the spot available?
          if (board.value[i][j] == '') {
            // exact copy of the gameboard
            board.value[i][j] = ai;

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            const gameState = JSON.parse(JSON.stringify(board.value));
            //console.log(gameState)

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            let score: number = minimax(
              board.value,
              searchDepth.value,
              true,
              -Infinity,
              Infinity,
              counter
            );

            if (searchDepth.value === 2 || searchDepth.value === 3) {
              // tempTree.tree[0].children?.pop();
              // console.log('tempNumber: ', tempNumber);
              for (let i = 1; i < treeArray.value.length; i++) {
                if (treeArray.value[i].key === tempNumber.toString()) {
                  //console.log('treeArray: ', treeArray.value[i].key);
                  // tempTree.tree[0].children?.push({
                  //   label: treeArray.value[i].tree[0].label,
                  //   key: treeArray.value[i].tree[0].key,
                  //   img: '',
                  // });
                } else {
                  //console.log('nope');
                }
              }
              tempNumber++;
              // treeArrayFinal.value.push(tempTree);
            } else {
              treeArrayFinal.value = treeArray.value;
            }

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            const boardStatus: boardState = {
              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              state: gameState,
              round: round.value,
              score: score,
              key: counter,
            };

            //console.log(boardStates.value);
            context.emit('boardState', boardStatus);

            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
            let scoreCopy: number = JSON.parse(JSON.stringify(score));

            // eslint-disable-next-line @typescript-eslint/no-unsafe-call
            possibleMoves.value.push({ x: i, y: j, score: scoreCopy });

            board.value[i][j] = '';
            if (score >= bestScore) {
              // console.log('bestScore:', score)
              if (score == bestScore) {
                move = { j, i };
                bestMovesArray.push(move);
              } else if (score > bestScore) {
                bestScore = score;
                move = { j, i };
                bestMovesArray = [];
                bestMovesArray.push(move);
              }
              // console.log('bestScoreArray:', bestMovesArray)
            }
            if (round.value === boardStatus.round) {
              boardStates.value.push(boardStatus);
            } else {
              boardStates.value = [];
              round.value++;
              boardStates.value.push(boardStatus);
            }
          }
          counter++;
        }
      }

      if (searchDepth.value === 2 || searchDepth.value === 3) {
        console.log(treeArray.value);
        let tempTreeArray: tree[] = [];
        let currentElement = treeArray.value[0].tree[0].key;

        treeArray.value.forEach((entry, index) => {
          tempTree.tree[0].children?.pop();

          if (currentElement === entry.tree[0].key) {
            tempTreeArray.push(entry);

            if (index === treeArray.value.length - 1) {
              currentElement = entry.tree[0].key;
              console.log(tempTreeArray);
              tempTreeArray.forEach((element, index) => {
                tempTree.tree[0].children?.push({
                  label: element.tree[0].label,
                  key: element.tree[0].key + 0.1 * index + 1,
                  avatar: 'assets/bear.webp',
                });
              });

              treeArrayFinal.value.push(tempTree);
              tempTree = {
                label: '',
                key: counter.toString(),
                tree: [
                  {
                    label: counter.toString(),
                    key: counter,
                    icon: 'share',
                    children: [
                      {
                        label: 'test',
                        key: 0,
                        avatar: 'assets/bear.webp',
                      },
                    ],
                  },
                ],
              };
              tempTreeArray = [];
            }
          } else {
            currentElement = entry.tree[0].key;
            console.log(tempTreeArray);
            tempTreeArray.forEach((element, index) => {
              tempTree.tree[0].children?.push({
                label: element.tree[0].label,
                key: element.tree[0].key + 0.1 * index + 1,
                avatar: 'assets/bear.webp',
              });
            });

            treeArrayFinal.value.push(tempTree);
            tempTree = {
              label: '',
              key: counter.toString(),
              tree: [
                {
                  label: counter.toString(),
                  key: counter,
                  icon: 'share',
                  children: [
                    {
                      label: 'test',
                      key: 0,
                      avatar: 'assets/bear.webp',
                    },
                  ],
                },
              ],
            };
            tempTreeArray = [];
          }
        });
      }

      round.value++;

      // let tempVar = Math.floor(Math.random() * bestMovesArray.length);

      move = { j: bestMovesArray[0].j, i: bestMovesArray[0].i };

      board.value[move.i][move.j] = ai;
      isCross.value = !isCross.value;
      lastMovesArray.value.push({ i: move.i, j: move.j });

      //console.log(possibleMoves.value)
      context.emit('possibleMoves', possibleMoves.value);
      context.emit('board', board.value);

      let result = checkWinner();

      if (result === 'X' || result === 'O') {
        console.log('Sieger ist: ', result);
        winMessage.value = `${result} hat gewonnen!`;
      } else if (result === 'tie') {
        console.log('Unentschieden!');
        winMessage.value = 'Unentschieden!';
      }

      //check which tree is the choosen one
      let tempKey = -1;
      for (let i = 0; i < boardStates.value.length; i++) {
        if (checkChoosenMove(boardStates.value[i].state)) {
          tempKey = boardStates.value[i].key;
        }
      }

      for (let i = 0; i < treeArrayFinal.value.length; i++) {
        treeArrayFinal.value[i].tree[0].label =
          boardStates.value[i].score.toString();
        treeArrayFinal.value[i].tree[0].key = boardStates.value[i].key;

        if (treeArrayFinal.value[i].key === tempKey.toString()) {
          treeArrayFinal.value[i].tree[0].icon = 'star';
        }
      }

      if (currentPlayer === human) {
        currentPlayer = ai;
      } else {
        currentPlayer = human;
      }

      console.log('TreeArrayFinal: ', treeArrayFinal.value);
    };

    const minimax = (
      board: Array<Array<string>>,
      depth: number,
      isMaximizing: boolean,
      alpha: number,
      beta: number,
      counter: number
    ) => {
      let tempTree: tree = {
        label: '',
        key: counter.toString(),
        tree: [
          {
            label: '',
            key: counter,
            icon: 'share',
          },
        ],
      };

      let result = checkWinner();
      if (result !== null) {
        switch (result) {
          case 'X': {
            tempTree.tree[0].label = 'win: 10';
            tempTree.label = 'win: 10';
            treeArray.value.push(tempTree);
            return 10;
          }
          case 'O': {
            return -10;
          }
          case 'tie': {
            tempTree.tree[0].label = 'tie: 0';
            tempTree.label = 'tie: 0';
            treeArray.value.push(tempTree);
            return 0;
          }
        }
      }
      //winner tree fehlt,

      if (depth === 0) {
        return 0;
      }

      if (isMaximizing === true) {
        // console.log('Max is picking: ');
        let bestScore = -Infinity;
        for (let i = 0; i < 3; i++) {
          for (let j = 0; j < 3; j++) {
            // Is the spot available?
            if (board[i][j] == '' && typeof depth === 'number') {
              board[i][j] = ai;

              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              let score = minimax(
                board,
                depth - 1,
                false,
                alpha,
                beta,
                counter
              );

              board[i][j] = '';

              bestScore = Math.max(score, bestScore);
              // check for alpha
              alpha = Math.max(alpha, bestScore);
              // Check for alpha beta pruning
              if (beta <= alpha) {
                tempTree.label = 'pruned -> bestScore: ' + alpha.toString();
                tempTree.tree[0].label =
                  'pruned -> bestScore: ' + alpha.toString();
                break;
              }
              tempTree.label = bestScore.toString();
              tempTree.tree[0].label = bestScore.toString();
            }
          }
        }

        treeArray.value.push(tempTree);

        return bestScore;
      } else {
        // console.log('Min is picking: ');
        let bestScore = Infinity;
        for (let i = 0; i < 3; i++) {
          for (let j = 0; j < 3; j++) {
            // Is the spot available?
            if (board[i][j] == '' && typeof depth === 'number') {
              board[i][j] = human;

              // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
              let score = minimax(board, depth - 1, true, alpha, beta, counter);

              board[i][j] = '';

              bestScore = Math.min(score, bestScore);
              // check for beta
              beta = Math.min(beta, bestScore);
              // Check for alpha beta pruning
              if (beta <= alpha) {
                tempTree.label = 'pruned -> bestScore: ' + alpha.toString();
                tempTree.tree[0].label =
                  'pruned -> bestScore: ' + alpha.toString();
                break;
              }
              tempTree.label = bestScore.toString();
              tempTree.tree[0].label = bestScore.toString();
            }
          }
        }
        treeArray.value.push(tempTree);

        return bestScore;
      }
    };

    // function syncDelay(milliseconds: number) {
    //   var start = new Date().getTime();
    //   var end = 0;
    //   while (end - start < milliseconds) {
    //     end = new Date().getTime();
    //   }
    // }

    // function findIcon(row: number, column: number) {
    //   switch (row) {
    //     case 0: {
    //       switch (column) {
    //         case 0: {
    //           return 'oben_links.png';
    //         }
    //         case 1: {
    //           return 'oben_mitte.png';
    //         }
    //         case 2: {
    //           return 'oben_rechts.png';
    //         }
    //       }
    //     }
    //     case 1: {
    //       switch (column) {
    //         case 0: {
    //           return 'mitte_links.png';
    //         }
    //         case 1: {
    //           return 'mitte_mitte.png';
    //         }
    //         case 2: {
    //           return 'mitte_rechts.png';
    //         }
    //       }
    //     }
    //     case 2: {
    //       switch (column) {
    //         case 0: {
    //           return 'unten_links.png';
    //         }
    //         case 1: {
    //           return 'unten_mitte.png';
    //         }
    //         case 2: {
    //           return 'unten_rechts.png';
    //         }
    //       }
    //     }
    //   }
    // }

    function equals3(a: string, b: string, c: string) {
      return a == b && b == c && a != '';
    }

    const undoMove = () => {
      if (lastMovesArray.value != undefined) {
        if (modiToggle.value === true) {
          let tempMove = lastMovesArray.value[lastMovesArray.value.length - 1];
          board.value[tempMove.i][tempMove.j] = '';
          lastMovesArray.value?.pop();
          tempMove = lastMovesArray.value[lastMovesArray.value.length - 1];
          board.value[tempMove.i][tempMove.j] = '';
          lastMovesArray.value?.pop();
        } else {
          let tempMove = lastMovesArray.value[lastMovesArray.value.length - 1];
          board.value[tempMove.i][tempMove.j] = '';
          lastMovesArray.value?.pop();
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

      if (signToggle.value === false) {
        isCross.value = true;
      } else {
        isCross.value = false;
      }

      if (modiToggle.value === false) {
        modiToggleName.value = 'Mensch';
        currentPlayer = human;
      } else {
        modiToggleName.value = 'KI';
        signToggle.value = true;
        currentPlayer = ai;
        makeComputerMove();
        isCross.value = false;
      }
    };

    watch(
      () => modiToggle.value,
      () => {
        if (modiToggle.value === false) {
          modiToggleName.value = 'Mensch';
          reloadGame();
        } else {
          modiToggleName.value = 'KI';
          signToggle.value === true;
          isCross.value = false;
          signToggleName.value = 'O';
          ai = 'X';
          human = 'O';
          reloadGame();
        }
      }
    );

    watch(
      () => signToggle.value,
      () => {
        if (signToggle.value === true) {
          signToggleName.value = 'O';
          isCross.value = false;
          ai = 'X';
          human = 'O';
        } else {
          signToggleName.value = 'X';
          isCross.value = true;
          ai = 'O';
          human = 'X';
        }
      }
    );

    const checkChoosenMove = (entryState: Array<Array<string>>): boolean => {
      var temp = false;
      for (var i = 0; i < 4; i++) {
        if (
          entryState[0][i] === board.value[0][i] &&
          entryState[1][i] === board.value[1][i] &&
          entryState[2][i] === board.value[2][i]
        ) {
          temp = true;
        } else {
          temp = false;
          return temp;
        }
      }
      return temp;
    };

    return {
      board,
      winMessage,
      isCross,
      modiToggle,
      modiToggleName,
      signToggle,
      signToggleName,
      searchDepth,
      possibleMoves,
      boardStates,
      treeArray,
      treeArrayFinal,
      boardStatesComp,
      reloadGame,
      makeMove,
      undoMove,
      checkChoosenMove,
    };
  },
});
</script>

<style lang="scss" scoped>
.main-box {
  margin: 10px 5px;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  min-height: 90vh;
  max-height: 90vh;

  .container__top {
    color: white;
  }

  .container {
    display: flex;
    margin-top: 10px;
    margin-left: 10px;
    justify-content: flex-start;
    background-color: whitesmoke;
    box-shadow: 1px 1px 20px rgb(211, 211, 211);

    .container__container {
      border-radius: 12px;
      padding: 50px;
      .text-message {
        margin-bottom: 50px;
      }

      .box {
        height: 150px;
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
    display: flex;
    justify-content: space-evenly;
    align-items: center;

    margin: 5px;
    min-width: 70px;
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

  .tree {
    min-height: inherit;
  }

  .possibleMoves__container {
    display: flex;
    flex-direction: row;
    border-radius: 12px;
    padding: 50px;
    margin-top: 10px;
    margin-bottom: 10px;
    min-height: inherit;
    min-width: 50%;
    justify-content: space-between;
    //scrollbar machen

    .trueStyle {
      background-color: goldenrod;
    }

    .possibleMoves {
      display: flex;
      flex-direction: column;
      justify-content: space-evenly;
      flex-wrap: wrap;
    }

    .possibleMovesTree {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      flex-wrap: wrap;
    }
  }
}

disabled {
  pointer-events: none;
}
</style>
