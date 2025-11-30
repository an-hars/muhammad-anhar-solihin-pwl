<script setup>
import { ref } from 'vue'

// 1. STATE (Menggunakan ref)
const newTask = ref('')    // Untuk menampung input user
const tasks = ref([])      // Array untuk menyimpan daftar tugas

// 2. FUNGSI TAMBAH TUGAS
function addTask() {
  // Cek agar tidak memasukkan tugas kosong
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value) // Masukkan ke array
    newTask.value = ''              // Reset input jadi kosong
  }
}

// 3. FUNGSI HAPUS TUGAS
function deleteTask(index) {
  tasks.value.splice(index, 1) // Hapus 1 elemen berdasarkan index
}
</script>

<template>
  <div class="container">
    <h1>To-Do List Anhar</h1>

    <form @submit.prevent="addTask" class="input-group">
      <input 
        v-model="newTask" 
        placeholder="Ketik tugas baru..." 
        class="task-input"
      >
      <button type="submit" class="btn-add">Tambah</button>
    </form>

    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span>{{ task }}</span>
        <button @click="deleteTask(index)" class="btn-delete">Hapus</button>
      </li>
    </ul>

    <p v-if="tasks.length === 0" class="empty-msg">
      Tidak ada tugas. Silahkan tambah tugas baru!
    </p>
  </div>
</template>

<style scoped>
/* CSS Sederhana agar tampilan rapi */
.container {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-family: sans-serif;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  color: #333;
}

.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.task-input {
  flex-grow: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.btn-add {
  padding: 8px 15px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #f9f9f9;
  border-bottom: 1px solid #eee;
  margin-bottom: 5px;
}

.btn-delete {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.empty-msg {
  text-align: center;
  color: #888;
  font-style: italic;
  margin-top: 20px;
}
</style>