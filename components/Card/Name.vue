<script setup lang="ts">
interface NameProps {
  name: string
}
const props = defineProps<NameProps>()
</script>

<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <button>x</button>
  </div>
</template>

<style scoped>
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: #fff;
  border-radius: 1rem;
  padding: 0.1rem;
  margin: 0 0.5rem 1rem 0;
  position: relative;
}

.card button {
  position: absolute;
  top: 6px;
  right: 6px;
  cursor: pointer;
}
</style>