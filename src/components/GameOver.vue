<template>
  <div class="text-center game-over">
    <h2 class="mb-2">
      {{ $t(`Você errou!`) }}
    </h2>

    <img :src="errorImage" class="img-fluid" />

    <h5 class="mb-4 mt-2">
      <template v-if="reason === 'time'">
        {{ $t('fim de jogo') }}
      </template>
      <template v-else>
        {{ $t('resposta correta') }}: {{ currentQuestion.rightAnswer }}
      </template>
    </h5>
    <p v-if="reason === 'answer'">
      {{ currentQuestion.explanation }}
    </p>
    <button @click="$emit('restartGame')" class="btn btn-primary">
      {{ $t('common-start-again') }}
    </button>
  </div>
</template>

<script>
import gameImages from "../dados/images.json";

export default {
  name: 'GameOver',

  props: {
    reason: {
      type: String,
      required: true,
    },
    currentQuestion: {
      type: Object,
      required: true,
    },
  },

  computed: {
    errorImage() {
      const imagesArray = gameImages.wrong;
      const image = imagesArray[Math.floor(Math.random() * imagesArray.length)];
      return require(`../assets/images/wrong/${image}`);
    },
  },
};
</script>

<style scoped>
.game-over {
  position: absolute;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  padding: 20px;
  border-radius: 5px;
  background-color: #343a40;
  color: white;
  z-index: 20;
  max-width: 600px !important;
  box-shadow: 2px 3px 12px black;
}
</style>
