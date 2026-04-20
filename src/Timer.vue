<script setup>
    import { onUnmounted, onMounted, ref } from 'vue';

    const time = ref(0);
    const size = ref({width: 0, height: 0});
    const div = ref(null);

    let timer;
    onMounted(() => {
        const rect = div.value.getBoundingClientRect();
        size.value = {width: rect.width, height: rect.height};
        timer = setInterval(() => {
            console.log("increment");
            time.value++;
        }, 1000);
    })

    onUnmounted(() => {
        clearInterval(timer);
    })
</script>

<template>
    <div ref="div">
        Temps : {{ time }}
        <br> <br>
        Largeur : {{ size.width }}px
        <br>
        Hauteur : {{ size.height }}px
    </div>
</template>