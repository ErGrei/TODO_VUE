<script>
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";
import Panel from "./components/Panel.vue";
import TodoTasks from "./components/TodoTasks.vue";
export default {
  components: {
    Panel,
    TodoTasks,
  },
  data() {
    return {
      v$: useVuelidate(),
      newTodos: {
        title: "",
        description: "",
        errorZopa: false,
      },
      todos: [
        {
          id: 1,
          title: "Todo 1",
          description: "Description 1",
          cheked: false,
        },
        {
          id: 2,
          title: "Todo 2",
          description: "Description 2",
          cheked: false,
        },
        {
          id: 3,
          title: "Todo 3",
          description: "Description 3",
          cheked: false,
        },
      ],
    };
  },
  methods: {
  

    async addTodo() {
      const isFormCorrect = await this.v$.$validate(); // returns false or true
      if (!isFormCorrect) {
        this.newTodos.errorZopa = true;
        return;
      }
      this.todos.push({
        id: this.todos.length + 1,
        title: this.newTodos.title,
        description: this.newTodos.description,
        cheked: false,
      });
      this.resetForm();
    },

    resetForm() {
      this.newTodos = {
        title: "",
        description: "",
      };
    },

    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },

  validations() {
    return {
      newTodos: {
        title: { required },
        description: { required },
      },
    };
  },
};
</script>

<template>
  <div class="app">
    <div class="container">
      <panel :newTodos="newTodos" />
      <todo-tasks :todos="todos" />
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>
