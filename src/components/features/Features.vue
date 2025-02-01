<template>
  <section class="features">
    <div class="features-container">
      <h2 class="section-title">Nossos Diferenciais</h2>
      
      <div class="features-grid">
        <FeatureCard
          v-for="feature in features"
          :key="feature.id"
          :feature="feature"
          class="animate-up"
        />
      </div>
    </div>
  </section>
</template>

<script>
import './Features.css'
import FeatureCard from './FeatureCard.vue'

export default {
  name: 'FeaturesSection',
  components: {
    FeatureCard
  },
  data() {
    return {
      features: [
        {
          id: 1,
          icon: '🚀',
          title: 'Rápido e Eficiente',
          description: 'Soluções otimizadas para máxima performance',
          color: '#C4B19C'
        },
        {
          id: 2,
          icon: '💡',
          title: 'Inovação Constante',
          description: 'Sempre atualizado com as últimas tecnologias',
          color: '#D4C5B4'
        },
        {
          id: 3,
          icon: '🛡️',
          title: 'Segurança Total',
          description: 'Proteção completa para seus dados',
          color: '#E5D5C5'
        }
        // Adicione mais features conforme necessário
      ]
    }
  }
}
</script> 