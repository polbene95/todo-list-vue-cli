<template>
  <div class="todo-item">
    <div>
      <div>
        <input type="checkbox" v-model="todo.completed" />
      </div>
      <p :class="{'is-completed': todo.completed}">{{todo.title}}</p>
      <div>
        <button v-show="todo.completed" @click="$emit('del-todo', todo.id)" class="del">X</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.todo-item > div {
  margin: auto;
  max-width: 900px;
  word-wrap: break-word;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.todo-item > div > div:nth-child(1),
.todo-item > div > div:nth-child(3) {
  width: 5%;
}
.todo-item > div > p {
  width: 87%;
  word-wrap: break-word;
}

.is-completed {
  text-decoration: line-through;
}

.del {
  background: #ff0000;
  color: #fff;
  align-self: flex-end;
  border-radius: 25px;
  padding: 3px 5px;
  border: none;
}
</style>