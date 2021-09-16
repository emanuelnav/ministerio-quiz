<template>
  <section class="relative w-screen h-screen">
    <!-- <header class="sticky top-0 h-1/5">Button Comenzar</header> -->
    <video
      class="absolute left-0 top-0 w-screen h-screen object-cover z-1"
      src="../assets/img/placainicio.mp4"
      autoplay
      muted
      loop
    ></video>
    <div class="absolute z-2 position">
      <button
        class="
          px-10
          py-4
          bg-blue-light
          text-blue-DEFAULT text-lg
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
  left: 80%;
}
</style>
