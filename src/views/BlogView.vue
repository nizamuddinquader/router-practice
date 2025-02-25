<script setup>
import { ref, onBeforeMount } from 'vue';
import { RouterLink } from 'vue-router';

const posts = ref([])
onBeforeMount(async()=>{
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  const data = await response.json();
  posts.value = data.slice(0,10);
  // console.log(posts.value)
  
})

</script>

<template>
  <main class="flex-1 ml-64 p-8">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- Blog Post Cards -->
        <article v-for="post in posts" :key="id" class="bg-white rounded-lg shadow-md overflow-hidden hover:shadow-lg transition duration-200">
            <img :src="`https://picsum.photos/800/400?random=${post.id}`" alt="Blog post" class="w-full h-48 object-cover">
            <div class="p-6">
                <div class="flex items-center mb-3">
                    <img :src="`https://picsum.photos/32/32?random=${post.id}`" alt="Author" class="w-8 h-8 rounded-full mr-3">
                    <span class="bg-blue-100 text-blue-800 text-xs font-medium px-2.5 py-0.5 rounded">Programming</span>
                </div>
                <h2 class="text-xl font-semibold text-gray-800 mb-2">{{ post.title }}</h2>
                <p class="text-gray-600 mb-4">{{ post.body }}</p>
                <div class="flex items-center justify-between">
                    <span class="text-sm text-gray-500">5 min read</span>
                    <!-- <a href="single.html" class="text-blue-500 hover:text-blue-600 font-medium">Read More →</a> -->
                     <router-link :to="{name:'post', params:{id:post.id}}" class="text-blue-500 hover:text-blue-600 font-medium">Read More</router-link>
                </div>
            </div>
        </article>
    </div>
  </main>
</template>

<style scoped></style>
