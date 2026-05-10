<template>
  <div class="card">
   
    <NuxtLink :to="`/posts/${post.slug}`">
      <h2>{{ post.title }}</h2>
    </NuxtLink>
    <p>{{ post.author }} · {{ post.category }}</p>
    <p>{{ post.snippet }}</p>
</div>
</template>

<script setup>
defineProps({
  post: {
    type: Object,
    required: true
  }
})
</script>
