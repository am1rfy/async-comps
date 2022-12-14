<template>
    <h1>{{ msg }}</h1>
</template>

<script>
export default {
    name: 'AsyncComp',
    data() {
        return {
            msg: 'Асинхронный компонент загружен!!!'
        }
    }
}
</script>