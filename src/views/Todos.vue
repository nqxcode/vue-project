<template>
    <div>
        <h2>Todos</h2>
        <hr/>
        <p>Поиск: <a target="_blank" v-bind:href="searchUrl">{{ searchUrl }}</a></p>
        <p>Поиск: <span v-html="searchLink" v-on:click.prevent=""></span></p>
        <hr/>

        <p>Счетчик {{ counter }}</p>
        <button v-on:click="incrementCounter(1, $event)"> Увеличить счетчик</button>
        <hr/>

        <span v-on:mousemove="handleMouseMove">X: {{ x }} Y: {{ y}} <span v-on:mousemove.stop="">Not change</span></span>
        <hr/>

        <input type="text" v-on:keyup.enter.space="alertValue" />

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
                searchLink: "<a target='_blank' href='http://www.google.com'>www.google.com</a>",
                counter: 0,
                x: 0,
                y: 0,
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
                        setTimeout(function () {
                            self.todos = json
                            self.loading = false;
                        }, 500)
                    })
            },
            incrementCounter(num, event) {
                this.counter += num;
                event.target.style.color = this.counter > 0 && this.counter < 5 ? 'red' : 'blue';
            },
            handleMouseMove(event) {
                this.x = event.clientX;
                this.y = event.clientY;
            },
            alertValue(event) {
                alert(event.target.value)
            }
        }
    }
</script>

<style scoped>

</style>