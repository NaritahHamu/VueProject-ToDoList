<script setup>
  import { ref, computed } from 'vue'

  const itemsHighPriority = ref([
  {id: 1, label: "Task 1", completed: true},
  {id: 2, label: "Task 2", completed: false},
  {id: 3, label: "Task 3", completed: false}
])
  const itemsNormalPriority = ref([
  {id: 1, label: "Task 3", completed: true},
  {id: 2, label: "Task 2", completed: true},
  {id: 3, label: "Task 1", completed: false}
])


</script>

<template>
  <div class="header">
    <h1>To Do List</h1>
  </div>
    <div class="inputField">
      <form 
        class="add-item-form"
      >
      <input
        type="text"
        placeholder="Add a task!"
      >
      
      <button
        class="btn btn-primary"
      >
        Save Item
      </button>
    </form>
    </div>
  <div class="list">
    <ul class="HighPriority">
      <li
        v-for="(item, index) in itemsHighPriority"
        :key="item.id"
        class="static-class, priority"
        :class="{
          strikeout: item.completed}"
        >
        {{ item.label }}
      </li>
    </ul>
    <ul class="NormalPriority">
      <li
        v-for="(item, index) in itemsNormalPriority"
        :key="item.id"
        class="static-class"
        :class="{
          strikeout: item.completed}"
        >
        {{ item.label }}
      </li>
    </ul>
  </div>
</template>

