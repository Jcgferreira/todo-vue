<script setup>
  const props = defineProps(['estado']);
</script>

<template>
    <div v-if="estado !== null" class="mt-4">
      <h3>Resultado: {{ props.estado }}</h3>
    </div>
</template>

<style scoped>

</style>