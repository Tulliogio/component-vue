<script setup>
import { ref, onMounted } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
const posts = ref([
  { id: 1, title: "Post 01", body: "description del post 01" },
  { id: 2, title: "Post 02", body: "description del post 02" },
  { id: 3, title: "Post 03", body: "description del post 03" },
  { id: 4, title: "Post 04" },
]);
const favorito = ref([]);
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);


const cambiarFavorito = (title) => {
  favorito.value = title;
};

const next = () => {
  inicio.value = inicio.value + postXpage
  fin.value = fin.value + postXpage
};
const prev = () => {
  inicio.value = inicio.value - postXpage
  fin.value = fin.value - postXpage
};

onMounted(async () => {
  loading.value = true;
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally {
    setTimeout(() => {
      loading.value = false
    }, 2000);
  }
})


/*fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => posts.value = data)
  .finally(() => {
    setTimeout(() => {
      loading.value = false
    }, 2000);
  });*/
</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>App</h1>
    <h2>Mi post favorito : {{ favorito }}</h2>

    <PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxLength="posts.length" class="mb-2" />
    <BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.id" :title="post.title" :id="post.id"
      :body="post.body" :cambiarFavorito="cambiarFavorito" />

  </div>

</template>