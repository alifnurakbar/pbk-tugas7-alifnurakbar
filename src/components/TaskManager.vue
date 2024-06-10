<template>
    <div id="task-manager">
      <h1>Top Up Game Task Manager</h1>
      <div class="input-group">
        <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambahkan tugas baru" />
        <button @click="addTask">Tambah</button>
      </div>
      <ul>
        <li v-for="task in tasks" :key="task.id" :class="{ completed: task.completed }">
          <span @click="toggleTaskCompletion(task.id)">{{ task.text }}</span>
          <button @click="removeTask(task.id)">Hapus</button>
        </li>
      </ul>
      <p>Jumlah tugas yang belum selesai: {{ incompleteTasksCount }}</p>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  import { useTaskStore } from '../stores/taskStore'
  
  export default {
    setup() {
      const newTask = ref('')
      const taskStore = useTaskStore()
  
      const addTask = () => {
        if (newTask.value.trim()) {
          taskStore.addTask(newTask.value)
          newTask.value = ''
        }
      }
  
      return {
        newTask,
        tasks: taskStore.tasks,
        incompleteTasksCount: taskStore.incompleteTasksCount,
        addTask,
        removeTask: taskStore.removeTask,
        toggleTaskCompletion: taskStore.toggleTaskCompletion
      }
    }
  }
  </script>
  
  <style scoped>
  #task-manager {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    background-color: #f9f9f9;
  }
  
  h1 {
    text-align: center;
    margin-bottom: 20px;
  }
  
  .input-group {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    background-color: #28a745;
    color: white;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #218838;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: flex;
    justify-content: space-between;
    padding: 10px;
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-bottom: 10px;
  }
  
  li.completed span {
    text-decoration: line-through;
    color: #999;
  }
  
  li span {
    cursor: pointer;
    flex-grow: 1;
  }
  
  li button {
    background-color: #dc3545;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  li button:hover {
    background-color: #c82333;
  }
  
  p {
    text-align: center;
    font-weight: bold;
  }
  </style>
  