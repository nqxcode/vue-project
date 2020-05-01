<template>
    <div>
        <strong>{{ formData.name }}</strong>
        <form v-on:submit.prevent="onSubmit">
            <input type="text" v-model="title">
            <button class="created" type="submit">Create</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: "AddTodo",
        props: ['formData'],
        data() {
            return {
                title: ''
            }
        },
        methods: {
            onSubmit() {
                if (this.title.trim()) {
                    const newTodo = {
                        id: Date.now(),
                        title: this.title,
                        completed: false,
                    }

                    this.$emit('add-todo', newTodo);
                    this.title = '';
                }
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
    }

    input {
        width: 95%;
    }
    button {
        width: 100px
    }
</style>