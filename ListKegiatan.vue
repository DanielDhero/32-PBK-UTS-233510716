<script setup>
import { ref, computed } from 'vue'

const listbaru = ref('')
const tugas = ref([])
const filter = ref('all')

function tambahlist() {
  if (listbaru.value.trim()) {
    tugas.value.push({ text: listbaru.value, done: false })
    listbaru.value = ''
  }
}

function hapusTugas(Tugas) {
  const index = tugas.value.indexOf(Tugas)
  if (index !== -1) {
    tugas.value.splice(index, 1)
  }
}

const filteredTasks = computed(() => {
  if (filter.value === 'done') return tugas.value.filter(t => t.done)
  if (filter.value === 'undone') return tugas.value.filter(t => !t.done)
  return tugas.value
})

</script>

<template>
  <div class="container">

    <h1 class="judul">List Kegiatan</h1>

    <div class="inputList">
      <input
        v-model="listbaru"
        @keyup.enter="tambahlist"
        class="inputKegiatan"
        placeholder="Tambahkan kegiatan..."
      />
      <button @click="tambahlist" class="addButton">Tambah</button>
    </div>

    <div class="filterTabel">
      <label>Filter:</label>
      <select v-model="filter" class="filter">
        <option value="semua">Semua</option>
        <option value="done">Selesai</option>
        <option value="undone">Belum selesai</option>
      </select>
    </div>

    <ul class="task-list">
      <li
        v-for="(Tugas, index) in filteredTasks"
        :key="index"
        class="task-item"
      >
        <div class="task-left">
          <input type="checkbox" v-model="Tugas.done" />
          <span :class="{ done: Tugas.done }">{{ Tugas.text }}</span>
        </div>
        <button @click="hapusTugas(Tugas)" class="delete-button">Batal</button>
      </li>
    </ul>

  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap');


body {
  margin: 0;
  padding: 0;
  background-color: #1e1e2f;
  color: #e0e0e0;
}

.container {
  max-width: 600px;
  margin: 50px auto;
  background-color: #2c2c3a;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.3);
}

.inputList {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.inputKegiatan {
  flex: 1;
  padding: 10px;
  font-size: 15px;
  border: 1px solid #444;
  border-radius: 6px;
  background-color: #1a1a26;
  color: #e0e0e0;
  font-family: 'Poppins', sans-serif;
}

.inputKegiatan:focus {
  border-color: #5831b4;
  outline: none;
}

.addButton {
  font-family: 'Poppins', sans-serif;
}

.addButton:hover {
  background-color: #5831b4;
}

.filterTabel {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.filter {
  padding: 6px 10px;
  font-size: 14px;
  background-color: #1a1a26;
  color: #e0e0e0;
  border: 1px solid #444;
  border-radius: 6px;
  font-family: 'Poppins', sans-serif;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #1a1a26;
  padding: 10px 14px;
  border-radius: 6px;
  margin-bottom: 10px;
  border: 1px solid #333;
  font-family: 'Poppins', sans-serif;
}

.task-left {
  display: flex;
  align-items: center;
  gap: 10px;
}

.task-left input[type='checkbox'] {
  transform: scale(1.2);
  accent-color: #4a90e2;
}

.task-left span {
  font-size: 15px;
  color: #e0e0e0;
  transition: color 0.2s, text-decoration 0.2s;
}

.task-left span.done {
  text-decoration: line-through;
  color: #888;
}

.delete-button {
  background: none;
  border: none;
  color: #e57373;
  font-size: 14px;
  font-weight: 500;
  font-family: 'Poppins', sans-serif;
  cursor: pointer;
  transition: color 0.2s;
}

.delete-button:hover {
  color: #f44336;
}

</style>