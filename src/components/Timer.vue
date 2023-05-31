<script setup lang="ts">
defineProps<{ count: string; label: string }>();
</script>

<template>
  <div class="wrapper">
    <div class="count">{{ count }}</div>
    <div class="label">{{ label }}</div>
  </div>
</template>

<style scoped>
.count {
  font-size: 4rem;
  font-weight: 800;
  color: #b9b4b4;
}

.wrapper {
  margin-top: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.label {
  color: #b9b4b4;
  font-size: 2rem;
}

@media (max-width: 600px) {
  .label {
    font-size: 1rem;
  }
  .count {
    font-size: 2rem;
  }
}

@media (max-width: 320px) {
  .label {
    font-size: 0.875rem;
  }
  .count {
    font-size: 1rem;
  }
}
</style>
