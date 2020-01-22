<template>
  <div>
    <BaseInput v-model="newTodoText" placeholder="New todo" @keydown.enter="addTodo" />
    <ul v-if="todos.length">
      <TodoListItem v-for="todo in todos" :key="todo.id" :todo="todo" @remove="removeTodo" />
    </ul>
    <p v-else>Nothing left in the list. Add a new todo in the input above.</p>
  </div>
</template>

<script>
import BaseInput from "./BaseInput.vue";
import TodoListItem from "./TodoListItem.vue";

let nextTodoId = 1;

export default {
  components: {
    BaseInput,
    TodoListItem
  },

  data() {
    return {
      newTodoText: "",
      todos: [
        {
          id: nextTodoId++,
          text: "Learn Modern Frontend Development Flow"
        },
        {
          id: nextTodoId++,
          text: "Learn Vue.js"
        },
        {
          id: nextTodoId++,
          text: "To be a full stack developer"
        }
      ]
    };
  },

  methods: {
    addTodo() {
      const trimmedText = this.newTodoText.trim();
      if (trimmedText) {
        this.todos.push({
          id: nextTodoId++,
          text: trimmedText
        });
        this.newTodoText = "";
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== id;
      });
    }
  }
};
</script>

<style scoped>
</style>