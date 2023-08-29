<script setup>
import { ref, onBeforeMount } from 'vue';

const posts = ref([]);

const fetchPosts = async () => {
  try {
    const response = await fetch('https://basic-blog.teamrabbil.com/api/post-newest');
    if (response.ok) {
      const data = await response.json();
      posts.value = data;
    } else {
      console.error('Error fetching posts:', response.statusText);
    }
  } catch (error) {
    console.error('Error fetching posts:', error);
  }
};

onBeforeMount(fetchPosts);

// console.log(posts);
</script>

<template>
    <div class="container">
        <div class="row mb-5">
            <div class="col-lg-12 mt-4">
                <h3>Latest Post</h3>
            </div>
            <div class="col-lg-6 mt-4" v-for="post in posts" :key="post.id">
                <div class="card">
                    <img :src="post.img" class="card-img-top" alt="...">
                    <div class="card-body">
                        <h5 class="card-title">{{post.title}}</h5>
                        <p class="card-text">{{post.short}}</p>
                        <a :href="`/?id=${post.id}`" class="btn btn-primary">আরো পড়ুন</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>