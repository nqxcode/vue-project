<template>
    <div>
        <h2>Todos</h2>
        <AddTodo
                v-bind:formData="formData"
                v-on:add-todo="addTodo"
        />
        <hr/>
        <TodoList
                v-bind:todos="todos"
                v-on:remove-todo="removeTodo"
        />
    </div>
</template>

<script>
    import AddTodo from '@/components/AddTodo.vue'
    import TodoList from '@/components/TodoList.vue'

    export default {
        name: 'Todos',
        data() {
            return {
                todos: [
                    {id: 1, title: 'Шоколад', completed: false},
                    {id: 2, title: 'Кофе', completed: false},
                    {id: 3, title: 'Торт', completed: false},
                ],
                formData: {
                    name: 'Добавление TODO'
                }
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
                .then(response => response.json())
                .then(json => {
                    console.log(json)
                    this.todos = json
                })
        },
        components: {
            TodoList,
            AddTodo,
        },
        methods: {
            removeTodo(id) {
                this.todos = this.todos.filter(t => t.id !== id)
            },
            addTodo(todo) {
                this.todos.push(todo)
            }
        }
    }
</script>

<style scoped>

</style>