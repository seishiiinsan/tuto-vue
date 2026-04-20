<script setup>
    import { computed, onMounted, ref } from 'vue';
    import Checkbox from './Checkbox.vue';
    import Timer from './Timer.vue';


    const showTimer = ref(true);
    const hideCompleted = ref(false);
    const todos = ref([]);
    const newTodo = ref('');

    onMounted(() => {
        fetch('https://jsonplaceholder.typicode.com/todos')
            .then(r => r.json())
            .then(v => todos.value = v.map(todo => ({...todo, date: todo.id})));
    })

    const addTodo = () => {
        todos.value.push({
            title: newTodo.value,
            completed: false,
            date: Date.now()
        })
        newTodo.value = '';
    }

    const sortedTodos = computed(() => {
        const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1);
        if (hideCompleted.value === true) {
            return sortedTodos.filter(todo => !todo.completed);
        }

        return sortedTodos;
    })

    const remainingTodos = computed(() => {
        return todos.value.filter(todo => !todo.completed).length;
    })
</script>

<template>
    <button @click="showTimer = !showTimer">Afficher / Masquer le timer</button>
    <Timer v-if="showTimer"></Timer>
 
    <form action="" @submit.prevent="addTodo">
        <fieldset role="group">
            <input type="text" placeholder="Tâche à effectuer" v-model="newTodo" />
            <button :disabled="newTodo.length == 0">Ajouter</button>
        </fieldset>
    </form>

    <div v-if="todos.length == 0">Vous n'avez pas de tâches à faire 🎉</div>

    <div v-else>
        <ul>
            <li :key="todo.date" v-for="todo in sortedTodos" style="display: flex; align-items: center; gap: 0.5rem;">
                <Checkbox :label="todo.title" v-model="todo.completed" />
            </li>
        </ul>

        <div>
            <label for="">
                <input type="checkbox" v-model="hideCompleted">
                Masquer les tâches terminées
            </label>

            <p v-if="todos.filter(todo => !todo.completed).length > 0">
                {{ remainingTodos }} {{ remainingTodos === 1 ? 'tâche restante' : 'tâches restantes' }}
            </p>
        </div>
    </div>

</template>