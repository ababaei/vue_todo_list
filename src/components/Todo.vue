<script lang="ts">
import { defineComponent } from 'vue';
import EditTaskForm from './EditTaskForm.vue';

export default defineComponent({
    name: "Todo",
    emits: ["delete-todo", "edit-task"],
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
        },
        taskEdited(newTitle: String) {
            this.todo.edit = false;
            this.$emit("edit-task", newTitle);
        }
    },
    computed: {
        isCompleted() {
            return this.todo.completed
        }
    }
})

</script>

<template>
    <div :class="{ completed: todo.completed }" v-if="!todo.edit">
        <input type="checkbox" v-model="isCompleted" @change="markComplete">
        {{ todo.title }}
        <button class="btn" @click="editTask"><img src="../assets/pen-fill.svg"></button>
        <button class="btn" @click="$emit('delete-todo', todo.id)" ><img src="../assets/x-circle-fill.svg"></button>
    </div>
    <EditTaskForm v-else :id=todo.id :title=todo.title
        @edit-task="taskEdited"
        @cancel-edit="editTask"
    />
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

    button, :deep(button) {
        vertical-align: middle;
    }

    img, :deep(img) {
        filter: invert(89%) sepia(22%) saturate(55%) hue-rotate(117deg) brightness(102%) contrast(106%);
        color: #f0fcf9
    }

    img:hover, :deep(img) {
        cursor: pointer;
    }
</style>