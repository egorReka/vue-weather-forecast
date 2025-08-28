<script setup>
import IconPin from '../icons/IconPin.vue';
import IconSun from '../icons/IconSun.vue';
import IconRain from '../icons/IconRain.vue';
import IconCloud from '../icons/IconCloud.vue';
import { computed } from 'vue';

const {dayData, city} = defineProps({
  dayData: Object,
  city: String
})

const date = computed(() => new Date(dayData.date));
const weekday = computed(() => date.value.toLocaleDateString('ru-RU', {weekday: 'long'}));
const formatted = computed(() => date.value.toLocaleDateString('ru-RU', { day: 'numeric', month: 'long', year: 'numeric' }).replace(' г.', ''));
const weatherCode = computed(() => dayData.day.condition.code);
const temperature = computed(() => Math.floor(dayData.day.avgtemp_c));
const weatherText = computed(() => dayData.day.condition.text);
</script>

<template>
  <div class="left">
    <div class="left__header">
      <h1 class="title-day">{{weekday}}</h1>
      <p class="full-date">{{formatted}}</p>
      <p class="location">
        <IconPin />
        {{city}}
      </p>
    </div>

    <div class="left__footer">
      <IconSun v-if="weatherCode <= 1000" :size="95" />
      <IconCloud v-if="weatherCode >= 1001 && weatherCode < 1063" :size="95" />
      <IconRain v-if="weatherCode >= 1063" :size="95" />
  
      <p class="temperature">{{ `${temperature} °C` }}</p>
      <p class="weather-text">{{ weatherText }}</p>
    </div>

  </div>
</template>

<style scoped>
.left {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  row-gap: 20px;
  min-height: 666px;
  padding: 56px 32px;
  background-color: var(--color-bg-main);
  border-radius: 30px;
  background-image: url('../assets/rectangle.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}

.title-day {
  margin: 0 0 16px;
  font-size: 37px;
  text-transform: capitalize;
}

.full-date {
  margin: 0 0 10px;
  font-size: 22px;
  font-weight: 500;
}

.location {
  display: flex;
  align-items: center;
  column-gap: 8px;
  margin: 0;
}

.temperature {
  margin: 9px 0 13px;
  font-weight: 700;
  font-size: 50px;
}

.weather-text {
  margin: 0;
  font-weight: 700;
  font-size: 30px;
}
</style>
