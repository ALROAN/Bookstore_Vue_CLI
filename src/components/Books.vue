
<template>
  <div class="flipCard">
    <div class="main flipCardInner" id="imgContainer">
      <div class="front">
        <transition
          name="animation"
          enter-active-class="animated zoomIn"
          leave-active-class="animated zoomOut"
          appear
        >
          <img v-bind:src="bookEmpty.portada" :alt="bookEmpty.titulo" />
        </transition>
      </div>
      <div class="back">
        <h3>{{ bookEmpty.titulo }}</h3>
        <p>{{ bookEmpty.descripcion }}</p>
        <a :href="bookEmpty.detalle" data-fancybox="images" :data-caption="bookEmpty.titulo">
          <button>+Info</button>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["bookEmpty"],

  created() {},

  data() {
    return {};
  },
  methods: {}
};
</script>

<style scoped>
.flipCard {
  height: 350px;
  width: 250px;
}

.flipCard .flipCardInner:hover {
  transform: rotateY(180deg);
}

.flipCardInner {
  position: relative;
  width: 250px;
  height: 350px;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.back,
.front {
  position: absolute;
  height: 350px;
  width: 250px;
  backface-visibility: hidden;
}

.front {
  background-color: white;
  color: black;
}

.back {
  background-color: gray;
  color: white;
  transform: rotateY(180deg);
}

img {
  width: 100%;
  height: 100%;
}

button {
  width: 75px;
  height: 40px;
}
</style>

