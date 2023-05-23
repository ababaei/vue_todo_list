<script lang="ts">
import { defineComponent } from 'vue';
// import uuid from 'uuid';

export default defineComponent({
    name: "AddTodo",
    data() {
        return {
            title: ""
        }
    },
    emits: ["add-todo"],
    methods: {
        addTodo(e: Event) {
            e.preventDefault();

            const newTodoObj: Object = {
                id: this.todosLen + 1,
                title: this.title,
                completed: false
            }

            this.$emit('add-todo', newTodoObj);
            this.title = '';
        }
    },
    props: {
        todosLen: {
            type: Number,
            required: true
        }
    }
})

</script>

<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add a new task" required>
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
        padding-left: 1em;
        border-radius: 8px;
        margin: 1em 0;
        width: 80%;
    }

    button {
        font-weight: bold;
        width: 7%;
        margin: 1em 0;
        border-radius: 10px;
        transition: all 0.5s linear;
    }

    button:hover {
        background-color: var(--bg-clr);
    }
</style>