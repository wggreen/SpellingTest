<template>
  <div>
    <p>Results: {{ correctCount }} / {{ questions.length }}</p>
    <p v-if="perfectScore">PERFECT SCORE</p>
  </div>
</template>

<script>
export default {
  props: ["questions"],
  computed: {
    correctCount() {
      return this.questions.filter((q) => {
        return q.word.toLowerCase() === q.userInput.toLowerCase;
      }).length;
    },
    perfectScore() {
      return this.correctCount === this.questions.length;
    },
  },
};
</script>

<style>
</style>