<template>
  <div class="todoApp">
    <input
      type="text"
      v-model="todo"
      @keyup.enter="addTodo"
      placeholder="Add todo and hit enter"
    />
    <div class="todoItems" v-for="todo in todos" :key="todo">
      <label :class="{ completed: todo.completed }" :for="todo.id">
        <input :id="todo.id" type="checkbox" v-model="todo.completed" />
        {{ todo.todo }}
      </label>
      <button @click="deleteTodo(todo.id)">Delete</button>
    </div>
  </div>
</template>
<script lang="ts">
import { ref } from "vue";

export default {
  name: "TodoApp",
  setup() {
    const todo = ref(null);
    const todos = ref({});
    return {
      todo,
      todos,
      addTodo() {
        if (!todo.value) return;
        const uuid = new Date().getTime();
        todos.value[uuid] = {
          id: uuid,
          todo: todo.value,
          completed: false,
        };
        todo.value = "";
      },
      deleteTodo(item) {
        delete todos.value[item];
      },
    };
  },
};
</script>
<style scoped>
.todoItems {
  text-align: left;
  width: 500px;
  margin: 0 auto;
  padding: 20px 0;
  border-bottom: 1px solid #cccccc;
  display: flex;
  justify-content: space-between;
}
.todoItems label {
  cursor: pointer;
}
input {
  margin-right: 10px;
}

.completed {
  color: #cccccc;
  text-decoration: line-through;
}
</style>
