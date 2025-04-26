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

const filteredKegiatan = computed(() => {
  return showUnfinishedOnly.value
    ? kegiatan.value.filter(item => !item.done)
    : kegiatan.value;
});

</script>

<template>


</template>

<style scoped>

</style>