<template>
  <main class="bg-blue-light">
    <div v-if="mainScreen" class="bg-blue-DEFAULT">
      <px-main @change-state="updateState"></px-main>
    </div>
    <div
      v-else
      class="
        flex flex-grow
        h-screen
        bg-blue-light
        animate__animated animate__fadeIn
      "
    >
      <px-animations-left></px-animations-left>
      <px-questions @change-state="updateState"></px-questions>
      <px-animations-right></px-animations-right>
    </div>
  </main>
</template>

<script>
import PxMain from "@/components/PxMain";
import PxQuestions from "@/components/PxQuestions";
import PxAnimationsLeft from "@/components/PxAnimationsLeft";
import PxAnimationsRight from "@/components/PxAnimationsRight";

export default {
  name: "App",
  data() {
    return {
      mainScreen: true,
    };
  },
  components: {
    PxMain,
    PxQuestions,
    PxAnimationsLeft,
    PxAnimationsRight,
  },
  methods: {
    updateState() {
      this.mainScreen = !this.mainScreen;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
main {
  font-family: "Montserrat", sans-serif;
}
</style>
