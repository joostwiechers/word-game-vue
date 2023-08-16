<script setup>
defineProps({
  message: String,
  type: String
})
</script>

<template>
  <div :class="['notification', `notification--${type}`]">
    {{ message }}
  </div>
</template>

<style lang="scss" scoped>
.notification {
  border-radius: 1rem;
  font-size: 1rem;
  padding: 1rem;
  margin: 0 auto 2rem;

  &--error {
    background: red;
  }

  &--success {
    background: lightgreen;
    color: black
  }
}
</style>
