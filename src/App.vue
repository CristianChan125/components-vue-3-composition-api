<script setup>
import BlogPost from './components/BlogPost.vue';
import { computed, onMounted, ref } from 'vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([])
const postXpage=10
const inicio = ref(0)
const fin = ref(postXpage)
const favorito=ref('')
const loading = ref(true)

const cambiarFavorito=(post)=>{
  favorito.value=post
}

const next = () =>{
  inicio.value= inicio.value+postXpage;
  fin.value= fin.value+postXpage
}

const prev = () =>{
  inicio.value= inicio.value-postXpage
  fin.value= fin.value-postXpage
}

fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res=>res.json())
  .then((data)=>posts.value=data)
  .finally(()=>{
    loading.value=false
  })

const maxLength=computed(()=>posts.value.length)
</script>
<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>Practica api con components</h1>
    <h2>Mi Post Favorito: {{favorito}}</h2>
    <PaginatePost class="mb-2" @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxLength="maxLength"></PaginatePost>
    <BlogPost class="mb-2" v-for="post in posts.slice(inicio,fin)" :key="post.id" :title="post.title" :id="post.id" :body="post.body" @cambiarFavorito="cambiarFavorito"></BlogPost>
  </div>
</template>