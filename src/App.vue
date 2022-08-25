<script>
export default {
  name: 'App',
  data() {
    return {
      header: "Shopping List",
      editing: false,
      newItem: "",
      newItemHighPriority: false,
      items: [
        { id: 1, label: "10 milk", purchased: true, highPriority: false },
        { id: 2, label: "20 eggs", purchased: false, highPriority: true },
        { id: 3, label: "30 bread", purchased: false, highPriority: false },
      ]
    }
  },
  computed: {
    CharacterCount() {
      return this.newItem.length
    },
    reversedItems() {
      return [...this.items].reverse()
    }
  },
  methods: {
    addItem() {
      this.items.push({
        id: this.items.length + 1,
        label: this.newItem,
        highPriority: this.newItemHighPriority
      });
      this.newItem = ""
      this.newItemHighPriority = false
    },
    doEdit(editing) {
      this.editing = editing
      this.newItem = ""
      this.newItemHighPriority = false
    },
    togglePurchased(item) {
      item.purchased = !item.purchased

    }
  }
}
</script>

<template>

  <section class="w-full bg-teal-50">
    <div class="mx-auto text-slate-600 text-center font-bold py-2 px-4 rounded">
      <h1 class="text-3xl mx-auto text-center pt-2">{{ header }}</h1>
    </div>
    <div class="mx-auto text-center py-2 px-4 pt-10">

      <button class="bg-teal-100 text-salte-600 font-bold mb-3 py-2 px-4 rounded" @click="doEdit(true)">Add
        Item</button>
    </div>

    <div v-if="editing" class="mx-auto">
      <input class="mx-2 bg-white appearance-none border-2 border-gray-200 rounded w-1/2 py-1 px-2 text-gray-700"
        v-on:keyup.enter="addItem" v-model="newItem" type="text" placeholder="Add an item" id="input">
      <label><input class="mx-2" type="checkbox" v-model="newItemHighPriority" value=true>High Priority</label>
      <p class="counter">{{ CharacterCount }}/100</p>
      <div class="flex flex-wrap mb-1">
        <button class="bg-teal-100 text-salte-600 font-bold py-1 px-2 rounded mx-2" v-on:click="addItem"
          v-bind:disabled="newItem.length === 0">Add</button>
        <button class="bg-teal-100 text-salte-600 font-bold py-1 px-2 rounded" v-if="editing"
          @click="doEdit(false)">Cancel</button>
      </div>
    </div>
    <p v-if="items.length === 0">Add some items to your List!!</p>
    <ul>
      <li class="text-lg" :class="{ strikeout: item.purchased, highPriority: item.highPriority }" @click="togglePurchased(item)" v-for="item in items" :key="item.id">
        {{ item.label }}</li>
    </ul>
  </section>
</template>

<style scoped>
.strikeout {
  text-decoration: line-through;
  color: #b8c2cc;
}

li {
  padding-left: 1rem;
}

.counter {
  font-size: 1rem;
  color: #b8c2cc;
  padding-left: 1rem;
  margin-bottom: 0.5rem;
}

.strikeout:hover {
  color: #8795a1;
}
.highPriority {
    color: #DE751F;
}
</style>
