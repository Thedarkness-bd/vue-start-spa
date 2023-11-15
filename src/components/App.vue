<template>
  <div class="header">
    <h1>{{ msg }}</h1>
    <button class="btn" v-if="editing" @click="doEdit(false)">Cancel</button>
    <button class="btn btn-primary" v-else @click="doEdit(true)">
      Add Item
    </button>
  </div>
  <form class="add-item-form" @submit.prevent="saveItem" v-if="editing">
    <input type="text" placeholder="Add items" v-model.trim="newItem" />

    <label>
      <input type="checkbox" v-model="newItemPriority" /> High Priority
    </label>
    <button class="btn btn-primary">Save item</button>
  </form>
  <ul>
    <li v-for="({ id, name }, index) in items" :key="id">{{ name }}</li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>
</template>

<script setup>
import { ref } from "vue";

const msg = ref("Shopping List App");
const items = ref([
  //   { id: 1, name: "Cauliflower" },
  //   { id: 2, name: "Potato" },
  //   { id: 3, name: "Cherry" },
]);
const newItem = ref("");
const newItemPriority = ref(false);
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, name: newItem.value });
  newItem.value = "";
};
const editing = ref(false);
const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};
</script>
