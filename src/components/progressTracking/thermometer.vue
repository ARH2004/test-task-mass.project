<template>
  <div class="thermometer">
    <div class="container">
      <div class="thermometer__wrapper">
        <button @click="contBestResult">click</button>
        <div class="thermometer__scale">
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

export default {
  name: "ProgressBar",
  props: {
    stages: {
      type: Array,
    },
  },
  methods: {
    getImage(item) {
      if (item.id === this.stages.length) {
        return cupImg;
      }
      return starImg;
    },
    getAltText(item) {
      if (item.id === this.stages.length) {
        return "icon-cup";
      }
      return "icon-star";
    },
    contBestResult() {
      let bestResults = this.stages.flatMap((stage) =>
        stage.games.map((game) => game.bestResult)
      );
      let maxBestResult = bestResults.reduce((acc, curr) => acc + curr, 0);
      console.log(maxBestResult);
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
}
.thermometer {
  &__scale {
    position: relative;
    width: 900px;
    background: rgba(239, 239, 239, 0.6);
    border-radius: 30px;
    display: flex;
  }
  &__item {
    position: relative;
    margin-left: 145px;
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