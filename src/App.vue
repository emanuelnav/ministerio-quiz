<template>
  <main class="flex flex-grow h-screen bg-blue-light">
    <px-animations-left></px-animations-left>
    <px-questions></px-questions>
    <px-animations-right></px-animations-right>
  </main>
</template>

<script>
import PxQuestions from "@/components/PxQuestions";
import PxAnimationsLeft from "@/components/PxAnimationsLeft";
import PxAnimationsRight from "@/components/PxAnimationsRight";

export default {
  name: "App",
  components: {
    PxQuestions,
    PxAnimationsLeft,
    PxAnimationsRight,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
main {
  font-family: "Montserrat", sans-serif;
}
</style>
