<script lang="ts">

import { defineComponent } from "vue"
import Todo from "./Todo.vue"

export default defineComponent({
    name: "Todos",
    emits: ["delete-todo", "edit-task"],
    components: {
        Todo
    },
    props: {
        todos: {
            type: Object,
            required: true
        }
    },
})

</script>

<template>
    <div id="list">
        <h2>TODOLIST</h2>
        <ul>
            <hr>
            <li v-bind:key=todo.id v-for="todo in todos">
                <Todo :todo=todo
                    @delete-todo="$emit('delete-todo', todo.id)"
                    @edit-task="$emit('edit-task', todo.id, $event)"
                />
                <hr>
            </li>
        </ul>
    </div>
</template>

<style>
    /* #list {
        position: relative;
        top: 0;
        margin-top: 0;
    } */
    hr {
        opacity: 50%;
        border: 1.2px dashed var(--txt-clr);

    }

    h2 {
        margin-bottom: 1em;
        text-align: center;
        text-shadow: 2px 2px 5px var(--txt-clr);
    }

    ul {
        padding: 0;
        width:auto;
        list-style-type: none;
        margin: 0;
    }

    ul li {
        margin-left: 0;
    }

    /* hr:first-of-type {
        margin: 0;
    } */
</style>