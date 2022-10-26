<template>
  <Spinner v-if="loading" />
  <div class="container">
      <h1>App</h1>   
      <h2>Mis Posts Favoritos: {{favorite}}</h2>         
      <PaginatePost 
        @next="next"
        @preview="preview"
        :init="init"
        :end="end"
        :maxlength="maxlength"
      />
      <blog-post  
        v-for="post in posts.slice(init, end)" :key="post.id"
        :title="post.title"
        :id="post.id"  
        :body= "post.body"  
        :colorText="post.colorText"  
        @changeFavorite="changeFavorite"        
        />      
  </div>
 
</template>

<script setup>
import {computed, ref} from 'vue'

import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue'
import Spinner from './components/Spinner.vue'

const posts = ref([])
const postByPage = 10
const init = ref(0)
const end = ref(postByPage)

const next = () => {
  init.value = init.value + postByPage
  end.value = end.value + postByPage
}

const preview = () => {
  init.value = init.value - postByPage
  end.value = end.value - postByPage
}

const changeFavorite = (title) => {
  favorite.value = title
}

const favorite = ref('')

const maxlength = computed(()=> {
  return posts.value.length
})

const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally {
    loading.value = false
  }
}

fetchData()

 
</script>
