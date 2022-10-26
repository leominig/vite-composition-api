<script setup>
const props = defineProps(['title', 'id', 'body', 'colorText'])
const emit = defineEmits(['changeFavorite'])
</script>

<template>
  <div class="card mb-2">
    <div class="card-body">
        <h5 
            class="card-title"
            :class="`text-${colorText}`"
            >{{props.title}} - {{props.id}}</h5>            
            <p>{{ props.body }}</p>    
        
        <button 
            @click="emit('changeFavorite', title)" 
            class="btn btn-outline-primary">Favoritos</button>         
    </div>    
  </div>
</template>


