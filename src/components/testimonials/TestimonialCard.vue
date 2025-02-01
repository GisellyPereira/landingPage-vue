<template>
  <div class="testimonial-card">
    <div class="testimonial-image">
      <img :src="testimonial.image" :alt="testimonial.name">
    </div>
    <p class="testimonial-text">{{ testimonial.text }}</p>
    <div class="testimonial-author">
      <h4>{{ testimonial.name }}</h4>
      <p>{{ testimonial.role }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TestimonialCard',
  props: {
    testimonial: {
      type: Object,
      required: true
    }
  }
}
</script> 