<template>
    <div>
        <h1>Home page</h1>

        <RouterLink :to="{ name: 'todos'}">Todos</RouterLink>
    </div>
</template>

<script>
    export default {
        name: "Home"
    }
</script>

<style scoped>

</style>