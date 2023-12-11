<script lang="ts">
import { Component, Vue, toNative } from "vue-facing-decorator";

@Component
class PostItemForm extends Vue {
  item: Item = {
    name: "",
    quantity: 0,
    category: "",
  };

  async postItem(){
    try {
      const response = await fetch("http://localhost:8000/api/items", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.item),
      });
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error(error);
    }
  }
}

interface Item {
  name: string;
  quantity: number;
  category: string;
}

export default toNative(PostItemForm);
</script>

<template>
  <div class="container">
    <form>
      <label for="name">Name</label>
      <input type="text" id="name" name="name" v-model="item.name" />
      <label for="quantity">Quantity</label>
      <input
        type="number"
        id="quantity"
        name="quantity"
        v-model="item.quantity"
      />
      <label for="category">Category</label>
      <input
        type="text"
        id="category"
        name="category"
        v-model="item.category"
      />
      <button type="submit" @click="postItem">Submit</button>
    </form>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;

  padding: 3rem;
  border: 1px solid white;
  border-radius: 10px;
}
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}
label {
  font-size: 1.5rem;
}
</style>