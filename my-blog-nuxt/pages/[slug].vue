<template>
  <div>
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/search">Search</NuxtLink>
    </nav>

    <NuxtLink to="/">← Back to Home</NuxtLink>

    <p v-if="pending">Loading post...</p>
    <p v-else-if="error">Failed to load post.</p>

    <div v-else-if="post">
      <h1>{{ post.title }}</h1>
      <p>By {{ post.author }} | {{ post.category }}</p>
      <hr />
      <div v-html="renderedContent" />
    </div>

    <div v-else>
      <p>Post not found.</p>
    </div>
  </div>
</template>

<script setup>
import { marked } from 'marked'

const config = useRuntimeConfig()
const route = useRoute()

const { data, pending, error } = await useFetch(
  `${config.public.apiBase}/api/blog-posts?filters[slug][$eq]=${route.params.slug}&populate=*`
)

const post = computed(() => data.value?.data?.[0])

const renderedContent = computed(() => {
  return post.value ? marked(post.value.content) : ''
})
</script>
