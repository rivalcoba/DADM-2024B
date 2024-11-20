<script setup>
import PlanPickerItem from './PlanPickerItem.vue';
import { ref, onMounted } from 'vue';
// Creando una referencia reactiva
// para almecenar el plan seleccionado
const selectedPlan = ref(null)
const plans =
  ref(['El cafetero', 'El chelero', 'El intelectual']);
const selectPlan = (name) => {
  // Almacenar el plan seleccionado
  selectedPlan.value = name;
};
// Intentado obtener la referencia al elemento .plans
console.log("Termina de ejecutar el script setup 🥳");

// registrando el hook mounted
onMounted(() => {
  console.log("El componente PlanPicker se ha montado 🎉");
  console.log(document.querySelector('.plans'));
});
</script>

<template>
  <div class="plans">
    <PlanPickerItem 
      v-for="plan in plans" 
      :key="plan" 
      :name="plan"
      @select="selectPlan"
      :selectPlan="selectedPlan" />
  </div>
</template>

<style scoped></style>