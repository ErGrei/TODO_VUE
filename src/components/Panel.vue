<script>
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";

export default {
  
  name: "Panel",
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      v$: useVuelidate(),
      newTodos: {
        title: "",
        description: "",
        errorZopa: false,
      },
    };
  },

  methods: {
    async addTodo() {
      this.newTodos.id = Date.now();
      this.newTodos.cheked = false;
      this.newTodos.editable = false;
      this.btnChange = 'Change';

      const isFormCorrect = await this.v$.$validate();

      if (!isFormCorrect) {
        this.newTodos.errorZopa = true;
        return;
      }
      this.$emit("addTodo", this.newTodos);

      // this.todos.push({
      //   id: this.todos.length + 1,
      //   title: this.newTodos.title,
      //   description: this.newTodos.description,
      //   cheked: false,
      // });
      this.resetForm();
    },

    resetForm() { 
      this.newTodos = { 
        title: "",
        description: "",
        errorZopa: false
      };
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
    <h1 class="title">Todo App</h1>
    <section class="todoapp">
      <form @submit.prevent="addTodo">
        <input
          type="text"
          class="new-todo"
          v-model.trim="newTodos.title"
          placeholder="Title"
        />
        <span class="error" v-if="newTodos.errorZopa">
          This field is required</span
        >
        <input
          v-model.trim="newTodos.description"
          placeholder="What needs to be done?"
          class="new-todo"
          type="text"
        />
        <span class="error" v-if="newTodos.errorZopa">
          This field is required</span
        >
        <button class="button__add" type="submit">Add</button>
      </form>
    </section>
  </div>
</template>

<style scoped>
.title {
  text-align: center;
}

.todoapp {
  width: 100%;
  margin: 0 auto;

  margin: 0 auto;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 1rem;
}
.new-todo {
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 3px;
  padding: 0.5rem 0.8rem;
  margin-right: 0.5rem;
  margin-top: 0.5rem;
}

.button__add {
  width: 5rem;
  height: 2rem;
  background-color: #ccc;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 1rem;
}

.button__add:hover {
  background-color: #c2d7eb;
}

.error {
  display: block;
  color: red;
}
</style>
