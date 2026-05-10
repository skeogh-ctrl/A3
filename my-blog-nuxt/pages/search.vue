<template>
  <div>
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/search">Search</NuxtLink>
    </nav>

    <h1>Search</h1>

    <input v-model="query" type="text" placeholder="Search by title or author..." />

    <p v-if="pending">Loading...</p>
    <p v-else-if="error">Failed to load posts.</p>
    <p v-else-if="query && results.length === 0">No results found.</p>

    <PostCard v-for="post in results" :key="post.id" :post="post" />
  </div>
</template>

<script setup>
const config = useRuntimeConfig()
const query = ref('')

const { data, pending, error } = await useFetch(
  `${config.public.apiBase}/api/blog-posts?populate=*`
)

const posts = computed(() => data.value?.data || [])

const results = computed(() => {
  const q = query.value.toLowerCase()
  if (!q) return posts.value
  return posts.value.filter(p =>
    p.title.toLowerCase().includes(q) ||
    p.author.toLowerCase().includes(q)
  )
})
</script>
