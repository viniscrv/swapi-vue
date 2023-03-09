<template>
    <header>
        <NuxtLink to="/"><h1>Star Wars Universe</h1></NuxtLink>
        <input type="text" placeholder="Pesquisar personagens" disabled />
    </header>
    <div>
        <slot />
    </div>
</template>

<style scoped lang="scss">

header {
    width: 100vw;
    background-color: #121214;
    padding: 2rem 6rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 2px solid #505059;

    input {
        background-color: #29292e;
        border: 2px solid #505059;
        border-radius: 6px;
        padding: 1rem;
        color: #cdcdcd;
        width: 300px;

        &:disabled {
            cursor: not-allowed;
        }
    }
    a {
        text-decoration: none;
        color: #cdcdcd;
    }
}
</style>
