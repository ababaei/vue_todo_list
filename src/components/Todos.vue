<script lang="ts">

import { defineComponent } from "vue"
import Todo from "./Todo.vue"

export default defineComponent({
    name: "Todos",
    emits: ["delete-todo"],
    components: {
        Todo
    },
    props: {
        todos: {
            type: Object,
            required: true
        }
    }
})

</script>

<template>
    <div>
        <h2>TODOLIST</h2>
        <ul>
            <li v-bind:key=todo.id v-for="todo in todos">
                <Todo :todo=todo @delete-todo="$emit('delete-todo', todo.id)" />
            </li>
        </ul>
    </div>
</template>

<style>
    h2 {
        margin-bottom: 10px;
        text-align: center;
    }

    ul {
        list-style-type: none;
    }
</style>