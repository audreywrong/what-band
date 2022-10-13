<template>
  <form>
    <div v-if="questionIndex < questions.length">
      <label>{{ question.question }}</label>
      <div v-for="c of question.choices" :key="c">
        <input type="radio" name="choice" v-model="answer" :value="c" />
        {{ c }}
      </div>
    </div>
    <div v-else>
      <button type="button" @click="restart">
        I don't like that band. Start over.
      </button>
    </div>
    <button type="button" @click="submit">check</button>
  </form>
  <p>score: {{ score }}</p>
</template>
<script>
const questions = [
  {
    question: "Screamo or scream-no?",
    choices: ["SCREAM TO ME", "Nah"],
    rightAnswer: "SCREAM TO ME",
  },
  {
    question: "Are you feeling sad or happy?",
    choices: ["I love people today.", "*sigh*"],
    rightAnswer: "*sigh*",
  },
];
export default {
  name: "App",
  data() {
    return {
      questions,
      score: 0,
      questionIndex: 0,
      question: questions[0],
      answer: "",
    };
  },
  methods: {
    submit() {
      const { answer, question, questions, questionIndex } = this;
      if (answer === question.rightAnswer) {
        this.score++;
      }
      if (questionIndex < questions.length) {
        this.questionIndex++;
        this.question = { ...questions[this.questionIndex] };
      }
    },
    restart() {
      this.question = questions[0];
      this.answer = "";
      this.questionIndex = 0;
      this.score = 0;
    },
  },
};
</script>
