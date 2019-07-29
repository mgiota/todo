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
          <button class="delete-button" @click="removeTodo(todo)">
            <svg class="trashcan" viewBox="0 0 400 400" width="400" height="400" background="#fff" fill="none" stroke="#000" stroke-width="25">
              <path class="can" d="M80 360 L320 360 L340 100 L60 100 Z"/>
              <path class="can" d="M130 320 L120 140"/>
              <path class="can" d="M200 320 L200 140"/>
              <path class="can" d="M270 320 L280 140"/>
              <path class="can" d="M50 55 L350 55"/>
              <path class="can" d="M170 40 L230 40"/>
            </svg>
          </button>
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
      completed: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false});
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    }
  }
};
</script>


<style>
body {
  font-family: 'Dancing Script', sans-serif;
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

.text-input {
  width: 50vw;
  max-width: 350px;
  font-family: inherit;
  font-size: 3vh;
  background-color: #e1f0c1;
  border: none;
  padding: 1% 0 1% 0;
}

.list-container {
  min-height: 55vh;
  margin-top: 5%;
}

label, button {
  cursor: pointer;

}

label {
  padding-right: 20px;
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
