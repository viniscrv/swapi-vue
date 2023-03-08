<template>
    <header>
        <h1>Star Wars Universe</h1>
        <input type="text" placeholder="Pesquisar personagens" />
    </header>
    <div>
        <slot />
    </div>
</template>

<style scoped>
    header {
        width: 100vw;
        background-color: #121214;
        padding: 2rem 6rem;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-bottom: 2px solid #505059;
    }

    input {
        background-color: #29292E;
        border: 2px solid #505059;
        border-radius: 6px;
        padding: 1rem;
        color: #cdcdcd;
        width: 300px;
    }
</style>