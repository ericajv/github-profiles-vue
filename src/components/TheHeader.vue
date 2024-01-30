<script>
import Toggle from './Toggle.vue'
export default {
    components: { Toggle }
}
</script>

<template>
    <header class="header">
        <div class="logo">
            <img src="../../public/github.svg" alt="icon github">
            <h1>GitHub Profiles</h1>
        </div>
        <Toggle />
    </header>
</template>

<style>
.header {
    background-color: var(--background-color-primary);
    color: #a49df9;
    padding: 1rem 2rem;
    border-bottom: 1px solid#5563ac;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.logo {
    display: flex;
    align-items: center;
    gap: 2rem;
}
</style>