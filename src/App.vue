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
  <div id="app">
    <Todos :todos="todos" @delete-todo="deleteTodo" />
    <AddTodo :todosLen=todos.length @add-todo="addTodo" />
  </div>
</template>

<style>
    .btn {
      background: #5f27cd;
      border-radius: 5px;
      color: #ddfff7;
      font-weight: bold;
    }

    #app {
      margin-top: 3vw;
    }
</style>