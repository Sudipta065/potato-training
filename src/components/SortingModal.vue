<template>
  <div class="modal-overlay" v-if="show">
    <div class="modal">
      <button class="close-btn" @click="close">&times;</button>

      <h2 class="modal-title">Try our new user interface!</h2>
      <p class="modal-text">
        Please enter the number of people (between 20 and 100) to start sorting.
      </p>
      <input
        type="number"
        v-model="numPeople"
        min="20"
        max="100"
        @input="validateInput"
        class="input-field"
      />

      <p v-if="errorMessage" class="error-text">{{ errorMessage }}</p>
      <div class="modal-actions">
        <button class="secondary-btn" @click="close">Later</button>
        <button class="primary-btn" @click="startSorting" :disabled="!isValid">
          Try now
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const props = defineProps(["show"]);
const emit = defineEmits(["start", "close"]);

const numPeople = ref(20);
const errorMessage = ref("");

const isValid = computed(() => numPeople.value >= 20 && numPeople.value <= 100);

const validateInput = () => {
  if (numPeople.value < 20) {
    errorMessage.value = "Number must be at least 20.";
  } else if (numPeople.value > 100) {
    errorMessage.value = "Number must be at most 100.";
  } else {
    errorMessage.value = "";
  }
};

const startSorting = () => {
  if (isValid.value) {
    emit("start", numPeople.value);
  }
};

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
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}
.modal {
  background: white;
  width: 400px;
  padding: 25px;
  border-radius: 10px;
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.15);
  text-align: center;
  position: relative;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 22px;
  cursor: pointer;
  color: #555;
}

.modal-title {
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #222;
}

.modal-text {
  font-size: 16px;
  color: #555;
  margin-bottom: 20px;
}

.input-field {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 15px;
  outline: none;
  background-color: #fff;
  color: #333;
}

.error-text {
  color: red;
  font-size: 14px;
  margin-bottom: 10px;
}

.modal-actions {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.primary-btn {
  background: #ff8c00;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.3s ease;
}
.primary-btn:hover {
  background: #e67e00;
}
.primary-btn:disabled {
  background: #cccccc;
  cursor: not-allowed;
}

.secondary-btn {
  background: #f0f0f0;
  color: #333;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.3s ease;
}
.secondary-btn:hover {
  background: #e0e0e0;
}
</style>
