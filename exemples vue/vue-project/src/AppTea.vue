<script setup>
import { ref } from "vue";
import Tea from "./components/Tea.vue";

const teas = [
  { name: "Verds", description: "Te verd suau i fresc", price: 2.5 },
  { name: "Negres", description: "Te negre intens i robust", price: 3.0 },
  { name: "Herbes", description: "Infusió de herbes naturals", price: 2.0 },
  { name: "Blanc", description: "Infusió de herbes aromàtiques", price: 2.0 },
  { name: "Vermell", description: "Infusió de fruites del bosc", price: 2.0 },
];

// Variable reactiva per a guardar el te seleccionat
const selectedTea = ref("");

// Función que rep l' event del fill
const handleEnviarNom = (name) => {
  selectedTea.value = name;
};
</script>

<template>
  <div class="content">
    <h1 class="title">Subscripcions disponibles</h1>
    <h2 class="subtitle">Disposem dels millor tes del món</h2>

     <!-- Te seleccionat en div -->
    <div v-if="selectedTea" class="selected-tea" :class="{ highlighted: selectedTea }">
      {{ selectedTea }}
    </div>

    <div class="plans">
    <!-- escoltem event -->
      <Tea :teas="teas" @enviarNom="handleEnviarNom" />
    </div>
  </div>
</template>

<style scoped></style>
