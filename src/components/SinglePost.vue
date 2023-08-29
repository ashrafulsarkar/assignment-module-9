<script setup>
import { ref, onBeforeMount } from 'vue';

const posts = ref([]);

onBeforeMount(async () => {
    // Parse query parameters from the URL
    const queryParams = new URLSearchParams(window.location.search);

    // Get the value of the "param" query parameter
    const param = queryParams.get('id');

    if (param) {
        try {
            const url = `https://basic-blog.teamrabbil.com/api/post-details/${ param }`
            const response = await fetch(url);
            if (response.ok) {
                const data = await response.json();
                posts.value = data;
            } else {
                console.error('Error fetching posts:', response.statusText);
            }
        } catch (error) {
            console.error('Error fetching posts:', error);
        }
    }
});

</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col-lg-12 mt-4 mb-5" v-for="post in posts" :key="post.id">
                <div class="card">
                    <img :src="post.img" class="card-img-top" alt="...">
                    <div class="card-body">
                        <h5 class="card-title">{{post.title}}</h5>
                        <p class="card-text">{{post.content}}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>