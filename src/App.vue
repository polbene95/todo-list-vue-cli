<template>
  <div id="app">
    <Header />
    <AddTodo @add-todo="addTodo" />
    <Todos v-bind:todos="todos" @del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

export default {
  name: "App",
  components: {
    Header,
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  created() {
    this.getTodos();
  },
  methods: {
    async getTodos() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/todos?_limit=5",
          {
            method: "GET",
          }
        );
        const todos = await response.json();
        this.todos = todos;
      } catch (error) {
        console.error(error);
      }
    },
    async deleteTodo(id) {
      try {
        await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
          method: "DELETE",
        });
        this.todos = this.todos.filter((todo) => todo.id !== id);
      } catch (error) {
        console.error(error);
      }
    },
    async addTodo({ title, completed }) {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/todos",
          {
            method: "POST",
            headers: {
              "Content-type": "application/json; charset=UTF-8",
            },
            body: JSON.stringify({
              title,
              completed,
            }),
          }
        );
        const newTodo = await response.json();
        this.todos.push(newTodo);
      } catch (error) {
        console.error(error);
      }
    },
  },
};
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
