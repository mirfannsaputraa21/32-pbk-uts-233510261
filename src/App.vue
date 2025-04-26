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

</style>