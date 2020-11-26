<template>
  <div>
    <md-card>
      <md-card-header class="header">To Do list </md-card-header>
      <md-field>
        <md-input
          class="input-item"
          v-model="currentTodo"
          @keydown.enter="addTodo()"
          placeholder="Add a todo..."
        ></md-input>
        <button class="hover" @click="addTodo()">
          <md-icon>add</md-icon>
        </button>
      </md-field>
      <ul class="todos">
        <li class="todo-item" v-for="todo in todos" :key="todo.id">
          <input
            class="completed"
            type="checkbox"
            @change="togglecompleted"
            v-model="todo.completed"
          />
          <span
            v-if="todo.editing === false"
            class="editing"
            :class="{ editing: todo == editedTodo }"
            @dblclick="editTodo(todo)"
          >
            {{ todo.label }}
          </span>
          <md-field v-if="todo.editing" class="editing">
            <md-input
              type="text"
              v-model="todo.label"
              @keyup.enter="cancelEdit(todo)"
              @keyup.esc="cancelEdit(todo)"
              @focusout="cancelEdit(todo)"
              placeholder="Change todo"
            />
          </md-field>
          <button v-if="todo.editing === false" @click="editTodo(todo)">
            Edit
          </button>
          <button v-if="todo.editing === true" @click="stopEdit(todo)">
            Save
          </button>
          <button v-if="todo.editing === false" @click="removeTodo(todo)">
            Delete
          </button>
          <button v-if="todo.editing === true" @click="editTodo(todo)">
            Cancel
          </button>
        </li>
      </ul>
    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editedTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false,
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      const index = this.todos.indexOf(todo);
      this.todos[index].editing = !this.todos[index].editing;
    },
    cancelEdit(todo) {
      todo.editing = false;
    },
  },
};
</script>


<style>
body {
  background-color: rgb(0, 0, 0);
}

.header {
  justify-content: center;
  text-align: center;
  font-size: 30px;
  font-style: oblique;
}

.md-card {
  max-width: 300px;
  margin: auto;
  margin-top: 20px;
  background-color: #3aadd6;
  color: #000000;
  text-transform: uppercase;
  padding: 20px;
}
ul {
  list-style-type: none;
  font-size: 16px;
  padding: 0px;
}
button {
  margin: 2px;
  border-radius: 5px;
  background-color: black;
  color: white;
}
.md-field {
  border: 3px solid white;
  border-radius: 10px;
  font-size: 20px;
  font-size: 20px;
}
.input-item {
  text-align: center;
  align-content: center;
}
</style>