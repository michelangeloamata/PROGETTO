<script setup lang="ts">
// This is how you pass in props.
defineProps<{
  text: string,
}>()
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ text }}</h1>
    <p>lets hope this isn't a tie...</p>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 5rem;
  position: relative;
  text-shadow: 3px 2px var(--shadow);
  text-decoration: underline;
  margin: 5rem 0 0 0;
  padding: 0;
}

.greetings h1,
.greetings p {
  text-align: center;
}

p {
  font-size: 1.5rem;
}
</style>

