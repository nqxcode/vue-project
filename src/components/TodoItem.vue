<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input type="checkbox" v-on:change="toggleTodo(todo)"/>
            <strong>{{ index + 1 }} </strong>

            <i>{{ todo.title}}</i>
        </span>
        <button class="rm" v-on:click="removeTodo(todo)">&times;</button>
    </li>
</template>

<script>
    export default {
        name: "TodoItem",
        props: {
            todo: {
                type: Object,
                required: true
            },
            index: {
                type: Number,
                required: true
            }
        },
        methods: {
            toggleTodo(todo) {
                todo.completed = !todo.completed
            },
            removeTodo(todo) {
                this.$emit('remove-todo', todo.id)
            }
        }
    }
</script>

<style scoped>
    li {
        display: flex;
        justify-content: space-between;
        border: 1px solid green;
        padding: 10px;
        margin: 10px;
    }

    input {
        margin-right: 10px;
    }

    .done {
        text-decoration: line-through;
    }

    .rm {
        color:red;
        border-radius: 10px;
    }
</style>