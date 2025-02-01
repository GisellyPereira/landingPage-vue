<template>
  <section class="pricing">
    <div class="pricing-container">
      <h2 class="section-title">Nossos Planos</h2>
      <div class="title-accent"></div>
      
      <div class="pricing-grid">
        <div class="price-card">
          <h3>Básico</h3>
          <div class="price">
            <span class="currency">R$</span>
            <span class="amount">99</span>
            <span class="period">/mês</span>
          </div>
          <ul class="features-list">
            <li>Feature 1</li>
            <li>Feature 2</li>
            <li>Feature 3</li>
          </ul>
          <button class="cta-button">Começar Agora</button>
        </div>

        <div class="price-card featured">
          <div class="featured-tag">Mais Popular</div>
          <h3>Profissional</h3>
          <div class="price">
            <span class="currency">R$</span>
            <span class="amount">199</span>
            <span class="period">/mês</span>
          </div>
          <ul class="features-list">
            <li>Feature 1</li>
            <li>Feature 2</li>
            <li>Feature 3</li>
            <li>Feature 4</li>
            <li>Feature 5</li>
          </ul>
          <button class="cta-button featured">Começar Agora</button>
        </div>

        <div class="price-card">
          <h3>Enterprise</h3>
          <div class="price">
            <span class="currency">R$</span>
            <span class="amount">299</span>
            <span class="period">/mês</span>
          </div>
          <ul class="features-list">
            <li>Feature 1</li>
            <li>Feature 2</li>
            <li>Feature 3</li>
            <li>Feature 4</li>
            <li>Feature 5</li>
            <li>Feature 6</li>
          </ul>
          <button class="cta-button">Começar Agora</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import './Pricing.css'

export default {
  name: 'PricingSection'
}
</script> 