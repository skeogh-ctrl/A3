<template>
  <div>
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/search"> Search</NuxtLink>
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
<style >
* 
{ box-sizing: 
border-box; 
margin: 0; 
padding: 0; 
}
nav{
  text-align: center;
}
a{
  font-size: 20px;
  font-weight: 800;
  color: #050835;
  text-decoration:none ;


 
 
}
select{
  background-color: #d2cde1;
  width: 100%;
  text-align: center;
  border-radius: 5px;
  padding: 7px;
  margin-bottom: 20px;
}
a:hover{
  color: #0b0b8f;
}
h1{
  padding: 20px;
  color: #321f62;
}
body { 
  font-family: sans-serif; 
  max-width: 900px; 
  margin: 0 auto; 
  padding: 2rem; 
}
.post-grid { 
  display: grid; 
  grid-template-columns: 
  repeat(auto-fill, 
  minmax(280px, 1fr)); 
  gap: 1.5rem; }
.card { 
  border: 1px solid #ddd; 
  background-color: #372662;
  color: #ffffff;
  border-radius: 8px; 
  padding: 1rem; 
}
.card  > a{
  color:#ffffff
}
.card  > a:hover{
  color:#a6a6a6
}
input { 
  width: 100%; 
  padding:0.5rem; 
  margin-bottom: 1rem; 
  }
</style>
