<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },

  methods: {
    deleteTodo(id) {
      this.$emit("deleteTodo", id);
    },

    changeTask(id) {
      this.$emit("changeTask", id);
    },

    togleBtn() {
      this.$emit("togleBtn", todo);
    }
  },
};
</script>

<template>
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
              :readonly="!todo.editable"
              class="label-title"
              :class="{ cheked: todo.cheked }"
              v-model="todo.title"
            />
          </div>
          <input
            type="text"
            :readonly="!todo.editable"
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
          <button
            class="change"
            :class="{
              completed__task: todo.cheked,
              change__task: todo.editable,
            }"
            @click="changeTask(todo.id)"
          >
            {{ todo.editable ? "Save" : "Change" }}
          </button>
        </div>
      </li>
    </ul>
  </section>
</template>

<style scoped>
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
  background-color: #cccccc00;
}
.label-description {
  width: 100%;
  padding: 0.5rem 0.8rem;
  margin-right: 0.5rem;
  margin-top: 0.5rem;
  margin-top: 0.5rem;
  background-color: #cccccc00;
}
.label-description:hover,
.label-title:hover {
  border: #035711, 1px, solid;
  border-radius: 0.5rem;
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

.change {
  width: 5rem;
  height: 2rem;
  background-color: #ccc;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 1rem;
  margin-left: 1rem;
}

.change:hover {
  background-color: #035711;
}

.change__task {
  border: 1px, solid, #035711;
  border-radius: 0.5rem;
  background-color: #057017b0;
  transition: all 0.8s ease;
}
</style>
