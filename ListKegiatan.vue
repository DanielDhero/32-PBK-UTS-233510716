<script setup>
import { ref, computed } from 'vue'

const listbaru = ref('')
const tugas = ref([])
const filter = ref('all')

function tambahTugas() {
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
      <button @click="addTask" class="addButton">Tambah</button>
    </div>

    <div class="filterTabel">
      <label>Filter:</label>
      <select v-model="filter" class="filter">
        <option value="semua">Semua</option>
        <option value="done">Selesai</option>
        <option value="undone">Belum selesai</option>
      </select>
    </div>

  </div>
</template>

<style scoped>
</style>