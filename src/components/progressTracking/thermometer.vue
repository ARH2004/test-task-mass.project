<template>
  <div class="thermometer">
    <div class="container">
      <div class="thermometer__wrapper">
        <div
          class="thermometer__scale"
          :style="{
            'background-image': `linear-gradient(to right, red ${percent}%, rgba(239, 239, 239, 0.6) ${percent}%)`,
          }"
        >
          <div
            class="thermometer__item"
            v-for="(item, index) in stages"
            :key="item.id"
          >
            <div class="thermometer__image">
              <img :src="getImage(item)" :alt="getAltText(item)" />
            </div>
            <!-- Проверяем, не является ли текущий элемент последним элементом массива `stages` -->
            <hr class="thermometer__line" v-if="index < stages.length - 1" />
            <div class="thermometer__number">
              {{ item.thresholdPoints }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import cupImg from "@/assets/images/icons/cup.svg";
import starImg from "@/assets/images/icons/star.svg";
import starBlueImg from "@/assets/images/icons/starBlue.svg";

export default {
  name: "ProgressBar",
  props: {
    stages: {
      type: Array,
    },
  },
  data() {
    return {
      percent: 15,
    };
  },
  methods: {
    contBestResult() {
      let bestResults = this.stages.flatMap((stage) =>
        stage.games.map((game) => game.bestResult)
      );
      let maxBestResult = bestResults.reduce((acc, curr) => acc + curr, 0);
      return maxBestResult;
    },
  },
  methods: {
    getStarImage(item) {
      let totalBestResult = this.stages.reduce((acc, stage) => {
        return (
          acc +
          stage.games.reduce((acc, game) => {
            return acc + game.bestResult;
          }, 0)
        );
      }, 0);
      if (totalBestResult >= item.thresholdPoints) {
        return starBlueImg;
      }
      return starImg;
    },
    getImage(item) {
      if (item.id === this.stages.length) {
        return cupImg;
      }
      return this.getStarImage(item);
    },
    getAltText(item) {
      if (item.id === this.stages.length) {
        return "icon-cup";
      }
      return "icon-star";
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
}
.thermometer__scale-blue {
  background-color: blue;
  position: relative;
  width: 900px;
  border-radius: 30px;
  display: flex;
}
.thermometer__scale {
  position: relative;
  width: 900px;
  border-radius: 30px;
  display: flex;
}
.thermometer {
  &__item {
    position: relative;
    margin-left: 15%;
  }
  &__image {
    position: absolute;
    bottom: 45px;
    left: -10px;
  }
  &__line {
    position: relative;
    top: 0px;
    left: 0px;
    width: 1px;
    height: 40px;
    border: 0.3px solid rgba(70, 163, 88, 0.5);
    opacity: 0.2;
  }
  &__number {
    position: absolute;
    top: 45px;
    left: -5px;
    font-weight: 400;
    font-size: 14px;
    line-height: 17px;
    text-align: center;
    letter-spacing: -0.01em;
    color: #000000;
    opacity: 0.5;
  }
}
</style>
