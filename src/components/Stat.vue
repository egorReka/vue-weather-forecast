<script setup>
const { label = 'Не задан', stat } = defineProps({
  label: String,
  stat: String,
});
</script>

<template>
  <dl class="stat">
    <dt class="stat__label">{{ label }}</dt>
    <dd class="stat__value">{{ stat }}</dd>
  </dl>
</template>

<style scoped>
.stat {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 15px;
  margin: 0;
  padding: 0;
}

.stat__label {
  margin: 0;
  font-size: 24px;
  font-weight: 700;
  text-transform: uppercase;
}

.stat__value {
  align-self: flex-end;
  margin: 0;
  font-weight: 500;
  font-size: 24px;
  white-space: nowrap;
}
</style>
