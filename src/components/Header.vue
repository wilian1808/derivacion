<template>
    <header class="header">
        <div class="header__content">
            <a href="/" class="header__title">Diferenciación numérica</a>
            <a href="https://github.com/wilian1808/derivacion" class="header__link" blank>GitHub</a>
        </div>
    </header>
</template>

<script>
export default {
    name: 'Header',
}
</script>

<style scoped>

.header {
    display: block;
    width: 100%;
    background-color: #232425;
}

.header__content {
    margin: 0 auto 0;
    padding: 1.4em 0;
    width: 92%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.header__title,
.header__link {
    display: block;
    color: #eeeeee;
    text-decoration: none;
    cursor: pointer;
    font-size: 16px;
    font-weight: 700;
    letter-spacing: .5px;
}

</style>