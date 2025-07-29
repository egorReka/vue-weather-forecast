<script setup>
import IconPin from '../icons/IconPin.vue';
import IconSun from '../icons/IconSun.vue';
</script>

<template>
  <div class="left">
    <h1 class="title-day">Вторник</h1>
    <p class="full-date">20 июня 2025</p>
    <p class="location">
      <IconPin />
      Москва
    </p>

    <IconSun />
  </div>
</template>

<style scoped>
.left {
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
  margin: 0 0 200px;
}
</style>
