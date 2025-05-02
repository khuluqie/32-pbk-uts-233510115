<script setup>
import { ref } from 'vue';

const tugas = ref([])
const tugasBaru = ref('')

const tambahTugas = () => {
  tugas.value.push({
    id: tugas.value.length + 1,
    nama: tugasBaru.value,
    selesai: false
  })
  tugasBaru.value = ''
  console.log(tugas.value)
}
</script>

<template>
  <input type="text" v-model="tugasBaru" @keyup.enter="tambahTugas">
  <button @click="tambahTugas">Tambah Tugas</button>

  <ul>
    <li v-for="t in tugas" :key="tugas.id">
      {{ t.nama }}
    </li>
  </ul>
</template>

<style scoped></style>
