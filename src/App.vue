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

const toggle = (tugas) => {
  tugas.selesai == !tugas.selesai
  console.log(tugas.selesai)
}

const hapusTugas = (t) => {
  tugas.value = tugas.value.filter(tugas => tugas.id !== t.id)
}

</script>

<template>
  <input type="text" v-model="tugasBaru" @keyup.enter="tambahTugas">
  <button @click="tambahTugas">Tambah Tugas</button>

  <ul>
    <li v-for="t in tugas" :key="tugas.id">
      <input type="checkbox" v-model="t.selesai" @change="toggle(t)" :checked="t.selesai">
      {{ t.nama }}
      <button @click="hapusTugas(t)">Hapus</button>
    </li>
  </ul>
</template>

<style scoped></style>
