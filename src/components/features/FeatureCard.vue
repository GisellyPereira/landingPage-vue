<template>
  <div class="feature-card" :style="cardStyle">
    <div class="feature-icon-wrapper">
      <span class="feature-icon">{{ feature.icon }}</span>
    </div>
    <div class="feature-content">
      <h3>{{ feature.title }}</h3>
      <p>{{ feature.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FeatureCard',
  props: {
    feature: {
      type: Object,
      required: true
    }
  },
  computed: {
    cardStyle() {
      return {
        '--card-accent-color': this.feature.color
      }
    }
  }
}
</script> 