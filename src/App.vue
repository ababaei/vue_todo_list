<script lang="ts">
import { defineComponent } from "vue"
import Todos from "./components/Todos.vue"
import AddTodo from "./components/AddTodo.vue"

interface Todo {
  id: String
  title: String
  completed: Boolean
  edit: Boolean
}

export default defineComponent ({
  name: "app",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [] as Todo[]
    }
  },
  methods: {
    addTodo(newTodoObj: Todo) {
      console.log("Add: " + newTodoObj.id);
      this.todos = [...this.todos, newTodoObj];
    },
    deleteTodo(id: String) {
      console.log("delete: " + id);
      var index = this.todos.map(x => {return x.id;}).indexOf(id)
      this.todos.splice(index, 1);
    }
  }
});

</script>

<template>
  <div id="todolist">
    <Todos :todos="todos" @delete-todo="deleteTodo" />
    <AddTodo @add-todo="addTodo" />
  </div>
</template>

<style>
    .btn {
      margin-left: 5px;
      width:  20px;
      background: none;
      border: none;
      /* border-radius: 5px; */
      color: #ddfff7;
      font-weight: bold;
    }

    #app {
      /* display: flex;
      justify-content: center; */
      border-radius: 25px;
      background-color: #5f27cd;
      width: 35vw;
      min-height: 80vh;
      height: fit-content;
      /* padding-bottom: 2vh; */
      min-width: 319px;
      box-shadow: 5px 5px 20px black;
    }

    @media (max-width: 1080px) {
      #app {
        width: 45vw;
      }
    }
    
    @media (max-width: 319px) {
      #app {
        display: none;
      }


    }
</style>