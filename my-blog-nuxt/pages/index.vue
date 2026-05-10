<template>
  <div>
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/search">Search</NuxtLink>
    </nav>

    <h1>Blog</h1>

    <CategoryFilter :categories="categories" v-model="selectedCategory" />

    <p v-if="pending">Loading posts...</p>
    <p v-else-if="error">Failed to load posts.</p>

    <div class="post-grid">
      <PostCard v-for="post in filteredPosts" :key="post.id" :post="post" />
    </div>
  </div>
</template>

<script setup>
const config = useRuntimeConfig()
const selectedCategory = ref('')

const { data, pending, error } = await useFetch(
  `${config.public.apiBase}/api/blog-posts?populate=*`
)

const posts = computed(() => data.value?.data || [])

const categories = computed(() => [
  ...new Set(posts.value.map(p => p.category))
])

const filteredPosts = computed(() => {
  if (!selectedCategory.value) return posts.value
  return posts.value.filter(p => p.category === selectedCategory.value)
})
</script>
