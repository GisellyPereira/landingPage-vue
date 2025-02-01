<template>
  <article class="blog-card">
    <div class="blog-image">
      <img :src="post.image" :alt="post.title">
      <span class="category">{{ post.category }}</span>
    </div>
    <div class="blog-content">
      <span class="date">{{ post.date }}</span>
      <h3>{{ post.title }}</h3>
      <p>{{ post.excerpt }}</p>
      <a href="#" class="read-more">Ler mais →</a>
    </div>
  </article>
</template>

<script>
export default {
  name: 'BlogCard',
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script> 