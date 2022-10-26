<script setup>
const emit = defineEmits(['next', 'preview'])
defineProps(['init', 'end','maxlength'])
</script>

<template>
  <div class="btn" role="group" aria-label="Basic example">
    <button 
        @click="emit('preview')" 
        type="button" 
        class="btn btn-outline-primary"   
        :disabled="init === 0"   
        >Previus {{init}}
    </button>
    <button 
        @click="emit('next')" 
        type="button" 
        class="btn btn-outline-primary"
        :disabled=" end >= maxlength"
        >Next {{end}}
    </button> 
</div>
</template>



