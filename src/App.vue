<script setup>
import { onMounted, provide, ref, watch } from 'vue';

import PaneRight from './components/PaneRight.vue';
import PaneLeft from './components/PaneLeft.vue';
import { cityProvide, API_ENDPOINT } from './constats';

const data = ref();
const error = ref();
const activeIndex = ref(0);
const city = ref('Москва');
provide(cityProvide, city);

async function getCity(city) {
  const params = new URLSearchParams({
    key: '680d9725a8fc4d05883172604252506',
    lang: 'ru',
    q: city,
    days: 3,
  });

  const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`);

  if (res.status !== 200) {
    error.value = await res.json();
    data.value = null;
    return;
  }

  error.value = null;
  data.value = await res.json();

  // console.log(data.value);
}
watch(city, () => {
  getCity(city.value);
});
onMounted(() => getCity(city.value));
</script>

<template>
  <main class="main">
    <PaneLeft />
    <PaneRight
      :data="data"
      :error="error"
      :active-index="activeIndex"
      @select-index="(i) => (activeIndex = i)"
    />
  </main>
</template>

<style scoped>
.main {
  display: grid;
  grid-template-columns: minmax(493px, 1fr) 1fr;
  align-items: center;
}
</style>
