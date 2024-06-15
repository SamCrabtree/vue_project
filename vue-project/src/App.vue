<script setup>
import { ref, computed, reactive } from 'vue'
const header = ref('Shopping List App')
const editing = ref(false)
const items = ref([
  {
    id:1, 
    label:"100 Hats", 
    purchased:false, 
    highPriority:true 
  }, 
  {
    id:2, 
    label:"3 Board Games", 
    purchased:false, 
    highPriority:false  
  }, 
  {
    id:3,
    label:"100 Cups", 
    purchased:true, 
    highPriority:false  
  }
])

const state = reactive({count:0})
const increment = ()=> {
  state.count++
}

const reversedItems = computed(()=>{
  return [...items.value].reverse()
})
const newItem = ref("")
const newItemPriority = ref(false)
const saveItem = ()=>{
  items.value.push(
    {
      id: items.value.length + 1,
      label: newItem.value,
      highPriority: newItemPriority.value
    })
  newItem.value = ""
}
const doEdit = (e)=>{
  editing.value = e
  newItem.value = ""
  newItemPriority = ""
}

const togglePurchased = (item) =>{
  item.purchased = !item.purchased
}
</script>

<template>
    
    <div class="header">
      <h1>{{ header }}</h1>
      <button 
      v-if="editing"
      class="btn btn-warning"
      @click="doEdit(false)">
        Cancel
      </button>
      <button v-else class="btn btn-primary" @click="doEdit(true)">
        Add Item
      </button>
    </div>
    <form 
      v-if="editing"
      class="add-item-form"
      @submit.prevent="saveItem" 
      >
      <input v-model.trim="newItem" type="text" placeholder="Add an item">
      <label>
        <input type="checkbox" v-model="newItemPriority">
        High Priority
      </label>
      <button 
      v-bind:disabled="newItem.length === 0"
      class="btn btn-primary">
      Save Item 
      </button>
    </form>

    <div class="container">
    <ul>
      <li 
          v-for="(item, index) in reversedItems" 
          @click="togglePurchased(item)"
          :key="item.id"
          :class="{
            strikeout: item.purchased, 
            priority: item.highPriority}">
        {{item.label}}
      </li>
    </ul>
    <p v-if="!items.length">
    Nothing to see here...
    </p>
    </div>
    <div class="counter">
      <button @click="increment">Increase Number Below</button>
      <h3>{{state.count}}</h3>
    </div>
  
</template>
