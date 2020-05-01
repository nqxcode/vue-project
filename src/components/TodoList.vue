<template>
    <div>
        <ul>
            <TodoItem
                v-for="(todo, i) in todos"
                v-bind:todo="todo"
                v-bind:index="i"
                v-on:remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
    import TodoItem from "@/components/TodoItem.vue";
    export default {
        name: "Todo",
        props: ['todos'],
        components: {
            TodoItem
        },
        methods: {
            removeTodo(id) {
                this.$emit('remove-todo', id);
            }
        }
    }
</script>

<style scoped>
    ul {
        list-style: none;
        padding: 10px;
    }
</style>