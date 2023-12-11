<script setup lang="ts">
import { ref } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import ListItems from "./components/ListItems.vue";
import PostItemForm from "./components/PostItemForm.vue";

let display = ref(false);
</script>

<template>
  <div>
    <HelloWorld msg="Home inventory" />
    <button @click="display = !display">Add Item</button>
    <div v-show="display"><PostItemForm /></div>
    <ListItems />
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  align-items: center;
}
button {
  margin-bottom: 2rem;
}
</style>
