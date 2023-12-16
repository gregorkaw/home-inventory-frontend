<script lang="ts">
import { Vue, Component, toNative } from "vue-facing-decorator";

@Component
class ListItems extends Vue {
  items: Item[] = [];

  mounted() {
    this.fetchItems();
  }

  async deleteItem(id: number) {
    try {
      const response = await fetch(`http://localhost:8000/api/items/${id}`, {
        method: "DELETE",
      });
      const data = await response.json();
      console.log(data);
      this.fetchItems();
    } catch (error) {
      console.error(error);
    }
  }
  async fetchItems() {
    try {
      const response = await fetch("http://localhost:8000/api/items");
      const data = await response.json();
      this.items = data.items;
      console.log(data);
    } catch (error) {
      console.error(error);
    }
  }
}

interface Item {
  id: number;
  name: string;
  quantity: number;
  category: string;
}

export default toNative(ListItems);
</script>

<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Quantity</th>
          <th>Category</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.id">
          <td>{{ item.name }}</td>
          <td>{{ item.quantity }}</td>
          <td>{{ item.category }}</td>
          <td><button @click="deleteItem(item.id)">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
div {
  width: 75%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 10px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 1rem;
  text-align: center;
  border-bottom: 1px solid #ddd;
}

td button {
  background-color: #ff4d4f;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 0.5rem 0.33rem;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

td button:hover {
  background-color: #ff7875;
}

td button:focus {
  outline: none;
}

td button:active {
  background-color: #ff4d4f;
}
</style>
