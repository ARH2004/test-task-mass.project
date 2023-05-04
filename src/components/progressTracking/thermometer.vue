<template>
  <div class="thermometer">
    <div class="container">
      <div class="thermometer__wrapper">
        <div class="thermometer__scale">
					<div class="thermometer__item" v-for="item in stages" :key="item.id">
						<div class="thermometer__image">
							<img src="@/assets/images/icons/star.svg" alt="icon-star">
						</div>
						{{ item.id }}
          	<hr class="thermometer__line" />
					</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "progress",
	props: {
		stages: {
			type: Array,
		}
	}
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
    min-width: 0;
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
}
</style>

<!-- <template>
  <div>
    <h1>Прогресс игрока</h1>
    <div v-for="stage in stages" :key="stage.id">
      <h2>{{ stage.name }}</h2>
      <div v-for="game in stage.games" :key="game.name">
        <h3>{{ game.name }}</h3>
        <Thermometer
          :points="game.bestResult"
          :thresholdPoints="stage.thresholdPoints"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Thermometer from "@/components/vTermometr.vue";
export default {
  components: {
    Thermometer,
  },
  data() {
    return {
      stages: [
        {
          name: "Этап первый",
          id: 1,
          thresholdPoints: 25,
          games: [
            {
              name: "Игра 1.1",
              bestResult: 0,
              isPlayed: false,
            },
          ],
        },
        {
          name: "Этап второй",
          id: 2,
          thresholdPoints: 50,
          games: [
            {
              name: "Игра 2.1",
              bestResult: 0,
              isPlayed: false,
            },
          ],
        },
        {
          id: 3,
          name: "Этап третий",
          thresholdPoints: 100,
          games: [
            {
              name: "Игра 3.1",
              bestResult: 0,
              isPlayed: false,
            },
          ],
        },
        {
          id: 4,
          name: "Этап четвертый",
          thresholdPoints: 200,
          games: [
            {
              name: "Игра 4.1",
              bestResult: 0,
              isPlayed: false,
            },
          ],
        },
        {
          id: 5,
          name: "Этап пятый",
          thresholdPoints: 500,
          games: [
            {
              name: "Игра 5.1",
              bestResult: 0,
              isPlayed: false,
            },
          ],
        },
        {
          id: 6,
          name: "Этап шестой",
          thresholdPoints: 1000,
          games: [
            {
              name: "Игра 6.1",
              bestResult: 0,
              isPlayed: false,
            },
            {
              name: "Игра 6.2",
              bestResult: 0,
              isPlayed: false,
            },
          ],
        },
      ],
    };
  },
};
</script> -->
