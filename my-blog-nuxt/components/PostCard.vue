<template>
  <div class="post-card">
   
      <h2>{{ post.title }}</h2>
  
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
