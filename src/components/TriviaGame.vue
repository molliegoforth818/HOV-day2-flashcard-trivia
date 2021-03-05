<template>
  <div>
    <h1>⚡️ Harry Potter Trivia ⚡️</h1>
    <button @click="hideAll" class="hide-button"> Hide All </button>
    <div class="difficulty-levels">
      <difficulty-levels
      :difficulty="chooseDifficulty"
      @difficulty-change="handleDifficultyChange" />
    </div>
    <div class="flash-cards">
    <div v-for="card in cards" :key="card.id">
      <flash-card :card="card" @status-change="handleStatusChange" /> 
    </div>
    </div>
  </div>
</template>

<script>
import { triviaCards } from "../trivia";
import DifficultyLevels from "./DifficultyLevels"
import FlashCard from "./FlashCard";

export default {
  components: { FlashCard, DifficultyLevels },
  data() {
    return {
      cards: [...triviaCards],
      chosenDifficulty: "all"
    };
  },
  methods: {
    handleStatusChange(card) {
      card.answerShown = !card.answerShown;
    },
    handleDifficultyChange(difficulty) {
      this.chosenDifficulty = difficulty;
    },
    hideAll() {
      this.cards.forEach(cards => (cards.answerShown = false));
    }
  },
  computed: {
    flashCards() {
      if (this.chosenDifficulty === "all"){
        return this.cards;
      }
      return this.cards.filter(cards => cards.difficulty ===this.chosenDifficulty);
    }
  }
};
</script>

<style scoped>
.flash-cards {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}
.hide-button{
  background: transparent;
  border: none;
  cursor: pointer;
  margin-bottom: 10px;
  font-size: 20px;
  color: goldenrod;
}

</style>