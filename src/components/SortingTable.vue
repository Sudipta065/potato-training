<template>
  <div class="table-container">
    <h2 class="table-head">Sort People by Potatoes</h2>

    <div class="table">
      <div class="table-header">
        <div class="table-cell header">Name</div>
        <div class="table-cell header">Email</div>
        <div class="table-cell header">Potatoes</div>
      </div>

      <draggable
        v-model="peopleList"
        tag="div"
        class="table-body"
        item-key="id"
        @end="checkSorting"
      >
        <template #item="{ element }">
          <div class="table-row">
            <div class="table-cell name">{{ element.name }}</div>
            <div class="table-cell email">{{ element.email }}</div>
            <div class="table-cell potatoes">{{ element.potatoes }}</div>
          </div>
        </template>
      </draggable>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from "vue";
import draggable from "vuedraggable";

const props = defineProps(["people"]);
const emit = defineEmits(["sorted"]);
const peopleList = ref([...props.people]);

const checkSorting = () => {
  const sorted = [...peopleList.value].sort((a, b) => b.potatoes - a.potatoes);
  if (JSON.stringify(sorted) === JSON.stringify(peopleList.value)) {
    emit("sorted");
  }
};
</script>

<style scoped>
.table-container {
  background: #ffffff;
  padding: 20px;
  border-radius: 10px;
  /* box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.1); */
  overflow: hidden;
  margin: 20px 0;
  width: 100%;
}

.table {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.table-head {
  color: #2c3e50;
}

.table-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 16px;
  background: #f8f9fa;
  font-weight: 600;
  font-size: 14px;
  color: #5a5a5a;
  border-bottom: 2px solid #e0e3e7;
}

.table-body {
  display: flex;
  flex-direction: column;
}

.table-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  font-size: 14px;
  color: #2c3e50;
  border-bottom: 1px solid #e0e3e7;
  transition: background 0.2s ease-in-out;
}

.table-row:nth-child(even) {
  background: #f5f7fa;
}
.table-row:nth-child(odd) {
  background: #ffffff;
}

.table-row:hover {
  background: #e8ebef;
}
.table-cell {
  flex: 1;
  padding: 6px 10px;
  text-align: left;
  font-size: 14px;
  font-weight: 500;
  color: #495057;
}

.name {
  font-weight: 600;
  color: #1f2937;
}

.email {
  color: #3b82f6;
  text-decoration: underline;
}

.potatoes {
  text-align: right;
  font-weight: bold;
}
</style>
