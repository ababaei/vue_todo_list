<script lang="ts">
import { defineComponent } from "vue"
import Todos from "./components/Todos.vue"
import AddTodo from "./components/AddTodo.vue"

interface Todo {
  id: Number
  title: String
  conpleted: Boolean
}

export default defineComponent ({
  name: "app",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      test: "salam",
      todos: [] as Todo[]
    }
  },
  methods: {
    addTodo(newTodoObj: Todo) {
      this.todos = [...this.todos, newTodoObj];
    },
    deleteTodo(id: Number) {
      console.log(id);
      var index = this.todos.map(x => {return x.id;}).indexOf(id)
      this.todos.splice(index, 1);
    }
  }
});

</script>

<template>
  <div id="todolist">
    <Todos :todos="todos" @delete-todo="deleteTodo" />
    <AddTodo :todosLen=todos.length @add-todo="addTodo" />
  </div>
</template>

<style>
    .btn {
      margin-left: 5px;
      width:  20px;
      background: #5f27cd;
      border-radius: 5px;
      color: #ddfff7;
      font-weight: bold;
    }

    #app {
      /* display: flex;
      justify-content: center; */
      border-radius: 25px;
      background-color: #5f27cd;
      width: 25vw;
      height: 80vh;
      /* margin: 10vh 0; */
      /* margin-top: 3vw; */
    }  
</style>