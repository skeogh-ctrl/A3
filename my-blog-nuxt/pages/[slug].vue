<template>
  <div>
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/search">Search</NuxtLink>
    </nav>

    <NuxtLink to="/">← Back to Home</NuxtLink>

    <div v-if="post">
      <h1>{{ post.attributes.title }}</h1>
      <p>By {{ post.attributes.author }} | {{ post.attributes.category }}</p>
      <hr />
   
      <p>{{ post.attributes.content }}</p>
    </div>

    <div v-else>
      <p>Post not found.</p>
    </div>
  </div>
</template>

<script setup>
const route = useRoute()


const allPosts = [
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
]


const post = computed(() =>
  allPosts.find(p => p.attributes.slug === route.params.slug)
)
</script>
