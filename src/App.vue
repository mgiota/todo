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
body {
  font-family: 'Dancing Script', sans-serif;
  background-image: url("strawberry.png");
  background-repeat: repeat;
}

h1 {
  font-size: 5vh;
  text-decoration: underline;
}

.page-container {
  display: grid;
  max-width: 900px;
  margin: auto;
}

.page {
  display: grid;
  margin: 10%;
  padding: 2%;
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

.list-item {
  font-size: 3vh;
  padding-bottom: 3%;
}

label, button {
  cursor: pointer;
}



.md-checkbox {
  border: 2px solid #000;
  border-radius: 50%;
  background-color: green;
}

</style>
