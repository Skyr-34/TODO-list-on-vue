<template>
  <div>
    <h4>Your TODO List</h4>
    <div class="todo-list">
      <div v-if="!todoList.length == 0">
        <div class="todo-item" v-bind:key="item" v-for="item in todoList">
          <button @click="compliteItem(item)">Complite</button>
          <p v-if="!item.complite">{{ item.text }}</p>
          <p class="item-complite" v-else>{{ item.text }}</p>
          <button @click="deleteItem(item)">Delete</button>
        </div>
      </div>
      <div v-else>
        <p>Your TODO list is empty</p>
      </div>
    </div>
  </div>

  <div class="add-list">
    <h3>Add TODO List</h3>
    <form @submit.prevent>
      <input v-bind:value="newItemText" @input="inputItemText" type="text" placeholder="Add your TODO">
      <button @click="createItem">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoList: [
        {id: 0, text: "TODO samething", complite: true},
        {id: 1, text: "TODO samething 1", complite: false},
        {id: 2, text: "TODO samething 2", complite: false},
        {id: 3, text: "TODO samething 3", complite: false},
      ],
      newItemText: '',
      
    }
  },
  methods: {
    compliteItem(item) {
      if (item.complite) {
        item.complite = false;
      } else {
        item.complite = true;
      }
    },
    deleteItem(item) {
      const i = this.todoList.indexOf(item);
      this.todoList.splice(i, 1);
      console.log(this.todoList.length);
    },
    createItem() {
      if (this.newItemText === '') {
        alert("Enter TODO text!!!");
      } else {
        const newItem = {
          id: Date.now(),
          text: this.newItemText,
          complite: false,
        }
        this.todoList.push(newItem);
        this.newItemText = '';
      }
    },
    inputItemText(event) {
      this.newItemText = event.target.value;
    }
  }
}
</script>

<style>
.todo-list {
  border: 2px solid #001369;
}
.todo-item {
  margin: 15px 0;
  width: 100%;
  display: flex;
  justify-content: space-around;
  border: 1px solid #001c69;
  height: 50px;
}

button {
  background: none;
  border: 1px solid #8e0a0a;
  padding: 5px 20px;
  color: #fff;
}

.item-complite {
  text-decoration: line-through;
  color: darkgrey;
}
.add-list {
  margin-top: 20px;
  border: 2px solid #8e0a0a;
  padding-bottom: 15px;
}

input {
  background-color: #373737;
  color: #fff;
  border: 1px solid  #8e0a0a;
  padding: 5px;
}
</style>