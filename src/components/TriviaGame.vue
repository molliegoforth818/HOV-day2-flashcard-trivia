<template>
  <h1>⚡️ Harry Potter Trivia ⚡️</h1>
  <div v-for="question in Qs" :key="Qs.id"></div>
</template>

<script>
import { triviaQs } from "../trivia";
import FlashCard from "./FlashCard";

export default {
  components: { FlashCard },
data() {
  return{
    Qs: [...triviaQs]
  }
}
}
</script>

<style>

</style>