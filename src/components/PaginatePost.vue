
<script setup>
defineProps(['inicio', 'fin', 'maxLength']);
const emit = defineEmits(["next", "prev"]);
</script>




<template>
     <div class="btn-group" role="group" aria-label="Basic example">
          <button @click="$emit('prev')" :disabled="inicio <= 0" type="button" class="btn btn-outline-primary">Previous
               {{ inicio }}

          </button>
          <button @click="$emit('next')" :disabled="fin >= maxLength" type="button" class="btn btn-outline-primary">Next
               {{
          fin
               }}</button>
     </div>
</template>   