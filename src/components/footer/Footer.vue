<template>
  <footer class="footer-section">
    <div class="footer-container">
      <div class="footer-content">
        <div class="footer-brand">
          <h2 class="footer-logo">ARCHVIZ</h2>
          <p class="footer-description">
            Transformando ideias em realidade digital através de soluções inovadoras e design excepcional.
          </p>
          <div class="social-links">
            <a href="#" class="social-link">
              <i class="fab fa-instagram"></i>
            </a>
            <a href="#" class="social-link">
              <i class="fab fa-linkedin"></i>
            </a>
            <a href="#" class="social-link">
              <i class="fab fa-behance"></i>
            </a>
          </div>
        </div>

        <div class="footer-links">
          <div class="footer-group">
            <h3>Empresa</h3>
            <ul>
              <li><a href="#sobre">Sobre</a></li>
              <li><a href="#servicos">Serviços</a></li>
              <li><a href="#portfolio">Portfólio</a></li>
              <li><a href="#contato">Contato</a></li>
            </ul>
          </div>

          <div class="footer-group">
            <h3>Serviços</h3>
            <ul>
              <li><a href="#visualizacao">Visualização 3D</a></li>
              <li><a href="#realidade-virtual">Realidade Virtual</a></li>
              <li><a href="#animacao">Animação</a></li>
              <li><a href="#consultoria">Consultoria</a></li>
            </ul>
          </div>

          <div class="footer-group">
            <h3>Legal</h3>
            <ul>
              <li><a href="#privacidade">Privacidade</a></li>
              <li><a href="#termos">Termos de Uso</a></li>
              <li><a href="#cookies">Cookies</a></li>
            </ul>
          </div>
        </div>
      </div>

      <div class="footer-bottom">
        <p class="copyright">
          © {{ currentYear }} ARCHVIZ. Todos os direitos reservados.
        </p>
      </div>
    </div>
  </footer>
</template>

<script>
import './Footer.css'

export default {
  name: 'FooterSection',
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  }
}
</script> 