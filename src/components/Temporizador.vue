<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempo="tempo" />
    <button class="button" @click="iniciar" :disabled="tempo != 0">
      <span class="icon">
        <i class="fas fa-play"></i>
      </span>
      <span>play</span>
    </button>
    <button class="button" @click="finalizar" :disabled="tempo == 0">
      <span class="icon">
        <i class="fas fa-stop"></i>
      </span>
      <span>stop</span>
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cronometro from "./Cronometro.vue";

export default defineComponent({
  name: "Temporizador",
  emits: ["aoTerminar"],
  components: {
    Cronometro,
  },
  data() {
    return {
      tempo: 0,
      cronometro: 0,
    };
  },
  methods: {
    iniciar() {
      this.cronometro = setInterval(() => {
        this.tempo++;
      }, 1000);
    },
    finalizar() {
      clearInterval(this.cronometro);
      this.$emit("aoTerminar", this.tempo);
      this.tempo = 0;
    },
  },
});
</script>

<style></style>
