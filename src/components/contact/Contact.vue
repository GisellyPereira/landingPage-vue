<template>
  <section class="contact-section">
    <div class="contact-container">
      <div class="contact-header">
        <h2 class="contact-title">Entre em Contato</h2>
        <div class="title-accent"></div>
        <p class="contact-subtitle">
          Estamos prontos para transformar sua visão em realidade. Entre em contato conosco.
        </p>
      </div>

      <div class="contact-content">
        <div class="contact-info">
          <div class="info-item">
            <div class="info-icon">📍</div>
            <div class="info-text">
              <h3>Localização</h3>
              <p>Av. Paulista, 1000 - São Paulo, SP</p>
            </div>
          </div>
          
          <div class="info-item">
            <div class="info-icon">📞</div>
            <div class="info-text">
              <h3>Telefone</h3>
              <p>+55 (11) 9999-9999</p>
            </div>
          </div>
          
          <div class="info-item">
            <div class="info-icon">✉️</div>
            <div class="info-text">
              <h3>Email</h3>
              <p>contato@archviz.com</p>
            </div>
          </div>
        </div>

        <form class="contact-form" @submit.prevent="handleSubmit">
          <div class="form-grid">
            <div class="form-group">
              <label for="name">Nome</label>
              <input 
                type="text" 
                id="name" 
                v-model="form.name"
                :class="{ 'error': errors.name }"
                placeholder="Seu nome completo"
              >
              <span class="error-message" v-if="errors.name">{{ errors.name }}</span>
            </div>

            <div class="form-group">
              <label for="email">Email</label>
              <input 
                type="email" 
                id="email" 
                v-model="form.email"
                :class="{ 'error': errors.email }"
                placeholder="seu@email.com"
              >
              <span class="error-message" v-if="errors.email">{{ errors.email }}</span>
            </div>

            <div class="form-group full-width">
              <label for="subject">Assunto</label>
              <input 
                type="text" 
                id="subject" 
                v-model="form.subject"
                :class="{ 'error': errors.subject }"
                placeholder="Assunto da mensagem"
              >
              <span class="error-message" v-if="errors.subject">{{ errors.subject }}</span>
            </div>

            <div class="form-group full-width">
              <label for="message">Mensagem</label>
              <textarea 
                id="message" 
                v-model="form.message"
                :class="{ 'error': errors.message }"
                placeholder="Sua mensagem"
                rows="6"
              ></textarea>
              <span class="error-message" v-if="errors.message">{{ errors.message }}</span>
            </div>
          </div>

          <button type="submit" class="submit-button" :disabled="isSubmitting">
            {{ isSubmitting ? 'Enviando...' : 'Enviar Mensagem' }}
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
import './Contact.css'

export default {
  name: 'ContactSection',
  data() {
    return {
      isSubmitting: false,
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      errors: {}
    }
  },
  methods: {
    validateForm() {
      this.errors = {}
      
      if (!this.form.name.trim()) {
        this.errors.name = 'Nome é obrigatório'
      }
      
      if (!this.form.email.trim()) {
        this.errors.email = 'Email é obrigatório'
      } else if (!this.isValidEmail(this.form.email)) {
        this.errors.email = 'Email inválido'
      }
      
      if (!this.form.subject.trim()) {
        this.errors.subject = 'Assunto é obrigatório'
      }
      
      if (!this.form.message.trim()) {
        this.errors.message = 'Mensagem é obrigatória'
      }
      
      return Object.keys(this.errors).length === 0
    },
    
    isValidEmail(email) {
      return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
    },
    
    async handleSubmit() {
      if (!this.validateForm()) return
      
      this.isSubmitting = true
      
      try {
        // Simular envio
        await new Promise(resolve => setTimeout(resolve, 1500))
        
        // Limpar formulário
        this.form = {
          name: '',
          email: '',
          subject: '',
          message: ''
        }
        
        alert('Mensagem enviada com sucesso!')
      } catch (error) {
        alert('Erro ao enviar mensagem. Tente novamente.')
      } finally {
        this.isSubmitting = false
      }
    }
  }
}
</script> 