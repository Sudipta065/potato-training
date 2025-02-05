<template>
  <div v-if="show" class="modal-overlay">
    <div class="modal">
      <button class="close-btn" @click="close">&times;</button>

      <h2 class="modal-title">🎉 Success!</h2>
      <p class="modal-text">
        You sorted the list correctly in
        <span class="time">{{ timeTaken }} seconds</span>!
      </p>

      <button class="primary-btn" @click="close">OK</button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(["show", "timeTaken"]);
const emit = defineEmits(["close"]);

const close = () => {
  emit("close");
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(5px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal {
  background: #ffffff;
  width: 350px;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.2);
  text-align: center;
  position: relative;
  animation: fadeIn 0.3s ease-in-out;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 22px;
  cursor: pointer;
  color: #6c757d;
}

.modal-title {
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #333;
}

.modal-text {
  font-size: 16px;
  color: #555;
  margin-bottom: 20px;
}

.time {
  font-weight: bold;
  color: #d9534f;
}

.primary-btn {
  background: #ff8c00;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s ease;
}

.primary-btn:hover {
  background: #e67e00;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
