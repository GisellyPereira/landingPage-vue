<template>
  <div class="price-card" :class="{ 'highlighted': plan.highlighted }">
    <h3>{{ plan.name }}</h3>
    <div class="price">
      <span class="amount">{{ plan.price }}</span>
      <span class="period">{{ plan.period }}</span>
    </div>
    <ul class="features">
      <li v-for="(feature, index) in plan.features" :key="index">
        {{ feature }}
      </li>
    </ul>
    <button class="cta-button" :class="{ 'highlighted': plan.highlighted }">
      Começar Agora
    </button>
  </div>
</template>

<script>
export default {
  name: 'PriceCard',
  props: {
    plan: {
      type: Object,
      required: true
    }
  }
}
</script> 