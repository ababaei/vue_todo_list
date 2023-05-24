<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: "EditTask",
    emits: ["edit-task", "cancel-edit"],
    props: {
        id: {
            type: String,
            required: true
        },
        title: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            newTitle: this.title
        }
    },
    methods: {
        onSubmit() {
            if (this.newTitle && this.newTitle !== this.title)
            {
                this.$emit("edit-task", this.newTitle);
            }
            else if (this.newTitle === this.title)
                this.$emit("cancel-edit");
        },
        onCancel() {
            this.$emit("cancel-edit");
        }
    }
})

</script>

<template>
    <form @submit.prevent="onSubmit">
        <div>
            <input :id="id" type="text" v-model.lazy.trim="newTitle">
            <button type="submit" class="btn"><img src="../assets/check-circle-fill.svg"></button>
            <button type="button" class="btn" @click="onCancel"><img src="../assets/x-circle-fill.svg"></button>
        </div>
    </form>
</template>

<style scoped>
    form {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }

    input {
        padding-left: 0.5em;
        border-radius: 8px;
        word-wrap: normal;
    }

    div {
        margin: 0 5%;
    }
</style>