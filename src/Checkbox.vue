<script setup>
    const model = defineModel({
        type: Boolean,
        required: true
    })

    defineProps({
        label: String
    })

    const emits = defineEmits(['check', 'uncheck'])
    const onChange = (event) => {
        if (event.currentTarget.checked) {
            emits('check', event.currentTarget);
        } else {
            emits('uncheck', event.currentTarget);
        }
    }
</script>

<template>
    <label>
        <input type="checkbox" v-model="model" />
        {{ label }}
    </label>
</template>