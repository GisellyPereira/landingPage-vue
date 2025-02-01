<template>
  <section class="blog-section">
    <div class="blog-container">
      <h2 class="blog-title">Blog</h2>
      <div class="title-accent"></div>
      
      <div class="blog-grid">
        <article class="blog-post" v-for="post in posts" :key="post.id">
          <div class="post-image">
            <img :src="post.image" :alt="post.title">
          </div>
          <div class="post-content">
            <div class="post-meta">
              <span class="post-category">{{ post.category }}</span>
              <span class="post-date">{{ post.date }}</span>
            </div>
            <h3 class="post-title">{{ post.title }}</h3>
            <p class="post-excerpt">{{ post.excerpt }}</p>
            <a href="#" class="post-link">Ler mais</a>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script>
import './Blog.css'
import img1 from '@/assets/img-1.jpg'
import img2 from '@/assets/img-2.jpg'
import img3 from '@/assets/img-3.jpg'

export default {
  name: 'BlogSection',
  data() {
    return {
      posts: [
        {
          id: 1,
          title: 'Como a Arquitetura Digital está Revolucionando Projetos',
          excerpt: 'Descubra as últimas tendências em visualização arquitetônica e como elas estão transformando a indústria.',
          image: img1,
          category: 'Tendências',
          date: '15 Mar 2024'
        },
        {
          id: 2,
          title: 'O Impacto da Realidade Virtual na Apresentação de Projetos',
          excerpt: 'Explore como a VR está mudando a forma como arquitetos apresentam seus projetos aos clientes.',
          image: img2,
          category: 'Tecnologia',
          date: '12 Mar 2024'
        },
        {
          id: 3,
          title: 'Sustentabilidade e Design Digital: O Futuro da Arquitetura',
          excerpt: 'Como as ferramentas digitais estão contribuindo para projetos mais sustentáveis.',
          image: img3,
          category: 'Sustentabilidade',
          date: '10 Mar 2024'
        }
      ]
    }
  }
}
</script> 