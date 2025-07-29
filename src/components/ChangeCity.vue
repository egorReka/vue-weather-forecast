<script setup>
import { inject, nextTick, ref } from 'vue';

import Button from './Button.vue';
import Input from './Input.vue';
import IconPin from '../icons/IconPin.vue';
import { cityProvide } from '../constats';

const isEdited = ref(false);
const city = inject(cityProvide);
const inputValue = ref(city.value);

async function onClickChangeCity() {
  await nextTick();

  isEdited.value = true;
}

function saveCity() {
  isEdited.value = false;
  city.value = inputValue.value;
}
</script>

<template>
  <div v-if="isEdited" class="change-city">
    <Input
      v-model="inputValue"
      v-model:additional="inputValue"
      v-focus
      placeholder="Введите город"
      @keyup.enter="saveCity()"
    />
    <Button @click="saveCity">Сохранить</Button>
  </div>

  <Button
    v-else
    v-bind="{ class: 'change-city__button' }"
    @click="onClickChangeCity"
  >
    <IconPin />
    Изменить город
  </Button>
</template>

<style scoped>
.change-city {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 12px;
}
</style>
