<template>
  <div>
    GameBoard
    <input v-model.number="size" type="number" :min="0" />
    <div v-for="(i, row) in size" :key="row" class="row">
      <div
        v-for="(j, col) in size"
        :key="col"
        class="cell"
        @click="cellClick(row, col)"
      >
        {{ showIcon(boardArray[row * size + col]) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    size: {
      type: Number,
      default: 0,
    },

  },
  data() {
    return {
      // size: this.paramSize,
      boardArray: [],
      currentPlayer: -1, // -1 or 1
      playerSymbols: ["X", "O"],
      turn: 1,
    };
  },
  watch: {
    size: function (val) {
      let boardSize = val ** 2;
      this.boardArray = new Array(boardSize);
    },
  },
  filters: {},
  methods: {
    showIcon: function (val) {
      return this.playerSymbols[val == -1 ? 0 : val];
    },
    cellClick: function (row, col) {
      let index = row * this.size + col;
      if (this.boardArray[index] == undefined) {
        // https://sodocumentation.net/vue-js/topic/10679/the-array-change-detection-caveats
        this.$set(this.boardArray, index, this.currentPlayer);
        // Switch user
        this.currentPlayer = -this.currentPlayer;
        this.turn++;
        let gameEndStatus = this.checkEndGame();
        switch (gameEndStatus) {
          case 0:
            console.log("Draw");
            break;
          case -1:
            console.log(`Player ${this.playerSymbols[0]} won`);
            break;
          case 1:
            console.log(`Player ${this.playerSymbols[1]} won`);
            break;
          default:
            break;
        }
      }
    },
    // -1: player -1 won
    // 0: game draw
    // 1: player 1 won
    checkEndGame: function () {
      for (let i = 0; i < this.size; i++) {
        let rowStartIdx = i * this.size;
        let rowEndIdx = i * this.size + this.size;

        // Row Total
        let rowTotal = this.boardArray
          .slice(rowStartIdx, rowEndIdx)
          .reduce(sumElement, 0);
        if (Math.abs(rowTotal) == this.size) {
          return rowTotal / this.size;
        }

        // Col Total
        let colTotal = this.boardArray
          .filter((val, idx) => idx % this.size == i)
          .reduce(sumElement, 0);
        if (Math.abs(colTotal) == this.size) {
          return colTotal / this.size;
        }
      }

      // Diagonal
      let DiagonalTotal = this.boardArray
        .filter((val, idx) => idx % (this.size + 1) == 0)
        .reduce(sumElement, 0);
      if (Math.abs(DiagonalTotal) == this.size) {
        return DiagonalTotal / this.size;
      }

      // Inverse Diagonal
      let InverseDiagonalTotal = this.boardArray
        .filter((val, idx) => idx % (this.size - 1) == 0)
        .slice(1, -1)
        .reduce(sumElement, 0);
      if (Math.abs(InverseDiagonalTotal) == this.size) {
        return InverseDiagonalTotal / this.size;
      }

      // Check Draw
      if (!this.boardArray.includes(undefined)) {
        return 0;
      }

      function sumElement(a, b) {
        return a + b;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
$base-color: #5381c6;
.row {
  display: flex;
}
.cell {
  border: 1px $base-color solid;
  padding: 10px;
  width: 15px;
  height: 15px;
}
</style>
