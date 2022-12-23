<script setup>
defineProps({
     title: String,
     id: Number,
     body: {
          type: String,
          default: 'Sin descripción'
     },
     cambiarFavorito: Function,
});

/*

const emit = defineEmits(["cambiarFavoritoNombre"]);*/
</script>

<template>

     <div class="card">
          <div class="card-body">
               <h5 class="card-title">{{ title }}-{{ id }}</h5>
               <p>{{ body }}</p>
               <button @click="cambiarFavorito(title)" class="btn btn-outline-primary">Favorito</button>
          </div>
     </div>
</template>