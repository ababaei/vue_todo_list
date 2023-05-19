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
            <input type="text" v-model="title" name="title" required>
            <button class="btn" type="submit">+</button>
        </form>
    </div>
</template>

<style scoped>
    div {
        place-items: center;
    }
</style>