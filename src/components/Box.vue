<template>
  <div class="BoxContainer">
    <!-- {{ eachBox }} -->
    <div
      class="Box"
      :style="{ 'background-color': eachBox }"
      @click="$emit('changeCurrentBoxColour', index)"
    ></div>
  </div>
</template>
<script>
export default {
  props: {
    eachBox: {},
    index: {},
  },
};
</script>
<style scoped>
.Box {
  width: 164px;
  height: 164px;
  border: 2px solid black;
}
</style>
