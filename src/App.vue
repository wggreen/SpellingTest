<template>
  <div id="app">
    <h1>Spelling Test</h1>
    <div v-if="!testFinished">
      <p>Word {{ activeIndex + 1 }} of {{ questions.length }}</p>
      <speech :word="questions[activeIndex].word" />
      <form @submit.prevent="handleSubmit">
        <input spellcheck="false" v-model="userInput" />
        <button type="submit">Submit</button>
      </form>
    </div>
    <div v-else>
      <score :questions="data" />
    </div>
  </div>
</template>

<script>
import data from "./data";
import Speech from "./components/Speech";
import Score from "./components/Score";

export default {
  components: { Speech, Score },
  data() {
    return {
      questions: data,
      activeIndex: 0,
      userInput: "",
    };
  },
  methods: {
    handleSubmit() {
      this.questions[this.activeIndex].userInput = this.userInput;
      this.activeIndex++;
      this.userInput = "";
    },
  },
  computed: {
    testFinished() {
      if (
        this.questions.filter((q) => {
          return q.word === q.userInput;
        }).length === this.questions.length
      ) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
