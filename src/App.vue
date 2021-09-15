<template>
  <main class="h-screen">
    <px-header></px-header>
    <px-questions></px-questions>
  </main>
</template>

<script>
import PxHeader from "@/components/PxHeader";
import PxQuestions from "@/components/PxQuestions";

export default {
  name: "App",
  components: {
    PxHeader,
    PxQuestions,
  },
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
