<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: "EditTask",
    emits: ["edit-task", "cancel-edit"],
    props: {
        id: {
            type: Number,
            required: true
        },
        title: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            newTitle: this.label as String
        }
    },
    methods: {
        onSubmit() {
            if (this.newTitle && this.newTitle !== this.title)
        }
    }
})

</script>

<template>
    <div>
        <form @submit="$emit('edit-task')"></form>
    </div>
</template>

<style>

</style>