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
  const newItem = ref("")
  const newItemPriority = ref("")
  const saveItem = (high)=>{
    if(high){
      itemsHighPriority.value.push({
      id:itemsHighPriority.value.length +1,
      label: newItem.value,
      completed: false
    })
      newItem.value = ""
      newItemPriority.value = ""
    }
    else{
      itemsNormalPriority.value.push({
      id:itemsHighPriority.value.length +1,
      label: newItem.value,
      completed: false
    })      
      newItem.value = ""
    }
  }
  const toggleCompleted = (items)=>{
    items.completed = !items.completed
  }
  const deleteThis = (array,item)=>{
    array.splice(item, 1);
  }


</script>

<template>
  <div class="header">
    <h1>To Do List</h1>
  </div>
    <div class="inputField">
      <form 
        class="add-item-form"
        v-on:submit.prevent="saveItem(newItemPriority)"
      >
      <input
        v-model.number="newItem"
        type="text"
        placeholder="Add a task!"
      >
      <label>
        <input
          type="checkbox" v-model="newItemPriority"
        >
        Priority
      </label>
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
      >
        <li
          @click="toggleCompleted(item)"
          :key="item.id"
          class="static-class, priority"
          :class="{
            strikeout: item.completed}"
          >
          {{ item.label }}
        </li>
      <button
        :key="item.id"
        @click="deleteThis(itemsHighPriority,item.key)"
        > Delete This </button>
      </li>
    </ul>
    <ul class="NormalPriority">
      <li
        v-for="(item, index) in itemsNormalPriority"
      >
        <li
          @click="toggleCompleted(item)"
          :key="item.id"
          class="static-class"
          :class="{
            strikeout: item.completed}"
          >
          {{ item.label }}
        </li>
      <button
        :key="item.id"
        @click="deleteThis(itemsNormalPriority,item.key)"
        > Delete This </button>
      </li>
    </ul>
  </div>
</template>

