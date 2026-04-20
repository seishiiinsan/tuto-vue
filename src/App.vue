<script setup>
    import { ref, watch, watchEffect } from 'vue'
    import { useTimer } from './composable/useTimer'
    
    const page = ref({
        title: ''
    })

    const { time, reset } = useTimer()

    watchEffect(() => {
        document.title = page.value.title
    })
</script>

<template>
    <input type="text" v-model="page.title">
    Temps écoulé : {{ time }}
    <button @click="reset">RESET</button>
</template>