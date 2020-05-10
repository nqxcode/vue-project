<template>
    <div>
        <h2>Todos</h2>
        <p>Поиск: <a target="_blank" v-bind:href="searchUrl">{{ searchUrl }}</a></p>
        <p>Поиск: <span v-html="searchLink"></span></p>

        <AddTodo
                v-bind:formData="formData"
                v-on:add-todo="addTodo"
        />
        <hr/>

        <RefreshTodos v-on:refresh-todos="refreshTodos"></RefreshTodos>
        <hr/>

        <Loader v-if="loading"/>
        <TodoList
                v-else-if="todos.length"
                v-bind:todos="todos"
                v-on:remove-todo="removeTodo"
        />
        <p v-if="!todos.length">No Todos!</p>
    </div>
</template>

<script>
    import RefreshTodos from '@/components/RefreshTodos.vue'
    import Loader from '@/components/Loader.vue'
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
                },
                loading: false,
                searchUrl: 'http://www.google.com',
                searchLink: "<a target='_blank' href='http://www.google.com'>www.google.com</a>"
            }
        },
        mounted() {
            this.refreshTodos();
        },
        components: {
            TodoList,
            AddTodo,
            Loader,
            RefreshTodos,
        },
        methods: {
            removeTodo(id) {
                this.todos = this.todos.filter(t => t.id !== id)
            },
            addTodo(todo) {
                this.todos.push(todo)
            },
            refreshTodos() {
                this.loading = true;
                fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
                    .then(response => {
                        return response.json();
                    })
                    .then(json => {
                        var self = this;
                        setTimeout(function() {
                            self.todos = json
                            self.loading = false;
                        }, 500)
                    })
            }
        }
    }
</script>

<style scoped>

</style>