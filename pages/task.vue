<template>
  <div class="container">
    <h1 class="title">Tâches à faire</h1>
    <div class="task-input">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Nouvelle tâche" />
      <button @click="addTask">Ajouter</button>
    </div>
    <ul class="task-list">
      <li v-for="task in tasks" :key="task.id" class="task-item">
        <span class="task-name">{{ task.name }}</span>
        <span class="task-points">({{ task.points }} points)</span>
        <button @click="completeTask(task.id)" class="complete-button">Terminer</button>
      </li>
    </ul>

    <h2 class="subtitle">Classement des utilisateurs</h2>
    <ul class="ranking-list">
      <li v-for="(user, index) in ranking" :key="user.id" class="ranking-item">
        <span class="ranking-position">{{ index + 1 }}.</span>
        <span class="user-name">{{ user.name }}</span>
        <span class="user-points">{{ user.points }} points</span>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

interface Task {
  id: number
  name: string
  points: number
}

interface User {
  id: number
  name: string
  points: number
}

const tasks = ref<Task[]>([
  { id: 1, name: 'Faire les courses', points: 5 },
  { id: 2, name: 'Nettoyer la maison', points: 10 },
  { id: 3, name: 'Faire du sport', points: 8 },
])

const users = ref<User[]>([
  { id: 1, name: 'Alice', points: 25 },
  { id: 2, name: 'Bob', points: 30 },
  { id: 3, name: 'Charlie', points: 20 },
])

const newTask = ref('')

const ranking = computed(() => {
  return [...users.value].sort((a, b) => b.points - a.points)
})

const addTask = () => {
  if (newTask.value.trim()) {
    const id = tasks.value.length + 1
    tasks.value.push({
      id,
      name: newTask.value.trim(),
      points: Math.floor(Math.random() * 10) + 1, // Points aléatoires entre 1 et 10
    })
    newTask.value = ''
  }
}

const completeTask = (taskId: number) => {
  const task = tasks.value.find(t => t.id === taskId)
  if (task) {
    const userIndex = Math.floor(Math.random() * users.value.length)
    users.value[userIndex].points += task.points
    tasks.value = tasks.value.filter(t => t.id !== taskId)
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.title {
  color: #2c3e50;
  font-size: 2em;
  margin-bottom: 20px;
}

.subtitle {
  color: #34495e;
  font-size: 1.5em;
  margin-top: 30px;
  margin-bottom: 15px;
}

.task-input {
  display: flex;
  margin-bottom: 20px;
}

.task-input input {
  flex-grow: 1;
  padding: 10px;
  font-size: 1em;
  border: 1px solid #bdc3c7;
  border-radius: 4px 0 0 4px;
}

.task-input button {
  padding: 10px 20px;
  font-size: 1em;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  transition: background-color 0.3s;
}

.task-input button:hover {
  background-color: #2980b9;
}

.task-list, .ranking-list {
  list-style-type: none;
  padding: 0;
}

.task-item, .ranking-item {
  background-color: #ecf0f1;
  margin-bottom: 10px;
  padding: 15px;
  border-radius: 4px;
  display: flex;
  align-items: center;
  transition: background-color 0.3s;
}

.task-item:hover, .ranking-item:hover {
  background-color: #e0e6e8;
}

.task-name, .user-name {
  flex-grow: 1;
}

.task-points, .user-points {
  margin: 0 10px;
  color: #7f8c8d;
}

.complete-button {
  padding: 5px 10px;
  background-color: #2ecc71;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.complete-button:hover {
  background-color: #27ae60;
}

.ranking-position {
  font-weight: bold;
  margin-right: 10px;
  color: #e74c3c;
}
</style>
