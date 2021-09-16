<template>
  <main class="flex flex-grow h-screen bg-blue-light">
    <!-- <px-header></px-header> -->
    <px-animations-left></px-animations-left>
    <px-questions></px-questions>
    <px-animations-right></px-animations-right>
    
    <!-- <px-footer></px-footer> -->
  </main>
</template>

<script>
import PxQuestions from "@/components/PxQuestions";
import PxAnimationsLeft from "@/components/PxAnimationsLeft";
import PxAnimationsRight from "@/components/PxAnimationsRight";
// import PxHeader from "@/components/PxHeader";
// import PxFooter from "@/components/PxFooter";

export default {
  name: "App",
  components: {
    PxQuestions,
    PxAnimationsLeft,
    PxAnimationsRight,
    // PxHeader,
    // PxFooter,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
main {
  font-family: "Montserrat", sans-serif;
}
</style>
