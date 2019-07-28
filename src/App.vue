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
          {{ todo.label }}
          <button class="delete-button" @click="removeTodo(todo)">Delete</button>
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
      currentTodo: ''
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
@import url('https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.css');
@import url('https://fonts.googleapis.com/css?family=Dancing+Script&display=swap');

body {
  font-family: 'Dancing Script', cursive;
  background-image: url("strawberry.png");
  background-repeat: repeat;
  max-width: 600px;
  margin: 5vh auto 5vh auto;
}

h1 {
  font-size: 5vh;
  text-decoration: underline;
}

.page {
  margin: 0 10% 0 10%;
  display: grid;
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
  padding: 5% 0 5% 5%;

}

.list-items {
  font-size: 3vh;
  padding-bottom: 3%;
}

</style>
