<template>
  <div>
    <game-board :size="this.$route.params.size"></game-board>
    <span> </span>
  </div>
</template>

<script>
import GameBoard from "../components/GameBoard.vue";
export default {
  components: { GameBoard },
  name: "IndexPage",
};
</script>
