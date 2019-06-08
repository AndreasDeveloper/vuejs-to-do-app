<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos"  v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'home',
  components: {
    Todos,
    AddTodo
  },
  // Seed Data
  data() {
    return {
      todos: [],
    }
  },
  // Methods
  methods: {
    // Delete Todo Method
    async deleteTodo(id) {
      try {
        const delReqRes = await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        this.todos = this.todos.filter(el => el.id !== id);
      } catch (err) {
        throw new Error(err);
      }
    },
    // Add Todo Method
    async addTodo(newTodo) {
      const { title, completed } = newTodo;
      try {
        const postReqRes = await axios.post('https://jsonplaceholder.typicode.com/todos', {
          title,
          completed // Destructured data from newTodo
        });
        this.todos = [...this.todos, postReqRes.data]; // Copying and adding already existing todos to new todos
      } catch (err) {
        throw new Error(err);
      }
    }
  },
  // Created Method - Run HTTP request - GET SEEDED TODOS FROM JSONPlaceholder
  async created() {
    try {
      const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=6');
      this.todos = res.data;
    } catch (err) {
      throw new Error(err);
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
