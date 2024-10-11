<script>
  export default {
    data() {
      return {
        input: '',
        items: []
      };
    },
    computed: {
      validItems() {
        return this.items.filter(item => !item.is_deleted);
      },
      deletedItems() {
        return this.items.filter(item => item.is_deleted);
      }
    },
    methods: {
      addItem() {
        if (this.input.trim() !== '') {
          this.items.push({
            id: this.items.length + 1,
            text: this.input,
            is_deleted: false
          });
          this.input = '';
        }
      },
      deleteItem(item) {
        item.is_deleted = true;
      }
    }
  };
</script>

<template>
  <input v-model="input" placeholder="Enter item">
  <button @click="addItem()">Pridať</button>
  <h2>Polozky</h2>
  <ul>
    <li v-for="item in validItems" :key="`item-${item.id}`">
      <span @click="deleteItem(item)" style="cursor: pointer; margin-right: 15px">X</span>
      {{ item.text }}
    </li>
  </ul>
  <h2>Zmazane</h2>
  <ul>
    <li v-for="item in deletedItems" :key="`deleted-item-${item.id}`" style="text-decoration: line-through;">
    {{ item.text }}
    </li>
  </ul>
</template>

<style scoped>
</style>