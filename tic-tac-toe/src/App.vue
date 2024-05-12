<script setup lang="ts">
import TitleSection from '@/components/TitleSection.vue'
import GameScreen from '@/components/GameScreen.vue'
</script>

<template>
  <header>
    <TitleSection text="tic tac toe" />
  </header>

  <main>
    <GameScreen />
  </main>
</template>

<style scoped></style>