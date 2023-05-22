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
    <div id="list">
        <h2>TODOLIST</h2>
        <hr>
        <ul>
            <li v-bind:key=todo.id v-for="todo in todos">
                <Todo :todo=todo @delete-todo="$emit('delete-todo', todo.id)" />
                <hr>
            </li>
        </ul>
    </div>
</template>

<style>
    #list {
        position: relative;
        top: 0;
        margin-top: 0;
    }

    h2 {
        margin-bottom: 1em;
        text-align: center;
    }

    ul {
        padding: 0;
        width:auto;
        list-style-type: none;
        margin-left: 0;
    }

    ul li {
        margin-left: 0;
    }
</style>