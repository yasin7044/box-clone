<template>
  <div id="app">
    <div class="BoxContainer">
      <Box
        v-for="(eachBox, index) in box"
        :key="index"
        :index="index"
        :eachBox="eachBox"
        @changeCurrentBoxColour="changeCurrentBoxColour"
      />
    </div>
  </div>
</template>

<script>
import Box from "./components/Box.vue";

export default {
  name: "App",
  components: {
    Box,
  },
  data() {
    return {
      box: [],
    };
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
    this.generateBox();
  },
  methods: {
    generateBox() {
      for (let i = 0; i < 50; i++) {
        this.box.push(this.getRandomColor());
      }
    },
    handleScroll() {
      if (window.innerHeight + window.scrollY >= document.body.offsetHeight) {
        this.generateBox();
      }
    },
    getRandomColor() {
      const color = Math.floor(Math.random() * 16777215).toString(16);
      return "#" + color;
    },
    changeCurrentBoxColour(index, $event) {
      console.log($event);
      this.$set(this.box, index, this.getRandomColor());
    },
  },
};
</script>
<style scoped>
.BoxContainer {
  display: flex;
  flex-wrap: wrap;
  justify-content: left;
  align-items: stretch;
}
</style>
