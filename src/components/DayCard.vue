<script setup>
import IconRain from '../icons/IconRain.vue';
import IconSun from '../icons/IconSun.vue';
import IconCloud from '../icons/IconCloud.vue';

const emit = defineEmits(['click']);

const { weatherCode, temperature, data } = defineProps({
  weatherCode: Number,
  temperature: Number,
  data: Date,
  isActive: Boolean,
});
</script>

<template>
  <button
    class="day-card"
    :class="{ active: isActive }"
    type="button"
    @click="emit('click')"
  >
    <IconSun v-if="weatherCode <= 1000" />
    <IconCloud v-if="weatherCode >= 1001 && weatherCode < 1063" />
    <IconRain v-if="weatherCode >= 1063" />

    <span class="day-card__day">{{
      data.toLocaleDateString('ru-RU', { weekday: 'short' })
    }}</span>
    <span class="day-card__temperature"
      >{{ `${Math.floor(temperature)} °C` }}
    </span>
  </button>
</template>

<style scoped>
.day-card {
  display: grid;
  row-gap: 14px;
  justify-content: center;
  justify-items: center;
  width: 100%;
  padding: 15px 26px;
  color: var(--color-primary);
  background-color: var(--color-bg-card);
  box-shadow: 1px 2px 4px 0 var(--color-bg-main);
  border: none;
  border-radius: 10px;
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.day-card:hover {
  background-color: var(--color-bg-hover);
}

.day-card.active {
  background-color: var(--color-primary);
  color: var(--color-primary-inverted);
}

.day-card__day {
  font-size: 16px;
}

.day-card__temperature {
  font-weight: 700;
  font-size: 18px;
}
</style>
