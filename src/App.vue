<script setup>
import { ref, computed, onMounted, watch } from 'vue';

const kegiatan = ref([
  { nomor: 1, Text: 'praktikum pemograman berbasis komponen', done: true },
  { nomor: 2, Text: 'praktikum pemograman berorientasi objek', done: true },
  { nomor: 3, Text: 'matematika deskrit', done: false }
]);

const aktif = ref("");
const showUnfinishedOnly = ref(false);

const addData = () => {
  const text = aktif.value.trim();
  if (text) {
    kegiatan.value.push({
      nomor: kegiatan.value.length + 1,
      Text: text,
      done: false
    });
    aktif.value = "";
  }
};

const removeItem = (nomor) => {
  kegiatan.value = kegiatan.value.filter(item => item.nomor !== nomor);
};


const filteredKegiatan = computed(() => {
  return showUnfinishedOnly.value
    ? kegiatan.value.filter(item => !item.done)
    : kegiatan.value;
});

onMounted(() => {
  console.log("Component dimuat.");
});

watch(kegiatan, () => {
  console.log("Daftar kegiatan diperbarui.");
}, { deep: true });
</script>

<template>

<div class="container">
    <h1> Daftar Kegiatan - M.IRFAN SAPUTRA</h1>

    <form @submit.prevent="addData" class="form">
      <input v-model="aktif" type="text" placeholder="Tambahkan kegiatan baru..." />
      <button type="submit">Tambah</button>
    </form>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="showUnfinishedOnly" />
        Tampilkan hanya kegiatan yang belum selesai
      </label>
    </div>

    <h2> Kegiatan</h2>
    <ul>
      <li
        v-for="item in filteredKegiatan"
        :key="item.nomor"
        :class="{ selesai: item.done }"
      >
        <input type="checkbox" v-model="item.done" />
        <span>{{ item.nomor }}. {{ item.Text }}</span>
        <button class="hapus" @click="removeItem(item.nomor)">Hapus</button>
      </li>
    </ul>

  </div>



</template>


<style scoped>
 body {
  margin: 0;
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(135deg, #1e1e2f, #2d2d44);
  color: #f0f0f0;
}

.container {
  max-width: 500px;
  margin: 10px auto;
  padding: 150px;
  background: #242438;
  border-radius: 18px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}

h1 {
  text-align: center;
  color: #ffffff;
  margin-bottom: 30px;
}

.form {
  display: flex;
  gap: 12px;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 12px 16px;
  font-size: 16px;
  border: 2px solid #4f46e5;
  border-radius: 10px;
  background: #1a1a2e;
  color: #ffffff;
  transition: 0.3s ease;
}

input[type="text"]:focus {
  outline: none;
  border-color: #818cf8;
  background: #2c2c3e;
}

button {
  padding: 12px 18px;
  background-color: #6366f1;
  color: white;
  border: none;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #4f46e5;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background: #1e1e2f;
  border: 1px solid #3b3b52;
  padding: 14px 16px;
  margin-bottom: 12px;
  border-radius: 10px;
  display: flex;
  align-items: center;
}

li:hover {
  background: #292942;
}

li.selesai span {
  text-decoration: line-through;
  color: #a0aec0;
}

span {
  flex: 1;
  margin-left: 10px;
  font-size: 16px;
  color: #f0f0f0;
}

.hapus {
  background-color: #ef4444;
  border: none;
  color: white;
  padding: 8px 12px;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.hapus:hover {
  background-color: #dc2626;
}

.filter {
  margin-bottom: 20px;
  font-size: 15px;
  color: #e2e8f0;
  display: flex;
  align-items: center;
}

.filter input[type="checkbox"] {
  margin-right: 8px;
}

</style>