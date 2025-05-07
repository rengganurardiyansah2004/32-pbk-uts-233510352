<template>
  <div class="container">
    <h1>List Kegiatan</h1>
    <ul>
      <input v-model="inputBaru" @keyup.enter="tambahKegiatan" placeholder="Tambah kegiatan baru..." /><button @click="tambahKegiatan">Tambah</button>
      <li v-for="(kegiatan, index) in kegiatanList" :key="index">
        <input type="checkbox" v-model="kegiatan.selesai" />
        <span :class="{ selesai: kegiatan.selesai }">{{ kegiatan.nama }}</span>
        <button @click="hapusKegiatan(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const kegiatanList = ref([
  { nama: 'Sarapan pagi', selesai: false },
  { nama: 'lari pagi', selesai: false },
  { nama: 'Makan siang', selesai: false },
  { nama: 'tidur siang', selesai: false },
  { nama: 'Makan malam', selesai: false },
  { nama: 'Tidur', selesai: false }
])

const inputBaru = ref('')

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
