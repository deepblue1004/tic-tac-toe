<template>
  <div>
    <game-board :size="this.$route.params.size"></game-board>
  </div>
</template>

<script>
import GameBoard from "../components/GameBoard.vue";
export default {
  components: { GameBoard },
  name: "IndexPage",
};
</script>
