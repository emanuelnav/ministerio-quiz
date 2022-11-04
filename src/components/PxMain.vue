<template>
  <section class="lg:relative w-screen h-screen flex items-center">
    <img
      class="lg:absolute left-0 lg:top-0 lg:h-screen object-cover z-1 w-screen"
      src="../assets/img/portada.jpg"
      autoplay
      muted
      loop
    />
    <div class="absolute z-2 position animate__animated animate__fadeInLeft">
      <button
        class="
          px-10
          py-4
          bg-blue-light
          text-blue-DEFAULT text-lg
          hover:bg-gray-200
          font-bold
          tracking-wide
          rounded-full
        "
        @click="startQuiz"
      >
        COMENZAR
      </button>
    </div>
  </section>
</template>

<script>
export default {
  methods: {
    startQuiz() {
      this.$emit("change-state");
    },
  },
};
</script>

<style scoped>
.position {
  bottom: 30%;
  left: 60%;
}
@media only screen and (max-width: 768px) {
  .position {
    top: 20%;
    left: 40%;
  }
}
@media only screen and (max-width: 450px) {
  .position {
    top: 20%;
    left: 25%;
  }
}
</style>
