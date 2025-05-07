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
  { nama: 'sarapan', selesai: false },
  { nama: 'lari pagi', selesai: false },
  { nama: 'makan siang', selesai: false },
  { nama: 'tidur siang', selesai: false },
  { nama: 'makan malam', selesai: false },
  { nama: 'tidur', selesai: false },
])

const tampilkanYangBelumSelesai = ref(false)
const inputBaru = ref('')

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
* {
  box-sizing: border-box;
}

body {
  background-color: #e6edff;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 20px;
}

.container {
  background: white;
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  position: relative;
}

h1 {
  background-color: #a855f7;
  color: white;
  padding: 15px;
  text-align: center;
  border-radius: 8px 8px 0 0;
  margin: -20px -20px 20px -20px;
  font-size: 20px;
}

label {
  display: block;
  margin-bottom: 15px;
  color: #555;
  font-size: 14px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

ul > input[type="text"] {
  width: calc(100% - 100px);
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px 0 0 8px;
  outline: none;
}

ul > button {
  width: 100px;
  padding: 10px;
  border: none;
  background-color: #a855f7;
  color: white;
  font-weight: bold;
  border-radius: 0 8px 8px 0;
  cursor: pointer;
}

ul > button:hover {
  background-color: #9333ea;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #f8f8ff;
  padding: 10px 15px;
  margin-bottom: 10px;
  border-radius: 8px;
}

li input[type="checkbox"] {
  margin-right: 10px;
}

li span {
  flex: 1;
  color: #333;
  font-size: 14px;
}

li span.selesai {
  text-decoration: line-through;
  color: #aaa;
}

li button {
  background: none;
  border: none;
  color: #999;
  cursor: pointer;
  font-size: 16px;
}

li button:hover {
  color: red;
}
</style>