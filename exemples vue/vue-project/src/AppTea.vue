<script setup lang="ts">
import Tes from './components/Tes.vue';

const llistatTe= ["Verd","Vermell","Negre","Blanc"]
</script>

<template>
    <div class="content">
        <h1 class="title">Subscripcions disponibles</h1>
        <h2 class="subtitle">
            Disposem dels millor tes del món
        </h2>
        <div class="plans">
           <Tes v-for="te in llistatTe":key="te" :name="te"/>
        </div>
    </div>
</template>