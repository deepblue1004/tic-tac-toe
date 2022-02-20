<template>
  <div>
    <div class="landing-title">YL's Tic Tac Toe</div>
    <div id="landing-body">
      <div>
        <div id="game-mode-title" class="landing-body-title">
          <font-awesome-icon icon="fa-solid fa-gamepad" /> Game Mode
        </div>
        <div id="game-mode-value" class="landing-body-value">
          <input
            type="radio"
            id="mode-player"
            name="game-mode"
            :value="0"
            v-model="botLevel"
          />
          <label for="mode-player"
            ><font-awesome-icon icon="fa-solid fa-child"
          /></label>

          <template v-for="i in 3">
            <input
              :key="i"
              type="radio"
              :id="'mode-bot-' + i"
              name="game-mode"
              :value="i"
              v-model="botLevel"
            />
            <label :key="i" :for="'mode-bot-' + i">
              <font-awesome-icon icon="fa-solid fa-robot" />
              {{ "•".repeat(i) }}
            </label>
          </template>
        </div>
      </div>

      <div>
        <div id="board-size-title" class="landing-body-title">
          <font-awesome-icon icon="fa-solid fa-chess-board" /> Board Size
        </div>
        <div id="board-size-value" class="landing-body-value">
          <template v-for="i in 3">
            <input
              :key="i"
              type="radio"
              :id="'size-' + i + 2"
              name="board-size"
              :value="i + 2"
              v-model="boardSize"
            />
            <label
              :key="i"
              :for="'size-' + i + 2"
              v-text="i + 2 + 'x' + (i + 2)"
            ></label>
          </template>
        </div>
      </div>

      <div>
        <div class="landing-body-title player-name-title">Player One</div>
        <div class="player-name-value">
          <input v-model="players.player1" />
        </div>
      </div>
      <div v-if="botLevel == 0">
        <div class="landing-body-title player-name-title">Player Two</div>
        <div class="player-name-value">
          <input v-model="players.player2" />
        </div>
      </div>
      <div v-else></div>

      <nuxt-link
        :to="{
          name: 'TicTacToe',
          params: { bot: botLevel, size: boardSize },
        }"
      >
        <button>Start Game</button>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      botLevel: 0,
      boardSize: 3,
      players: {
        player1: "YenLong",
        player2: "Bot",
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.landing-title {
  padding: 20px 0;
  text-align: center;
  font-size: xxx-large;
  color: $primary-darker;
  background-color: $secondary;
  font-family: system-ui;
  font-weight: bolder;
}

#landing-body {
  display: grid;
  grid-template-columns: 250px 250px;
  row-gap: 10px;
  align-content: start;
  justify-items: center;
  justify-content: center;
  padding: 20px;
  position: absolute;
  top:
  box-sizing: border-box;
  border: 10px solid $primary-darkest;
  background-color: $primary-dark;


  .landing-body-title {
    font-size: xx-large;
    color: $primary-darkest;
    font-family: monospace;
    font-weight: bolder;
  }

  .landing-body-value {
    text-align: center;
    justify-content: space-around;
    display: grid;
    grid-template-columns: 80px 80px;
    grid-template-rows: 80px 80px;
    grid-column-gap: 10px;
    grid-row-gap: 10px;

    input[type="radio"] {
      opacity: 0;
      position: fixed;
      width: 0;
    }

    label {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background-color: white;
      padding: 10px;
      font-family: sans-serif, Arial;
      font-size: x-large;
      line-height: 20px;
      border: 2px solid $secondary-lightest;
      border-radius: 4px;
      color: $secondary;

      svg {
        font-size: xx-large;
      }
    }

    input[type="radio"]:checked + label {
      background-color: $tertiary-lighter;
      border-color: $tertiary;
    }
  }
}
</style>
