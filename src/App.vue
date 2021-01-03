<template>
  <div id="app">
    <div class="section">
      <div class="container">
        <Todos :todos="todos" @addTodo="addTodo" @onComplete="completed" @onDelete="deleteTodo" />
      </div>
    </div>
  </div>
</template>

<script>
import "bulma/css/bulma.css";
import Todos from './components/Todos' 
export default {
  name: "App",
  components: {
    Todos,
  },
  data() {
    return{
      todos: [
        {
          "userId": 1,
          "id": 1,
          "title": "delectus aut autem",
          "completed": false
        },
        {
          "userId": 1,
          "id": 2,
          "title": "quis ut nam facilis et officia qui",
          "completed": true
        },
      ],
    };
  },
  methods:{
    addTodo(todo){
      this.todos.unshift(todo);
    },
    completed(id){
      const updated_todos = this.todos.map(todo => todo.id == id ? Object.assign(todo, { completed: true }) : todo );
      this.todos = updated_todos;
    },
    deleteTodo(id){
      let deleted_todos = this.todos.filter(todo => todo.id != id);
      this.todos = deleted_todos;
    }
  },
};
</script>

<style>

#app {

  background-color: #f8961e;
  font-family: 'Roboto', sans-serif;
  min-height: 100vh;
}
</style>
