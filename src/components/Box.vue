<template>
  <div class="BoxContainer">
    <div
      class="Box"
      :style="{ 'background-color': eachBox }"
      v-for="(eachBox, index) in box"
      :key="index"
      @click="changeCurrentBox(index)"
    ></div>
  </div>
</template>

<script>
export default {
  name: "Box",
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
      for (let i = 0; i < 30; i++) {
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
    changeCurrentBox(index) {
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
  align-items: center;
  flex-grow: 1;
  margin: 30px;
}
.Box {
  width: 13em;
  height: 13em;
  border: 2px solid black;
}
</style>
