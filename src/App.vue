<script>
import Panel from "./components/Panel.vue";
import TodoTasks from "./components/TodoTasks.vue";

export default {
  components: {
    Panel,
    TodoTasks,
  },

  data() {
    return {
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
    addTodo(todo) {
      this.todos.push(todo);
    },

    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
};
</script>

<template>
  <div class="app">
    <div class="container">
      <panel :todos="todos" @addTodo="addTodo" />
      <todo-tasks :todos="todos" @deleteTodo="deleteTodo" />
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
