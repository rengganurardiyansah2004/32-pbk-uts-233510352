<template>
  <div class="container">
    <h1>List Kegiatan</h1>
    <label>
    <input type="checkbox" v-model="tampilkanYangBelumSelesai" />Hanya tampilkan yang belum selesai</label>
    <ul>
      <input v-model="inputBaru" @keyup.enter="tambahKegiatan" placeholder="Tambah kegiatan baru..." /><button @click="tambahKegiatan">Tambah</button>
      <li v-for="(kegiatan, index) in kegiatanYangDitampilkan" :key="index">
        <input type="checkbox" v-model="kegiatan.selesai" />
        <span :class="{ selesai: kegiatan.selesai }">{{ kegiatan.nama }}</span>
        <button @click="hapusKegiatan(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const kegiatanList = ref([
  { nama: 'Belajar Vue', selesai: false },
  { nama: 'Ngoding Project', selesai: false }
])

const tampilkanYangBelumSelesai = ref(false)

const kegiatanYangDitampilkan = computed(() => {
  return tampilkanYangBelumSelesai.value
    ? kegiatanList.value.filter(k => !k.selesai)
    : kegiatanList.value
})


function tambahKegiatan() {
  if (inputBaru.value.trim() !== '') {
    kegiatanList.value.push({ nama: inputBaru.value, selesai: false })
    inputBaru.value = ''
  }
}

function hapusKegiatan(index) {
  kegiatanList.value.splice(index, 1)
}
</script>

<style>
.container {
  max-width: 600px;
  margin: auto;
  font-family: sans-serif;
}

.selesai {
  text-decoration: line-through;
  color: gray;
}

</style>
