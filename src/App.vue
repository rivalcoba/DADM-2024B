<script setup>
  import { ref } from 'vue';
  // Modelo
  const header = ref('App lista de compras');
  // --- items ---
  // Item-Model
  const items = ref([
    {id:'0', label: '10 bolillos', purchased: false, priority: true},
    {id:'1', label:'1 lata frijoles', purchased: true, priority: true},
    {id:'2', label:'1 Chelas', purchased: false, priority: false},
    {id:'3', label:'1 Nutella', purchased: true, priority: true},
  ]);
  // Item-Method
  const saveItem = () => {
    // Add new item
    items.value.push({id: items.value.length + 1, label: newItem.value});
    // Clean the input
    newItem.value = '';
  };
  // --- Formulario ---
  const newItem = ref('');
  const newItemHighPriority = ref(false);
  const editing = ref(true);
  const activateEdition = (activate) => {
    editing.value = activate;
  };


</script>

<template>
  <div class="header">
    <h1> 
      <i 
        class="material-icons shopping-cart-icon">
        local_mall
      </i> 
      {{ header }}
    </h1>
    <button 
      v-if="editing" 
      class="btn" 
      @click="activateEdition(false)">
        Cancelar
      </button>
    <button 
      v-else 
      class="btn btn-primary" 
      @click="activateEdition(true)">
        Agregar Articulo
    </button>
  </div>
  <!-- Agrupando Entradas de usuario -->
  <form
    class="add-item form"
    v-if="editing"
    v-on:submit.prevent="saveItem">
    <!-- Entrada de texto -->
    <input 
      type="text" 
      placeholder="Add Item" 
      v-model.trim="newItem">
    <!-- Radio Buttons -->
    <label><input type="checkbox" v-model="newItemHighPriority">Alta Prioridad</label>
    <!-- Boton -->
    <button 
      :disabled="newItem.length === 0"
      class="btn btn-primary">
      Salvar Articulo
    </button>
  </form>
  <!-- Lista -->
  <ul>
    <li 
      v-for="{label, id, purchased, priority} in items" 
      :key="id"
      :class="{ strikeout: purchased, priority: priority}"
      class="amazing"> 
      {{priority ? "🔥": "🛍️"}} {{ label }}
    </li>
  </ul>
  <p v-if="items.length === 0">🥀 NO HAY ELEMENTOS EN TU LISTA 🥀</p>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
</style>
