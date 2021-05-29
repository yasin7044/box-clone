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
      windowWidth: window.innerWidth,
      gettingNoOfDiv: 0,
    };
  },
  watch: {
    windowWidth: {
      immediate: true,
      handler() {
        this.gettingNoOfDiv = Math.floor(this.windowWidth / 168);
      },
    },
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
    window.addEventListener("resize", this.onResize);

    this.generateBox();
  },

  methods: {
    onResize() {
      this.windowWidth = window.innerWidth;
    },
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
    changeCurrentBoxColour(index) {
      this.$set(this.box, index, this.getRandomColor());
      this.changingNearestBox(index);
    },
    changingNearestBox(index) {
      if (this.gettingNoOfDiv <= 1) {
        console.log("No Neighbour Found");
      } else if (this.gettingNoOfDiv - (index % this.gettingNoOfDiv) > 1) {
        console.log("Right");
        this.$set(this.box, index + 1, this.getRandomColor());
      } else {
        console.log("Left");
        this.$set(this.box, index - 1, this.getRandomColor());
      }
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
