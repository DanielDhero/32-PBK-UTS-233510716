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

</style>