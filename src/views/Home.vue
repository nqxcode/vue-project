<template>
    <div>
        <h1>Home page</h1>
        <p>Lorem...</p>
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