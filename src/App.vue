<template>
  <input v-model="input" placeholder="Enter item">
  <button @click="addItem()">Pridať</button>
  <h2>Polozky</h2>
  <ul>
    <li v-for="item in validItems" :key="item.id">
      <span class="deleteItem" @click="deleteItem(item)">X</span>
      {{ item.text }}
    </li>
  </ul>
  <h2>Zmazane</h2>
  <ul>
    <li class="lineTrough" v-for="item in deletedItems" :key="`deleted-item-${item.id}`">
    {{ item.text }}
    </li>
  </ul>
</template>

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
    if (this.input.trim() === '') return
 
    this.items.push({
         id: this.items.length + 1,
         text: this.input,
         is_deleted: false
     });
     this.input = '';
},
      deleteItem(item) {
        item.is_deleted = true;
      }
    }
  };
</script>



<style scoped>

.lineTrough {
  text-decoration: line-through;
}

.deleteItem {
  cursor: pointer;
  margin-right: 15px;
}
</style>