<template>
  <section class="testimonials">
    <div class="testimonials-container">
      <div class="testimonials-header">
        <h2 class="section-title">O que nossos clientes dizem</h2>
      </div>

      <div class="testimonials-slider" ref="slider">
        <div class="testimonials-track" :style="trackStyle">
          <div v-for="testimonial in testimonials" 
               :key="testimonial.id" 
               class="testimonial-card">
            <div class="testimonial-content">
              <div class="quote-icon">❝</div>
              <p class="testimonial-text">{{ testimonial.text }}</p>
              <div class="testimonial-author">
                <img :src="testimonial.image" :alt="testimonial.name" class="author-image">
                <div class="author-info">
                  <h4>{{ testimonial.name }}</h4>
                  <span>{{ testimonial.role }}, {{ testimonial.company }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="slider-controls">
        <button class="control-btn prev" @click="prevSlide" :disabled="currentSlide === 0">
          <span>←</span>
        </button>
        <div class="slider-dots">
          <button v-for="(_, index) in testimonials" 
                  :key="index"
                  class="dot"
                  :class="{ active: currentSlide === index }"
                  @click="goToSlide(index)">
          </button>
        </div>
        <button class="control-btn next" @click="nextSlide" 
                :disabled="currentSlide === testimonials.length - 1">
          <span>→</span>
        </button>
      </div>
    </div>
  </section>
</template>

<script>
import './Testimonials.css'
import perfilJoao from '@/assets/perfil-joao.jpg'
import perfilMaria from '@/assets/perfil-maria.jpg'
import perfilPedro from '@/assets/perfil-pedro.jpg'

export default {
  name: 'TestimonialsSection',
  data() {
    return {
      currentSlide: 0,
      testimonials: [
        {
          id: 1,
          text: 'Incrível experiência! A equipe superou todas as expectativas. O projeto foi entregue antes do prazo e com qualidade excepcional.',
          name: 'João Silva',
          role: 'CEO',
          company: 'TechCorp',
          image: perfilJoao
        },
        {
          id: 2,
          text: 'A atenção aos detalhes e o profissionalismo da equipe são impressionantes. Recomendo fortemente!',
          name: 'Maria Santos',
          role: 'Diretora de Marketing',
          company: 'Inovativa',
          image: perfilMaria
        },
        {
          id: 3,
          text: 'Transformaram completamente nossa visão em realidade. O resultado final superou nossas expectativas.',
          name: 'Pedro Costa',
          role: 'Arquiteto Chefe',
          company: 'DesignPro',
          image: perfilPedro
        }
      ]
    }
  },
  computed: {
    trackStyle() {
      return {
        transform: `translateX(-${this.currentSlide * 100}%)`
      }
    }
  },
  methods: {
    nextSlide() {
      if (this.currentSlide < this.testimonials.length - 1) {
        this.currentSlide++
      }
    },
    prevSlide() {
      if (this.currentSlide > 0) {
        this.currentSlide--
      }
    },
    goToSlide(index) {
      this.currentSlide = index
    }
  }
}
</script> 