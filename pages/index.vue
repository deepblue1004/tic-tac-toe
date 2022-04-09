<template>
  <div>
    <landing></landing>
  </div>
</template>

<script>
import GameBoard from "../components/GameBoard.vue";
import Landing from "../components/Landing.vue";
export default {
  components: { GameBoard, Landing },
  name: "IndexPage",
};
</script>

<style lang="scss">
body {
  margin: 0;
}
</style>
