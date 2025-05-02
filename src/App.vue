<script setup>
import { ref, computed } from 'vue';

const tugas = ref([])
const tugasBaru = ref('')
const filter = ref('semua')

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

const filterTugas = computed(() => {
  if (filter.value === 'selesai') {
    return tugas.value.filter(t => t.selesai)
  } else if (filter.value === 'belum selesai') {
    return tugas.value.filter(t => !t.selesai)
  } else {
    return tugas.value
  }
})

</script>

<template>
  <input type="text" v-model="tugasBaru" @keyup.enter="tambahTugas">
  <button @click="tambahTugas">Tambah Tugas</button>
  <div>
    <button @click="filter = 'semua'">Semua</button>
    <button @click="filter = 'selesai'">Selesai</button>
    <button @click="filter = 'belum selesai'">Belum Selesai</button>
  </div>
  <ul>
    <li v-for="t in filterTugas" :key="tugas.id">
      <input type="checkbox" v-model="t.selesai" @change="toggle(t)" :checked="t.selesai">
      {{ t.nama }}
      <button @click="hapusTugas(t)">Hapus</button>
    </li>
  </ul>
</template>

<style scoped></style>
