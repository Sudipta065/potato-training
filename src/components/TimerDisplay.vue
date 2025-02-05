<template>
  <div v-if="startTime" class="timer">
    Time: <span class="timer-value">{{ elapsedTime }}s</span>
  </div>
</template>

<script setup>
import { ref, watchEffect } from "vue";
import { useNow } from "@vueuse/core";

const props = defineProps(["startTime"]);
const elapsedTime = ref(0);

watchEffect(() => {
  if (props.startTime) {
    elapsedTime.value = Math.floor((useNow().value - props.startTime) / 1000);
  }
});
</script>

<style scoped>
.timer {
  font-size: 18px;
  font-weight: 600;
  color: #6c757d;
  background: #f8f9fa;
  padding: 10px 15px;
  border-radius: 8px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.timer-value {
  color: #d9534f;
  font-weight: bold;
}
</style>
