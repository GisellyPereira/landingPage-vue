<template>
  <div id="app">
    <MainHeader />
    <HeroSection />
    <FeaturesSection />
    <TestimonialsSection />
    <PricingSection />
    <BlogSection />
    <ContactSection />
    <FooterSection />
  </div>
</template>

<script>
import MainHeader from './components/header/Header.vue'
import HeroSection from './components/hero/Hero.vue'
import FeaturesSection from './components/features/Features.vue'
import TestimonialsSection from './components/testimonials/Testimonials.vue'
import PricingSection from './components/pricing/Pricing.vue'
import BlogSection from './components/blog/Blog.vue'
import ContactSection from './components/contact/Contact.vue'
import FooterSection from './components/footer/Footer.vue'
import './assets/styles/animations.css'

export default {
  name: 'App',
  components: {
    MainHeader,
    HeroSection,
    FeaturesSection,
    TestimonialsSection,
    PricingSection,
    BlogSection,
    ContactSection,
    FooterSection
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
