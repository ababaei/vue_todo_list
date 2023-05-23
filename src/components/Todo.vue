<script lang="ts">
import { defineComponent } from 'vue';
import EditTaskForm from './EditTaskForm.vue';

export default defineComponent({
    name: "Todo",
    emits: ["delete-todo"],
    components: {
        EditTaskForm
    },
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed;
        },
        editTask() {
            this.todo.edit = !this.todo.edit;
        }
        taskEdited() {
            this.todo.edit = false;
            this.$emit()
        }
    }
})

</script>

<template>
    <div :class="{ 'completed': todo.completed }" v-if="!todo.edit">
        <input type="checkbox" @click="markComplete">
        {{ todo.title }}
        <button class="btn" @click="editTask"><img src="../assets/pen-fill.svg"></button>
        <button class="btn" @click="$emit('delete-todo', todo.id)" ><img src="../assets/x-circle-fill.svg"></button>
    </div>
    <EditTaskForm v-else :id=todo.id :title=todo.title />
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
        /* filter: invert(100%) sepia(11%) saturate(4931%) hue-rotate(182deg) brightness(99%) contrast(91%); */
        /* filter: invert(92%) sepia(13%) saturate(399%) hue-rotate(95deg) brightness(105%) contrast(105%); */
        filter: invert(89%) sepia(22%) saturate(55%) hue-rotate(117deg) brightness(102%) contrast(106%);
        color: #f0fcf9
    }

    img:hover {
        cursor: pointer;
    }
</style>