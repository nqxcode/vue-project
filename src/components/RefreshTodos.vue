<template>
    <div>
        <button v-on:click="refreshTodos">Refresh</button>
    </div>
</template>

<script>
    export default {
        name: "RefreshTodos",
        methods: {
            refreshTodos() {
                this.$emit('refresh-todos');
            }
        }
    }
</script>

<style scoped>
    div {
        display: flex;
        justify-content: right;
    }
</style>