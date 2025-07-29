<script setup></script>

<template>
  <button class="button">
    <slot />
  </button>
</template>

<style scoped>
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 9px;
  width: 100%;
  padding: 10px 14px;
  font-size: 20px;
  background-image: var(--gradient);
  border: none;
  border-radius: 10px;
  color: var(--color-primary);
}

.button:hover {
  background-image: var(--gradient-inverted);
}
</style>
