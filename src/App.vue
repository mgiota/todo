<template>
  <div class="page">
    <div class="title-container">
      <h1>My to-do list</h1>
    </div>
    <div class="input-container">
      <input class="text-input" v-model="currentTodo" @keydown.enter="addTodo()" placeholder=" Type here">
    </div>
    <div class="list-container">
      <ul class="todos">
        <li class="list-items" v-for="todo in todos" :key="todo.id">
          <label class="checkbox-container">
            <input type="checkbox">
            <span class="checkmark"></span>
            {{ todo.label }}
          </label>

          <button class="edit-button" v-model="todo.editingTodo" @click="editTodo(todo)">
            <svg class="pen" width="20" height="20" fill="none" stroke="#000" stroke-width="1.05">
              <path d="M4 12 L15 1 L19 5 L8 16 L4 12"/>
              <path d="M16 4 L7 13"/>
              <path d="M3 13 L7 17 L1 19 L3 13 "/>
            </svg>
          </button>
          <button class="delete-button" @click="removeTodo(todo)">
            <svg class="trashcan" width="20" height="20" fill="none" stroke="#000" stroke-width="1.05">
              <path class="can" d="M4 18 L16 18 L16 5 L4 5 Z"/>
              <path class="can" d="M7 16 L7 7"/>
              <path class="can" d="M10 16 L10 7"/>
              <path class="can" d="M13 16 L13 7"/>
              <path class="can" d="M3 2.5 L17 2.5"/>
              <path class="can" d="M8.5 1.5 L11.5 1.5"/>
            </svg>
          </button>
          <div v-if="todo.editingTodo">
            <input class="edit-input" type="text" v-model="todo.editedTodo" @keyup.esc="hideEditTodo(todo)" @keydown.enter="updateTodo(todo)" placeholder=" Edit here">
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>



<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: '',
      editingTodo: '',
      editedTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, editingTodo: false});
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.editingTodo = true;
    },
    updateTodo(todo) {
      todo.label = todo.editedTodo;
      todo.editingTodo = false;
    },
    hideEditTodo(todo) {
      todo.editingTodo = false;
    }
  }
};
</script>


<style>
body {
  font-family: 'Quicksand', sans-serif;
  background-image: url("strawberry.png");
  background-repeat: repeat;
  max-width: 900px;
  margin: auto;
}

h1 {
  font-size: 5vh;
  text-decoration: underline;
}

.page {
  display: grid;
  margin: 10%;
  padding: 5% 2% 5% 2%;
  grid-template-rows: 15vh 10vh auto;
  border: 5px solid #9ACD32;
  border-radius: 30px;
  background-color: white;
}

.title-container {
  margin: auto;
}

.input-container {
  margin: auto;
}

.text-input, .edit-input {
  width: 50vw;
  max-width: 350px;
  font-family: inherit;
  font-size: 3vh;
  background-color: #e1f0c1;
  border: none;
  padding: 1% 0 1% 0;
}

.edit-input {
  margin-bottom: 5%;
  width: 35vw;
}

.list-container {
  min-height: 55vh;
  margin-top: 5%;
}

label, button {
  cursor: pointer;
  margin-bottom: 5%;

}

label {
  padding-right: 5px;
}

li {
    list-style-type: none;
}

/* Hide the browser's default checkbox */
.checkbox-container input {
  display: none;
}

.checkbox-container {
  display: inline-block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 3vh;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #fff;
  border: 3px solid #9ACD32;
  border-radius: 50%;
}

.checkbox-container input:checked ~ .checkmark {
  background-color: #9ACD32;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-container input:checked ~ .checkmark:after {
  display: inline-block;
  left: 8px;
  top: 4px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

button {
  display: inline-block;
  background: none;
  border: none;
}

svg {
  width: 20px;
  height: 20px;
}

</style>
