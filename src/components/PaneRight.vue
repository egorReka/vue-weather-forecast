<script setup>
import { computed } from 'vue';

import Stat from '../components/Stat.vue';
import ChangeCity from '../components/ChangeCity.vue';
import DayCard from '../components/DayCard.vue';
import { errorMap } from '../constats';

const { data, error, activeIndex } = defineProps({
  error: Object,
  data: Object,
  activeIndex: Number,
});

const emit = defineEmits(['select-index', 'select-city']);

const statData = computed(() => {
  if (!data) {
    return [];
  }

  return [
    {
      label: 'Влажность',
      stat: data.current.humidity + ' %',
    },
    {
      label: 'Облачность',
      stat: data.current.cloud + ' %',
    },
    {
      label: 'Ветер',
      stat: data.current.wind_kph + ' км/ч',
    },
  ];
});

const errorDisplay = computed(() => {
  return errorMap.get(error?.error?.code);
});
</script>

<template>
  <div class="right">
    <p v-if="error" class="error">{{ errorDisplay }}</p>

    <div v-if="data">
      <ul class="stats">
        <li v-for="item in statData" :key="item.label">
          <Stat v-bind="item" />
        </li>
      </ul>

      <ul class="days">
        <li v-for="(day, index) in data?.forecast?.forecastday" :key="index">
          <DayCard
            :data="new Date(day?.date)"
            :temperature="day?.day?.avgtemp_c"
            :weather-code="day?.day?.condition?.code"
            :is-active="activeIndex === index"
            @click="() => emit('select-index', index)"
          />
        </li>
      </ul>
    </div>

    <ChangeCity />
  </div>
</template>

<style scoped>
.right {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  min-height: 623px;
  padding: 55px 60px;
  border-radius: 0 25px 25px 0;
  background-color: var(--color-bg-main);
}

.error {
  margin: -55px 0 0;
  padding: 15px 52px;
  height: max-content;
  font-weight: 400;
  font-size: 18px;
  text-align: center;
  color: var(--color-primary);
  box-shadow: 1px 2px 4px 0 var(--color-bg-main);
  background-color: var(--color-bg-card);
  border-radius: 0 0 25px 25px;
}

.stats {
  display: grid;
  gap: 16px;
  margin: 0 0 80px;
  padding: 0;
  list-style: none;
}

.days {
  display: flex;
  gap: 1px;
  margin: 0;
  padding: 0;
  list-style: none;
}
</style>
