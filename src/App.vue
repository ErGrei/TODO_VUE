<script>
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";
export default {

  data() {
    return {
      v$: useVuelidate(),
      newTodos: {
        title: "",
        description: "",
        errorZopa: false
      },
      todos: [
        {
          id: 1,
          title: "todo 1",
          description: "sdfgsdfgdsfgdsf",
          cheked: false,
        },
        {
          id: 2,
          title: "todo 2",
          description: "eghthnghnyjmyujn",
          cheked: false,
        },
      ],
    };
  },
  methods: {
    resetForm() {
      this.newTodos = {
        title: "",
        description: "",
      };
    },
    async addTodo() {
      const isFormCorrect = await this.v$.$validate(); // returns false or true
      if (!isFormCorrect) {
        this.newTodos.errorZopa = true
        return};
      this.todos.push({
        id: this.todos.length + 1,
        title: this.newTodos.title,
        description: this.newTodos.description,
        cheked: false,
      });
      this.resetForm();
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
      <header>
        <h1 class="title">Todo App</h1>
      </header>
      <main>
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
            <button class="button" type="submit">Add</button>
          </form>
        </section>

        <section class="todo">
          <h2 class="title" v-if="todos.length === 0">Todo List is empty</h2>
          <ul
            class="todo-list"
            :class="{ completed__task: todo.cheked }"
            v-for="todo in todos"
          >
            <li class="todo-item" :key="todo.id">
              <div class="view">
                <div class="cotainer__tittle__descrip">
                  <input class="toggle" type="checkbox" v-model="todo.cheked" />
                  <input
                    type="text"
                    class="label-title"
                    :class="{ cheked: todo.cheked }"
                    v-model="todo.title"
                  />
                </div>
                <input
                  type="text"
                  class="label-description"
                  :class="{ cheked: todo.cheked }"
                  v-model="todo.description"
                />

                <button
                  class="destroy"
                  :class="{ completed__task: todo.cheked }"
                  @click="deleteTodo(todo.id)"
                >
                  Del
                </button>
              </div>
            </li>
          </ul>
        </section>
      </main>
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

.button {
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

.button:hover {
  background-color: #c2d7eb;
}

.todo {
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 3px;
  padding: 0.5rem 0.8rem;
  margin-right: 0.5rem;
  margin-top: 0.5rem;
}
.todo-list {
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 3px;
  padding: 0.5rem 0.8rem;
  margin-right: 0.5rem;
  margin-top: 0.5rem;
}

.cotainer__tittle__descrip {
  display: flex;
  width: 100%;
}
.label-title {
  width: 100%;
  padding: 0.5rem 0.8rem;
  margin-right: 0.5rem;
  margin-top: 0.5rem;
}
.label-description {
  width: 100%;
  padding: 0.5rem 0.8rem;
  margin-right: 0.5rem;
  margin-top: 0.5rem;
}

.destroy {
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

.destroy:hover {
  background-color: #eb1313;
}

.cheked {
  text-decoration: line-through;
  color: #035711;
}

.completed__task {
  color: #035711;
  border: 1px, solid, #035711;
  border-radius: 0.5rem;
  background-color: #96f8a750;
  transition: all 0.8s ease;
}

.error {
  display: block;
  color: red;
}
</style>
