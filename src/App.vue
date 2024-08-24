<template>
  <section class="flex justify-center items-center h-screen flex-col gap-10">
    <h1 class="text-2xl font-extralight uppercase tracking-widest">TodoApp</h1>
    <form class="flex flex-row gap-3" @submit.prevent="onSubmit">
      <input type="text" v-model="taskName" placeholder="Entrez un nom..." class="outline-none px-5 py-3 border tracking-widest font-extralight" />
      <button type="submit" class="px-5 py-3 bg-black text-white font-extralight uppercase tracking-wide">Créer</button>
    </form>
    <div class="text-xl uppercase font-extralight tracking-widest" v-if="tasks.length === 0">Il n'y a aucune tâche inscrite</div>
    <ul>
      <li v-for="task in sortedTasks()" :key="task.date" :class="{ 'line-through': !!task.completed }" class="flex flex-row gap-3 font-extralight text-lg">
        <input type="checkbox" v-model="task.completed" />
        {{ task.title }}
      </li>
    </ul>
  </section>
</template>

<script setup>

import { ref } from 'vue';

const tasks = ref([]);
const taskName = ref('');

const onSubmit = () => {
  if (!taskName.value) return;

  tasks.value.push({
    title: taskName.value,
    completed: false,
    date: Date.now()
  });
  taskName.value = '';
}

const sortedTasks = () => {
  return tasks.value.toSorted((a,b) => a.completed > b.completed ? 1 : -1)
}
</script>