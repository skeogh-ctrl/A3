<template>
  <div>
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/search">Search</NuxtLink>
    </nav>

    <h1>Search</h1>

    <input
      v-model="query"
      type="text"
      placeholder="Search by title or author..."
    />

    <p v-if="query && results.length === 0">No results found.</p>

    <div v-for="post in results" :key="post.id">
      <PostCard :post="post" />
    </div>
  </div>
</template>

<script setup>

const posts = ([
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

const query = ref('')

const results = computed(() => {
  const q = query.value.toLowerCase()
  if (!q) return posts.value
  return posts.value.filter(p =>
    p.attributes.title.toLowerCase().includes(q) ||
    p.attributes.author.toLowerCase().includes(q)
  )
})
</script>
