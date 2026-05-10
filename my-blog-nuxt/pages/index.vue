<template>
  <div>
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/search">Search</NuxtLink>
    </nav>

    <h1>Blog Homepage</h1>

    <!-- Category filter dropdown (hardcoded for now) -->
    <select v-model="selectedCategory">
      <option value="">All Categories</option>
      <option value="Tech">Tech</option>
      <option value="Lifestyle">Lifestyle</option>
      <option value="News">News</option>
    </select>

    <!-- Placeholder posts (will be replaced with API data later) -->
    <div v-for="post in filteredPosts" :key="post.id">
      <PostCard :post="post" />
    </div>
  </div>
</template>

<script setup>
// Hardcoded placeholder data — will be replaced with Strapi API later
const posts = ref([
  {
    id: 1,
  attributes: {
    title: 'My First Post',
    author: 'Jane Doe',
    snippet: 'preview',
    content: 'fjshdjfh sjdkfhdskjfhsdk djfhsdkjf',
    category: 'Tech',
    slug: 'my-first-post'
  }
},
{
  id: 2,
  attributes: {
    title: 'A Lifestyle Post',
    author: 'John Smith',
    snippet: 'preview',
    content: 'fjshdjfh sjdkfhdskjfhsdk djfhsdkjf',
    category: 'Lifestyle',
    slug: 'a-lifestyle-post'
  }
},
{
  id: 3,
  attributes: {
    title: 'Breaking News',
    author: 'Jane Doe',
    snippet: 'preview',
    content: 'fjshdjfh sjdkfhdskjfhsdk djfhsdkjf',
    category: 'News',
    slug: 'breaking-news'
  }
  }
])

const selectedCategory = ref('')

const filteredPosts = computed(() => {
  if (!selectedCategory.value) return posts.value
  return posts.value.filter(p => p.attributes.category === selectedCategory.value)
})
</script>