<script lang="ts">
import { defineComponent } from 'vue';
import { v4 as uuid } from 'uuid';
// import uuid from 'uuid';

export default defineComponent({
    name: "AddTodo",
    emits: ["add-todo"],
    data() {
        return {
            title: ""
        }
    },
    methods: {
        addTodo(e: Event) {
            e.preventDefault();
            
            if(this.title === '')
                return;
            
            const newTodoObj: Object = {
                id: uuid(),
                title: this.title,
                completed: false
            }

            this.$emit('add-todo', newTodoObj);
            this.title = '';
        }
    }
})

</script>

<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model.trim="title" name="title" placeholder="Add a new task" required>
            <button class="btn" type="submit">Add</button>
        </form>
    </div>
</template>

<style scoped>
    form {
        display:flex;
        justify-content:center;
        width: 100%;
        gap: 2%;
    }

    input {
        padding-left: 0.5em;
        border-radius: 8px;
        margin: 1em 0;
        width: 80%;
    }

    button {
        font-weight: bold;
        width: 7%;
        min-width: fit-content;
        margin: 1em 0;
        border-radius: 10px;
        transition: all 0.2s ease-in-out;
    }

    button:hover {
        background-color: var(--bg-clr);
        cursor:pointer;
    }
</style>