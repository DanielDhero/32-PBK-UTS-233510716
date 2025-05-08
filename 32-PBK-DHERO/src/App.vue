<script setup>
import { ref, computed } from 'vue'
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

  </div>
</template>

<style scoped>
</style>