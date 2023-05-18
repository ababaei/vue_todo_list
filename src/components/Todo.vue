<script lang="ts">
import { defineComponent } from 'vue';


export default defineComponent({
    name: "Todo",
    emits: ["delete-todo"],
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed;
        }
    }
})

</script>

<template>
    <div :class="{ 'completed': todo.completed }">
        <input type="checkbox" @click="markComplete">
        {{ todo.title }}
        <button class="btn" @click="$emit('delete-todo', todo.id)">X</button>
    </div>
</template>

<style scoped>
    .completed {
        text-decoration: line-through;
    }
</style>