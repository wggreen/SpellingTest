<template>
  <button @click="sayWord" class="clickable">Say Word</button>
</template>

<script>
export default {
  props: ["word"],
  data() {
    return {};
  },
  methods: {
    sayWord() {
      const utterance = new SpeechSynthesisUtterance(this.word);
      speechSynthesis.speak(utterance);
    },
  },
};
</script>

<style>
.clickable {
  margin-bottom: 20px;
}
</style>