<template>
  <div class="post-card">
    <NuxtLink :to="`/posts/${post.attributes.slug}`">
      <h2>{{ post.attributes.title }}</h2>
    </NuxtLink>
    <p>{{ post.attributes.author }} · {{ post.attributes.category }}</p>
    <p>{{ post.attributes.snippet }}</p>
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
