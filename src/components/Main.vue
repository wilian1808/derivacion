<template>
    <main class="main">
        <div class="main__content">
            <h1 class="main__title">Diferenciación numérica</h1>
            <p class="main__subtitle">o derivacion numérica</p>
        </div>
    </main>
</template>

<script>
export default {
    name: 'Main'
}
</script>

<style scoped>
.main {
    display: block;
    width: 100%;
    background-color: #25c2a0;
    padding: 3em;
    display: flex;
    justify-content: center;
    align-items: center;
}

.main__content {
    text-align: center;
}

.main__title {
    color: #000000;
    font-size: 3rem;
    font-weight: bold;
}

.main__subtitle {
    padding: 1em 0 0 0;
    font-size: 1.5rem;
}
</style>