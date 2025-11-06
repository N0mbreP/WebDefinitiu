<script setup>
// què escolto? els prop
const props = defineProps({
  teas: {
    type: Array,
    required: true,
  },
});
// què envio? els emits
// Definim emits que el component pot enviar
// emit és una funció que ens inventem i que permet enviar events al component pare
const emit = defineEmits(["enviarNom"]);
// Funció que emet el nom del te seleccionat
const agafarNom = (name) => {
  emit("enviarNom", name);
};

</script>

<template>
<div class="plans">
    <div class="plan" v-for="tea in props.teas" :key="index" @click="agafarNom(tea.name) ">
      <div class="description">
        <span class="title">{{ tea.name }}</span>
        <span>{{ tea.description }}</span>
        <span>{{ tea.price }} €</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>