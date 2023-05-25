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
      const index = this.todos.map(x => {return x.id;}).indexOf(id)
      this.todos.splice(index, 1);
    },
    editTodo(id: String, newTitle: String) {
      const index = this.todos.map(x => {return x.id;}).indexOf(id);
      this.todos[index].title = newTitle;
    }
  },
  mounted() {
      const item: string | null = localStorage.getItem("todos"); 
      if (item)
        this.todos = JSON.parse(item);
  },
  watch: {
    todos: {
      handler() {
        localStorage.setItem("todos", JSON.stringify(this.todos));
      },
      deep: true
    }
  }
});

</script>

<template>
  <div id="todolist">
    <Todos :todos="todos"
      @delete-todo="deleteTodo"
      @edit-task="editTodo"
    />
    <AddTodo @add-todo="addTodo" />
  </div>
</template>

<style>
    .btn {
      margin-left: 5px;
      width:  20px;
      background: none;
      border: none;
      color: #ddfff7;
      font-weight: bold;
    }

    #app {
      border-radius: 25px;
      background-color: #5f27cd;
      width: 35vw;
      min-height: 80vh;
      height: fit-content;
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