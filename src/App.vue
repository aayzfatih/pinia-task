<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia Tasks</h1>
    </header>
    <!-- New Task Form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!-- loading -->

    <div class="loading" v-if="taskStore.isLoading">Loading Tasks</div>
    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All task</button>
      <button @click="filter = 'favs'">Fav task</button>
    </nav>

    <!-- task list -->
    <div v-if="filter === 'all'" class="task-list">
      <p>You have {{ taskStore.totalCount }} task left to do</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div v-else-if="filter === 'favs'" class="task-list">
      <p>You have {{ taskStore.favCount }} favs left to do</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>

  </main>
</template>

<script setup>
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';
import { useTaskStore } from './stores/TaskStore';
import { ref } from 'vue'
const taskStore = useTaskStore()

//fetch tasks
taskStore.getTasks();

const filter = ref("all")
</script>

<style lang="scss" scoped></style>