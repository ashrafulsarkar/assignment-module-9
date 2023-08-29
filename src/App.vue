<script setup>
import Header from './components/Header.vue'
import { ref } from 'vue';
import SinglePost from './components/SinglePost.vue'
import Home from './components/Home.vue';

const paramValue = ref('')

// Parse query parameters from the URL
const queryParams = new URLSearchParams(window.location.search);

// Get the value of the "param" query parameter
const param = queryParams.get('id');
if (param) {
	paramValue.value = param
}
</script>

<template>
	<Header></Header>
	<Home v-show = "paramValue == ''"></Home>
	<SinglePost></SinglePost>
</template>