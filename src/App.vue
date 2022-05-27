<script lang="ts">
import GitHubCorners from "./components/GitHubCorners.vue";

export default {
  name: "App",
  components: {
    'github-corners': GitHubCorners,
  },
  data() {
    return {
      position: "right",
      isSwapColor: false,
      colors: ["#151513", "red", "green", "blue"],
      currentColorIndex: 0,
    };
  },
  computed: {
    currentBgColor(): string {
      if (!this.isSwapColor) {
        return this.colors[this.currentColorIndex];
      } else {
        return "white";
      }
    },
    currentColor(): string {
      if (!this.isSwapColor) {
        return "white";
      } else {
        return this.colors[this.currentColorIndex];
      }
    },
  },
  methods: {
    updatePageBg() {
      if (this.isSwapColor) {
        const currentBgColor = this.colors[this.currentColorIndex];

        document.body.style.setProperty("background-color", currentBgColor);
      } else {
        document.body.style.removeProperty("background-color");
      }
    },
    swapPosition() {
      this.position = this.position == "right" ? "left" : "right";
    },
    swapColor() {
      this.isSwapColor = !this.isSwapColor;
      this.updatePageBg();
    },
    changeBgColor() {
      if (this.currentColorIndex + 1 >= this.colors.length) {
        this.currentColorIndex = 0;
      } else {
        this.currentColorIndex++;
      }
      this.updatePageBg();
    },
  },
};
</script>

<template>
  <div id="home">
    <github-corners
      repo="gluons/vue-gh-corners"
      :bg-color="currentBgColor"
      :color="currentColor"
      :position="position"
    ></github-corners>
    <div id="custom">
      <button type="button" @click="swapPosition">Swap Position</button>
      <button type="button" @click="swapColor">Swap Color</button>
      <button type="button" @click="changeBgColor">Change Color</button>
    </div>
  </div>
</template>

<style>

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
