<template>
  <div class="todo-item" :class="{'is-completed': todo.completed}">
    <p>
      <input type="checkbox" v-model="todo.completed" />
      {{todo.title}}
      <button
        v-if="todo.completed"
        @click="$emit('del-todo', todo.id)"
        class="del"
      >X</button>
    </p>
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

.is-completed {
  text-decoration: line-through;
}

.del {
  background: #ff0000;
  color: #fff;
  float: right;
  border-radius: 25px;
  padding: 3px 5px;
  border: none;
}
</style>