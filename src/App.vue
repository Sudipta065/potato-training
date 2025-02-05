<template>
  <div>
    <button class="button-sort" @click="showModal = true">Start Sorting</button>
    <SortingModal
      v-if="showModal"
      :show="showModal"
      @start="startGame"
      @close="showModal = false"
    />
    <TimerDisplay v-if="startTime && !gameCompleted" :startTime="startTime" />
    <SortingTable v-if="people.length" :people="people" @sorted="finishGame" />
    <SuccessModal
      v-if="gameCompleted"
      :show="gameCompleted"
      :timeTaken="timeTaken"
      @close="resetGame"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import SortingModal from "./components/SortingModal.vue";
import SortingTable from "./components/SortingTable.vue";
// import TimerDisplay from "./components/TimerDisplay.vue";
import TimerDisplay from "./components/TimerDisplay.vue"
import SuccessModal from "./components/SuccessModal.vue";

const showModal = ref(false);
const people = ref([]);
const startTime = ref(null);
const gameCompleted = ref(false);
const timeTaken = ref(0);

const generateRandomPeople = (count) => {
  const names = ["Alice", "Bob", "Charlie", "Diana", "Eve", "Frank"];
  const peopleSet = new Set();
  while (peopleSet.size < count) {
    peopleSet.add({
      id: crypto.randomUUID(),
      name: names[Math.floor(Math.random() * names.length)],
      email: `user${Math.floor(Math.random() * 1000)}@potatostan.com`,
      potatoes: Math.floor(Math.random() * 1000) + 1,
    });
  }
  return [...peopleSet];
};

const startGame = (count) => {
  people.value = generateRandomPeople(count);
  startTime.value = Date.now();
  gameCompleted.value = false; //timer resetting
  showModal.value = false;
};

const finishGame = () => {
  timeTaken.value = Math.floor((Date.now() - startTime.value) / 1000);
  gameCompleted.value = true;
  startTime.value = null; // Stop the timer
};

const resetGame = () => {
  people.value = [];
  startTime.value = null;
  gameCompleted.value = false;
};
</script>
<style scoped>
.button-sort {
  background-color: #ff8c00;
}
</style>
