<template>
  <div>
    <h1>⚡️ Harry Potter Trivia ⚡️</h1>
    <button @click="hideAll" class="hide-button"> Hide All </button>
    <div class="difficulty-levels">
      <difficulty-levels
      :difficulty="selectedDifficulty"
      @difficulty-change="handleDifficultyChange" />
    </div>
    <div class="questions">
    <div v-for="card in flashCards" :key="card.id">
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
      selectedDifficulty: "all"
    };
  },
  methods: {
    handleStatusChange(card) {
      card.answerShown = !card.answerShown;
    },
    handleDifficultyChange(difficulty) {
      this.selectedDifficulty = difficulty;
    },
    hideAll() {
      this.cards.forEach(cards => (cards.answerShown = false));
    }
  },
  computed: {
    flashCards() {
      if (this.selectedDifficulty === "all"){
        return this.cards;
      }
      return this.cards.filter(cards => cards.difficulty ===this.selectedDifficulty);
    }
  }
};
</script>

<style scoped>
.questions {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}
.hide-button {
  background: transparent;
  border: none;
  cursor: pointer;
  margin-bottom: 10px;
  font-size: 20px;
  color: goldenrod;
}
</style>