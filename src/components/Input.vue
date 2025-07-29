<script setup>
// без v-model
// const emit = defineEmits(['update:value']);

const model = defineModel({ type: String, required: true, default: '' });

// несколько v-model на одном компоненте
// const additional = defineModel('additional', { type: String, required: true });
</script>

<template>
  <!-- без v-model -->
  <!-- <input
    class="input"
    type="text"
    @input="emit('update:value', $event.target.value)"
  /> -->

  <input v-model="model" class="input" type="text" />
</template>

<style scoped>
.input {
  width: 100%;
  padding: 15px 19px;
  font-size: 18px;
  font-weight: 400;
  border: none;
  border-radius: 10px;
  background-color: var(--color-bg-card);
  box-shadow: 1px 2px 4px 0 var(--color-bg-main);
  color: var(--color-primary);
}

.input::placeholder {
  color: var(--color-placeholder);
}
</style>
