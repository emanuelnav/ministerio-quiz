<template>
  <section class="flex flex-col flex-grow w-full h-full justify-center items-center">
    <span v-show="index < count">{{ index + 1 }} / {{ count }}</span>
    <div class="p-12 max-w-3xl mt-8 flex justify-center">
      <div v-if="index < count">
        <h3 class="text-2xl font-bold text-blue-dark text-center">
          {{ questions[index].question }}
        </h3>
        <label
          :for="key"
          class="
            block
            mt-4
            border-2 border-blue-DEFAULT
            rounded-full
            py-2
            px-6
            text-lg text-blue-DEFAULT
            font-bold
            text-center
          "
          v-for="(answer, key) in questions[index].answers"
          :key="answer"
          :class="{
            'hover:bg-gray-200 cursor-pointer': selectAnswer == '',
            'bg-red-500': selectAnswer == key,
            'bg-green-500':
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
              px-5
              py-2
              bg-blue-DEFAULT
              text-blue-light text-sm
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
              px-5
              py-2
              bg-blue-DEFAULT
              text-blue-light text-sm
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
      <div v-else>
        <h2 class="text-center">Resultados</h2>
        <span>{{ countAnswersCorrect }}</span>
        <div class="mt-6 flow-root">
          <button
            class="
              float-right
              px-5
              py-2
              bg-blue-DEFAULT
              text-blue-light text-sm
              font-bold
              tracking-wide
              rounded-full
            "
            @click="restartQuiz"
          >
            Reintentar
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "PxQuestions",
  data() {
    return {
      selectAnswer: "",
      index: 0,
      count: 5,
      countAnswersCorrect: 0,
      questions: [
        {
          question: "¿Cuántos kilómetros de rutas construiremos en el 2021?",
          answers: { a: "280 km", b: "360 km", c: "140 km" },
          correctAnswer: "b",
        },
        {
          question:
            "¿A cuántas localidades garantizará agua potable el Segundo Acueducto del Interior?",
          answers: { a: "21", b: "26", c: "29" },
          correctAnswer: "b",
        },
        {
          question:
            "¡Chaco reestructuró su deuda externa en dólares! ¿De cuánto será el ahorro que logrará la Provincia hasta el 2024?",
          answers: {
            a: "USD 212 millones",
            b: "USD 180 millones",
            c: "USD 140 millones",
          },
          correctAnswer: "a",
        },
        {
          question: "¿Cuántas cuadras pavimentaremos este año en Chaco?",
          answers: { a: "+500", b: "+1000", c: "+800" },
          correctAnswer: "b",
        },
        {
          question:
            "Chaco Reactiva es el plan de recuperación económica que pusimos en marcha. ¿Cuáles son sus principales objetivos?",
          answers: {
            a: "Fortalecimiento de la industria",
            b: "Generación de empleo",
            c: "Crecimiento de la infraestructura y el consumo",
            d: "Todas son correctas",
          },
          correctAnswer: "d",
        },
      ],
    };
  },

  methods: {
    answered(e) {
      this.selectAnswer = e.target.value;
      if (this.selectAnswer == this.questions[this.index].correctAnswer) {
        this.countAnswersCorrect++;
      }
    },
    nextQuestion() {
      this.selectAnswer = "";
      this.index++;
    },
    showResults() {
      this.index++;
    },
    restartQuiz() {
      this.index = 0;
      this.selectAnswer = "";
      this.countAnswersCorrect = 0;
    },
  },
};
</script>
