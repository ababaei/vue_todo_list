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
        <button class="btn" @click="$emit('delete-todo', todo.id)" ><img src="../assets/x-circle-fill.svg"></button>
    </div>
</template>

<style scoped>
    .completed {
        text-decoration: line-through;
    }

    div {
        word-break: break-all;  
        text-align: justify;
        margin: 0 5%;
    }

    button {
        vertical-align: middle;
    }

    img {
        filter: invert(100%) sepia(11%) saturate(4931%) hue-rotate(182deg) brightness(99%) contrast(91%);
        color: #e8e4f1
    }
</style>