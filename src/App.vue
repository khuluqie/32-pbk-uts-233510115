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
}

const toggle = (tugas) => {
  tugas.selesai == !tugas.selesai
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
  <div class="w-screen h-screen bg-gradient-to-br from-slate-900 to-slate-800 text-white flex items-center justify-center">
    <div class="w-full max-w-xl h-[90vh] bg-slate-950 rounded-xl shadow-xl p-6 flex flex-col">

      <div class="flex items-center gap-2 mb-4">
        <input
          type="text"
          v-model="tugasBaru"
          @keyup.enter="tambahTugas"
          placeholder="Tambah tugas baru..."
          class="flex-1 px-4 py-2 rounded-lg bg-slate-800 text-white focus:outline-none focus:ring-2 focus:ring-cyan-400 transition"
        />
        <button
          @click="tambahTugas"
          class="bg-cyan-600 hover:bg-cyan-500 text-white px-4 py-2 rounded-lg transition"
        >
          Tambah
        </button>
      </div>

      <div class="flex justify-center gap-3 mb-4">
        <button
          @click="filter = 'semua'"
          :class="[
            'px-3 py-1 rounded-full transition font-semibold',
            filter === 'semua' ? 'bg-cyan-500 text-white' : 'bg-slate-700 hover:bg-slate-600 text-gray-300'
          ]"
        >
          Semua
        </button>
        <button
          @click="filter = 'selesai'"
          :class="[
            'px-3 py-1 rounded-full transition font-semibold',
            filter === 'selesai' ? 'bg-cyan-500 text-white' : 'bg-slate-700 hover:bg-slate-600 text-gray-300'
          ]"
        >
          Selesai
        </button>
        <button
          @click="filter = 'belum selesai'"
          :class="[
            'px-3 py-1 rounded-full transition font-semibold',
            filter === 'belum selesai' ? 'bg-cyan-500 text-white' : 'bg-slate-700 hover:bg-slate-600 text-gray-300'
          ]"
        >
          Belum Selesai
        </button>
      </div>

      <div class="flex-1 overflow-y-auto scrollbar-thin scrollbar-thumb-cyan-600 scrollbar-track-slate-700 rounded-md p-2 space-y-2 bg-slate-800">
        <transition-group name="list" tag="ul">
          <li
            v-for="t in filterTugas"
            :key="t.id"
            class="flex items-center justify-between bg-slate-950 rounded-lg mt-2 px-4 py-5 hover:bg-slate-700 transition duration-200"
          >
            <div class="flex items-center gap-2">
              <input type="checkbox" v-model="t.selesai" @change="toggle(t)" />
              <span :class="{'line-through text-gray-400': t.selesai}">{{ t.nama }}</span>
            </div>
            <button
              @click="hapusTugas(t)"
              class="text-sm bg-red-500 hover:bg-red-600 text-white px-2 py-1 rounded-lg transition"
            >
              Hapus
            </button>
          </li>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<style scoped>
.list-enter-active, .list-leave-active {
  transition: all 0.3s ease;
}
.list-enter-from {
  opacity: 0;
  transform: translateY(10px);
}
.list-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.scrollbar-thin::-webkit-scrollbar {
  width: 6px;
}
.scrollbar-thin::-webkit-scrollbar-thumb {
  border-radius: 8px;
}
</style>