<template>
    <div class="flex-container">
        <AsyncComp v-if="asyncCompLoaded"/>
        <h1 v-else>Асинхронный компонент пока не нужон)</h1>

        <button
            @click="this.asyncCompLoaded = !this.asyncCompLoaded"
            class="show-btn"
        >
            Show
        </button>
    </div>
</template>

<script>
import LoadingComp from './components/LoadingComp.vue'
import ErrorComp from './components/ErrorComp.vue'

import { defineAsyncComponent } from 'vue'
import asyncComp from "./components/AsyncComp.vue";

const loadAsyncCompWithDelay = ({ path, delay }) => new Promise((resolve, reject) => {
    setTimeout(() => {
        import(path)
            .then(data => resolve(data))
    }, delay)
})

const AsyncComp = defineAsyncComponent({
    loader: () => loadAsyncCompWithDelay({
        path: './components/AsyncComp.vue',
        delay: 3000,
    }),
    loadingComponent: LoadingComp,
    errorComponent: ErrorComp,
    delay: 0,
    timeout: 1000
})

export default {
    components: { AsyncComp },
    data() {
        return {
            asyncCompLoaded: false
        }
    },
}
</script>

<style>
#app {
    width: 100vw;
    height: 100vh;

    display: flex;
    justify-content: center;
    align-items: center;
}
.flex-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.show-btn {
    margin-top: 5vh;
    padding: 10px 15px;
}
</style>
