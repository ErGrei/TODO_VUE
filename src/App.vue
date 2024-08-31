<script>
import Panel from "./components/Panel.vue";
import TodoTasks from "./components/TodoTasks.vue";

export default {
  components: {
    Panel,
    TodoTasks,
  },

  mounted() {
    const todosFromStorage = localStorage.getItem(this.STORAGE_KEY);
    try {
      this.todos = todosFromStorage ? JSON.parse(todosFromStorage) : [];
    } catch (error) {
      console.error("Error while parsing todos from localStorage:", error);
    }
  },

  data() {
    return {
      STORAGE_KEY: "todos",
      todos: [],
    };
  },

  methods: {
    addTodo(todo) {
      this.todos.push(todo);
      localStorage.setItem(this.STORAGE_KEY, JSON.stringify(this.todos));
    },

    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      localStorage.setItem(this.STORAGE_KEY, JSON.stringify(this.todos));
    },

    changeTask(id) {
      this.todos = this.todos.map((todo) => {
        if (todo.id === id) {
          todo.editable = !todo.editable;
          console.log(todo.editable);
          togleBtn();
        }
        return todo;
      });
      localStorage.setItem(this.STORAGE_KEY, JSON.stringify(this.todos));
    },

    togleBtn() {
      if (todo.editable) {
        this.btnChange = "Save";
        return;
      }
      this.btnChange = "Change";
    },
  },
};
</script>

<template>
  <div class="app">
    <div class="container">
      <panel :todos="todos" @addTodo="addTodo" />
      <todo-tasks
        :todos="todos"
        @deleteTodo="deleteTodo"
        @changeTask="changeTask"
      />
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
