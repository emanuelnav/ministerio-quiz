<template>
  <section
    class="flex flex-col flex-grow w-full h-full justify-center items-center"
  >
    <span class="font-bold text-lg" v-show="index < count">
      {{ index + 1 }} / {{ count }}
    </span>
    <div class="p-12 max-w-3xl mt-8 flex justify-center max-h-screen">
      <div v-if="index < count">
        <div class="flex justify-center items-center">
          <img
            class="self-start arrow-img hidden lg:block"
            src="../assets/img/arrow.png"
            alt="Flecha"
          />
          <h3 class="text-xl lg:text-2xl font-bold text-blue-dark text-center">
            {{ questions[index].question }}
          </h3>
        </div>
        <label
          :for="key"
          class="
            block
            mt-4
            border-2 border-blue-DEFAULT
            rounded-full
            py-1
            lg:py-2
            px-2
            lg:px-6
            text-lg
            lg:text-2xl
            font-bold
            text-center
          "
          v-for="(answer, key) in questions[index].answers"
          :key="answer"
          :class="{
            'hover:bg-gray-200 cursor-pointer': selectAnswer == '',
            'bg-red-500 text-white': selectAnswer == key,
            'bg-green-500 text-white':
              key == questions[index].correctAnswer && selectAnswer != '',
          }"
        >
          <input
            type="radio"
            :id="key"
            class="hidden"
            :value="key"
            @change="answered($event)"
            :disabled="selectAnswer != ''"
          />
          {{ answer }}
        </label>
        <div class="mt-6 flow-root">
          <button
            class="
              float-right
              px-6
              py-4
              bg-blue-DEFAULT
              text-blue-light text-sm
              hover:bg-blue-dark
              font-bold
              tracking-wide
              rounded-full
            "
            v-show="selectAnswer != '' && index < count - 1"
            @click="nextQuestion"
          >
            Siguiente
          </button>
        </div>
        <div class="mt-6 flow-root">
          <button
            class="
              float-right
              px-6
              py-4
              bg-blue-DEFAULT
              text-blue-light text-sm
              hover:bg-blue-dark
              font-bold
              tracking-wide
              rounded-full
            "
            v-show="selectAnswer != '' && index == count - 1"
            @click="showResults"
          >
            Ver Resultados
          </button>
        </div>
      </div>
      <div v-else class="flex flex-col justify-center items-center">
        <h2 class="text-center text-4xl font-black text-blue-dark mb-2">
          {{ results[countAnswersCorrect].text }}
        </h2>
        <img
          class="result-img animate__animated animate__zoomIn"
          :src="results[countAnswersCorrect].image"
          :alt="results[countAnswersCorrect].name"
        />
        <span
          class="
            rounded-full
            h-20
            w-20
            flex
            items-center
            justify-center
            bg-blue-dark
            text-blue-DEFAULT text-4xl
            font-bold
            mt-4
          "
        >
          {{ countAnswersCorrect }}
        </span>
        <span class="text-blue-DEFAULT text-4xl font-bold">Aciertos</span>
        <div class="mt-6 flow-root">
          <button
            class="
              float-right
              px-6
              py-4
              bg-blue-DEFAULT
              text-blue-light text-sm
              hover:bg-blue-dark
              font-bold
              tracking-wide
              rounded-full
            "
            @click="restartQuiz"
          >
            Volver al Inicio
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
let noHits = new Audio(require("../assets/audio/nohits.mp3"));
let oneHit = new Audio(require("../assets/audio/onehit.mp3"));
let threeHits = new Audio(require("../assets/audio/threehits.mp3"));
let allHits = new Audio(require("../assets/audio/allhits.mp3"));

export default {
  name: "PxQuestions",
  data() {
    return {
      selectAnswer: "",
      index: 0,
      count: 5,
      countAnswersCorrect: 0,
      failSound: new Audio(require("../assets/audio/fail.mp3")),
      successSound: new Audio(require("../assets/audio/success.mp3")),
      soundEffects: [noHits, oneHit, oneHit, threeHits, threeHits, allHits],
      results: [
        {
          name: "0 aciertos",
          image: "https://i.imgur.com/6rYD9i4.jpg",
          text: "AUCH!",
        },
        {
          name: "1 acierto",
          image: "https://i.imgur.com/Ofihx3U.png",
          text: "Probemos suerte la proxima!",
        },
        {
          name: "2 aciertos",
          image: "https://i.imgur.com/Ofihx3U.png",
          text: "Probemos suerte la proxima!",
        },
        {
          name: "3 aciertos",
          image: "https://i.imgur.com/3MTiIWF.gif",
          text: "WOW!",
        },
        {
          name: "4 aciertos",
          image: "https://i.imgur.com/3MTiIWF.gif",
          text: "WOW!",
        },
        {
          name: "5 aciertos",
          image: "https://i.imgur.com/iePOA2D.png",
          text: "Nivel Expert@!",
        },
      ],
      questions: [
        {
          question:
            "¿Desde enero del 2021 hasta la fecha, cuántas obras llevamos inauguradas en Sáenz Peña?",
          answers: { a: "12", b: "14", c: "17" },
          correctAnswer: "c",
        },
        {
          question:
            "Entre estas obras de infraestructura sanitaria local hay una que iniciará muy pronto. ¿Cuál es?",
          answers: {
            a: "Hospital Odontológico",
            b: "Hospital Materno Infantil",
            c: "Hospital 4 de Junio",
          },
          correctAnswer: "b",
        },
        {
          question:
            "Junto a IPDUV estamos construyendo 74 departamentos del PRO.CRE.AR. ¿Hasta cuándo está abierta la inscripción?",
          answers: {
            a: "Todavía no comenzó",
            b: "Ya terminó",
            c: "Hasta el 15/11",
          },
          correctAnswer: "c",
        },
        {
          question:
            "Hace poco inauguramos la Residencia Estudiantil de Sáenz Peña. ¿Cuántos chicos y chicas pueden vivir allí gratis y con todas las comodidades?",
          answers: { a: "50", b: "150", c: "200" },
          correctAnswer: "c",
        },
        {
          question:
            "¿Sabías que el Centro de Convenciones 'Ferichaco' fue íntegramente remodelado? ¿Qué uso se le dará a este espacio?",
          answers: {
            a: "De interés cívico",
            b: "Esparcimiento cultural",
            c: "¡Ambas!",
          },
          correctAnswer: "c",
        },
      ],
    };
  },

  methods: {
    answered(e) {
      this.selectAnswer = e.target.value;
      if (this.selectAnswer == this.questions[this.index].correctAnswer) {
        this.successSound.play();
        this.countAnswersCorrect++;
      } else {
        this.failSound.play();
      }
    },
    nextQuestion() {
      this.selectAnswer = "";
      this.index++;
    },
    showResults() {
      this.index++;
      this.soundEffects[this.countAnswersCorrect].play();
    },
    restartQuiz() {
      this.soundEffects[this.countAnswersCorrect].pause();
      this.soundEffects[this.countAnswersCorrect].currentTime = 0;
      this.index = 0;
      this.selectAnswer = "";
      this.countAnswersCorrect = 0;
      this.$emit("change-state");
    },
  },
};
</script>

<style scoped>
.arrow-img {
  width: 2rem;
}

.result-img {
  width: 400px;
  height: 400px;
}
label {
  color: #16b9ed;
}
</style>
