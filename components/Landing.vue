<template>
  <div>
    <div class="landing-title">YL's Tic Tac Toe</div>
    <div id="landing-body">
      <div id="game-mode-title" class="landing-body-title">Game Mode</div>
      <div id="game-mode-value" class="landing-body-value">
        <input
          type="radio"
          id="mode-player"
          name="game-mode"
          :value="0"
          v-model="botLevel"
        />
        <label for="mode-player">Player</label>

        <span v-for="i in 3" :key="i">
          <input
            type="radio"
            :id="'mode-bot-' + i"
            name="game-mode"
            :value="i"
            v-model="botLevel"
          />
          <label :for="'mode-bot-' + i">Bot Lv {{ i }}</label>
        </span>
      </div>

      <div id="board-size-title" class="landing-body-title">Board Size</div>
      <div id="board-size-value" class="landing-body-value">
        <span v-for="i in 3" :key="i">
          <input
            type="radio"
            :id="'size-' + i + 2"
            name="board-size"
            :value="i + 2"
            v-model="boardSize"
          />
          <label :for="'size-' + i+2" v-text="i + 2 + 'x' + (i + 2)"></label>
        </span>
      </div>

      <div v-if="botLevel != 0">
        <div class="landing-body-title player-name-title">Player's Name</div>
        <div class="player-name-value"><input v-model="players.player1" /></div>
      </div>
      <div v-else>
        <div class="landing-body-title player-name-title">Player One</div>
        <div class="player-name-value"><input v-model="players.player1" /></div>
        <div class="landing-body-title player-name-title">Player Two</div>
        <div class="player-name-value"><input v-model="players.player2" /></div>
      </div>

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
  background-color: $secondary-lighter;
  font-family: system-ui;
  font-weight: bolder;
}

#landing-body {
  display: grid;
  row-gap: 10px;
  align-content: start;
  justify-items: center;
  justify-content: center;
  position: fixed;
  height: 100%;
  width: 100%;
  padding-top: 15vh;
  background-color: $primary-lighter;

  .landing-body-title {
    font-size: xx-large;
    color: $primary-darker;
    font-family: monospace;
    font-weight: bolder;
  }

  .landing-body-value {
    input[type="radio"] {
      opacity: 0;
      position: fixed;
      width: 0;
    }

    label {
      display: inline-block;
      background-color: #ddd;
      padding: 10px 20px;
      font-family: sans-serif, Arial;
      border: 2px solid #444;
      border-radius: 4px;
    }

    input[type="radio"]:checked + label {
      background-color: #bfb;
      border-color: #4c4;
    }
  }
}
</style>
