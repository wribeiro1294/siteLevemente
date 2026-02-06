<script setup>
import { ref } from 'vue'
import SignupModal from './components/SignupModal.vue'

// Dados para FAQ
const faqs = ref([
  {
    question: 'O que é o LeveMENTE?',
    answer: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    open: false
  },
  {
    question: 'Como funciona o programa?',
    answer: 'Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
    open: false
  },
  {
    question: 'Quais são os benefícios?',
    answer: 'Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.',
    open: false
  },
  {
    question: 'Como posso me inscrever?',
    answer: 'Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.',
    open: false
  }
])

// Dados para serviços
const services = ref([
  {
    icon: '🧘‍♀️',
    title: 'Bem-estar Mental',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt.'
  },
  {
    icon: '💪',
    title: 'Saúde Física',
    description: 'Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip.'
  },
  {
    icon: '🎯',
    title: 'Objetivos Personalizados',
    description: 'Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat.'
  }
])

const toggleFaq = (index) => {
  faqs.value[index].open = !faqs.value[index].open
}

// Signup modal visibility
const showSignup = ref(false)

const onSignup = (data) => {
  // handle submitted data (e.g., send to API). For now, just log.
  console.log('Signup submitted', data)
}
</script>

<template>
  <!-- Header -->
  <header class="header">
    <div class="container">
      <nav class="nav">
        <div class="logo">
          <span class="logo-text">LeveMENTE</span>
        </div>
        <ul class="nav-menu">
          <li><a href="#inicio">Início</a></li>
          <li><a href="#sobre">Sobre</a></li>
          <li><a href="#servicos">Serviços</a></li>
          <li><a href="#faq">FAQ</a></li>
          <li><a href="#contato">Contato</a></li>
        </ul>
        <button class="nav-cta">Começar Agora</button>
      </nav>
    </div>
  </header>

  <!-- Hero Section -->
  <section id="inicio" class="hero">
    <div class="container">
      <div class="hero-content">
        <div class="hero-text fade-up" style="animation-delay:120ms">
          <h1>Transforme sua vida com <span class="highlight">equilíbrio</span> e bem-estar</h1>
          <p class="hero-subtitle">Descubra o caminho para uma vida mais saudável, equilibrada e plena. Nossa abordagem integra saúde mental e física para resultados duradouros.</p>
          <div class="hero-buttons">
            <button class="btn-primary" @click="showSignup = true">Comece sua jornada</button>
            <button class="btn-secondary">Saiba mais</button>
          </div>
          <div class="hero-stats">
            <div class="stat">
              <span class="stat-number">2500+</span>
              <span class="stat-label">Pessoas transformadas</span>
            </div>
            <div class="stat">
              <span class="stat-number">98%</span>
              <span class="stat-label">Taxa de satisfação</span>
            </div>
          </div>
        </div>
  <div class="hero-image fade-up" style="animation-delay:240ms">
          <img src="https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Pessoa praticando exercícios" />
          <div class="hero-card">
            <div class="card-icon">✨</div>
            <div class="card-content">
              <h4>Resultado Garantido</h4>
              <p>Metodologia comprovada</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Serviços Section -->
  <section id="servicos" class="services">
    <div class="container">
      <div class="section-header">
        <h2>Nossos Serviços</h2>
        <p>Oferecemos uma abordagem completa para o seu bem-estar</p>
      </div>
      <div class="services-grid">
        <div v-for="service in services" :key="service.title" class="service-card">
          <div class="service-icon">{{ service.icon }}</div>
          <h3>{{ service.title }}</h3>
          <p>{{ service.description }}</p>
          <button class="service-btn">Saiba mais →</button>
        </div>
      </div>
    </div>
  </section>

  <!-- Sobre Section -->
  <section id="sobre" class="about">
    <div class="container">
      <div class="about-content">
        <div class="about-text">
          <div class="section-tag">Sobre nós</div>
          <h2>Transformando vidas através do equilíbrio</h2>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
          <div class="about-features">
            <div class="feature">
              <div class="feature-icon">✓</div>
              <span>Acompanhamento personalizado</span>
            </div>
            <div class="feature">
              <div class="feature-icon">✓</div>
              <span>Metodologia cientificamente comprovada</span>
            </div>
            <div class="feature">
              <div class="feature-icon">✓</div>
              <span>Resultados mensuráveis</span>
            </div>
          </div>
          <button class="btn-primary">Conheça nossa metodologia</button>
        </div>
        <div class="about-image">
          <img src="https://images.unsplash.com/photo-1544367567-0f2fcb009e0b?ixlib=rb-4.0.3&auto=format&fit=crop&w=500&q=80" alt="Equipe profissional" />
        </div>
      </div>
    </div>
  </section>

  <!-- FAQ Section -->
  <section id="faq" class="faq">
    <div class="container">
      <div class="section-header">
        <h2>Perguntas Frequentes</h2>
        <p>Tire suas principais dúvidas sobre nossos serviços</p>
      </div>
      <div class="faq-container">
        <div class="faq-list">
          <div v-for="(faq, index) in faqs" :key="index" class="faq-item">
            <button class="faq-question" @click="toggleFaq(index)">
              <span>{{ faq.question }}</span>
              <span class="faq-toggle" :class="{ 'open': faq.open }">+</span>
            </button>
            <div class="faq-answer" v-show="faq.open">
              <p>{{ faq.answer }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- CTA Section -->
  <section class="cta-section">
    <div class="container">
      <div class="cta-content">
        <h2>Pronto para transformar sua vida?</h2>
        <p>Comece sua jornada de bem-estar hoje mesmo e descubra o seu melhor potencial.</p>
        <button class="btn-primary large">Começar agora</button>
      </div>
    </div>
  </section>

  <SignupModal v-model:show="showSignup" @submitted="onSignup" />

  <!-- Footer -->
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-brand">
          <div class="logo">
            <span class="logo-text">LeveMENTE</span>
          </div>
          <p>Transformando vidas através do equilíbrio entre corpo e mente. Sua jornada de bem-estar começa aqui.</p>
          <div class="social-links">
            <a href="#" aria-label="Facebook">📘</a>
            <a href="#" aria-label="Instagram">📷</a>
            <a href="#" aria-label="LinkedIn">💼</a>
            <a href="#" aria-label="Twitter">🐦</a>
          </div>
        </div>
        <div class="footer-links">
          <div class="link-group">
            <h4>Navegação</h4>
            <ul>
              <li><a href="#inicio">Início</a></li>
              <li><a href="#sobre">Sobre</a></li>
              <li><a href="#servicos">Serviços</a></li>
              <li><a href="#faq">FAQ</a></li>
            </ul>
          </div>
          <div class="link-group">
            <h4>Serviços</h4>
            <ul>
              <li><a href="#">Bem-estar Mental</a></li>
              <li><a href="#">Saúde Física</a></li>
              <li><a href="#">Consultorias</a></li>
              <li><a href="#">Programas</a></li>
            </ul>
          </div>
          <div class="link-group">
            <h4>Contato</h4>
            <ul>
              <li><a href="#">(11) 99999-9999</a></li>
              <li><a href="#">contato@levemente.com</a></li>
            </ul>
          </div>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2026 LeveMENTE. Todos os direitos reservados.</p>
        <div class="footer-legal">
          <a href="#">Política de Privacidade</a>
          <a href="#">Termos de Uso</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
/* Reset e Importações */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  line-height: 1.6;
  color: #1e293b;
  background-color: #ffffff;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

/* Utility: full-bleed container for sections that must span the entire viewport width */
.container--full {
  max-width: 100%;
  padding-left: 48px;
  padding-right: 48px;
}

/* Tipografia */
h1, h2, h3, h4 {
  font-weight: 600;
  line-height: 1.2;
  color: #0f172a;
}

h1 { font-size: 3.5rem; }
h2 { font-size: 2.5rem; }
h3 { font-size: 1.5rem; }
h4 { font-size: 1.25rem; }

/* Motion */
.fade-up {
  opacity: 0;
  transform: translateY(12px);
  animation: fadeUp 700ms ease forwards;
}

@keyframes fadeUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Botões */
.btn-primary, .btn-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 12px 24px;
  border-radius: 8px;
  font-weight: 500;
  text-decoration: none;
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: 16px;
}

.btn-primary {
  background: linear-gradient(135deg, #22c55e 0%, #065f46 100%);
  color: white;
  box-shadow: 0 4px 14px 0 rgba(22, 163, 74, 0.25);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px 0 rgba(22, 163, 74, 0.35);
}

.btn-primary.large {
  padding: 16px 32px;
  font-size: 18px;
}

.btn-secondary {
  background: transparent;
  color: #16a34a;
  border: 2px solid #16a34a;
}

.btn-secondary:hover {
  background: #16a34a;
  color: white;
}

/* Header */
.header {
  position: fixed;
  top: 0;
  width: 100%;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid #e2e8f0;
  z-index: 1000;
}

.nav {
  /* Use grid to visually center the logo while keeping nav controls aligned to the right */
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  gap: 16px;
  padding: 16px 0;
}

.logo-text {
  font-size: 1.9rem;
  font-weight: 700;
  letter-spacing: 0.6px;
  background: linear-gradient(135deg, #22c55e 0%, #065f46 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  justify-self: center;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 28px;
  justify-self: end;
  align-items: center;
}

.nav-menu a {
  text-decoration: none;
  color: #334155;
  font-weight: 600;
  font-size: 0.95rem;
  transition: color 0.16s ease, transform 0.16s ease;
  padding: 6px 8px;
  border-radius: 8px;
}

.nav-menu a:hover {
  color: #065f46;
  transform: translateY(-2px);
}

.nav-cta {
  background: linear-gradient(135deg, #22c55e 0%, #065f46 100%);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.18s ease, box-shadow 0.18s ease;
  justify-self: end;
}

.nav-cta:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(6, 95, 70, 0.18);
}

/* Hero Section */
.hero {
  /* Make hero occupy the full viewport height minus the fixed header */
  padding: 24px 0 40px;
  min-height: calc(100vh - 72px);
  display: flex;
  align-items: center;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  overflow: hidden;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}

.hero-text h1 {
  margin-bottom: 24px;
  line-height: 1.02;
  font-size: 4rem;
  letter-spacing: -1px;
}

.highlight {
  background: linear-gradient(135deg, #10b981 0%, #065f46 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: 1.25rem;
  color: #334155;
  margin-bottom: 32px;
  line-height: 1.6;
}

.hero-buttons {
  display: flex;
  gap: 16px;
  margin-bottom: 48px;
}

.hero-stats {
  display: flex;
  gap: 32px;
}

.stat {
  display: flex;
  flex-direction: column;
}

.stat-number {
  font-size: 2rem;
  font-weight: 700;
  color: #16a34a;
}

.stat-label {
  font-size: 0.875rem;
  color: #334155;
}

.hero-image {
  position: relative;
}

.hero-image img {
  width: 100%;
  border-radius: 16px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

.hero-card {
  position: absolute;
  bottom: -20px;
  right: -20px;
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  display: flex;
  align-items: center;
  gap: 12px;
}

.card-icon {
  font-size: 2rem;
}

.card-content h4 {
  margin: 0;
  font-size: 1rem;
}

.card-content p {
  margin: 0;
  color: #334155;
  font-size: 0.875rem;
}

/* Serviços Section */
.services {
  padding: 150px 0; /* Increased padding to make the content more centered */
  background: #065f46; /* Keep the green background */
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-header h2 {
  margin-bottom: 16px;
  color: white; /* Set the title color to white */
}

.section-header p {
  font-size: 1.125rem;
  color: white; /* Set the subtitle color to white */
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 32px;
}

.service-card {
  background-color: #eff2f7; /* Set the card background to #eff2f7 */
  color: #1e293b; /* Adjust text color for contrast */
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.service-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

.service-card h3 {
  color: #0f172a; /* Darker text for better readability */
}

.service-card p {
  color: #475569; /* Subtle text color for descriptions */
}

.service-btn {
  color: #065f46; /* Green text for the button */
  font-weight: 600;
  text-decoration: underline;
  margin-top: 16px;
}

/* Sobre Section */
.about {
  padding: 100px 0;
  background: #f8fafc;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}

.section-tag {
  display: inline-block;
  background: #d1fae5;
  color: #065f46;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 0.875rem;
  font-weight: 500;
  margin-bottom: 16px;
}

.about-text h2 {
  margin-bottom: 24px;
}

.about-text p {
  color: #334155;
  margin-bottom: 32px;
  font-size: 1.125rem;
  line-height: 1.7;
}

.about-features {
  margin-bottom: 32px;
}

.feature {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 16px;
}

.feature-icon {
  width: 24px;
  height: 24px;
  background: #d1fae5;
  color: #065f46;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 14px;
}

.about-image img {
  width: 100%;
  border-radius: 16px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

/* FAQ Section */
.faq {
  padding: 100px 0;
  background: white;
}

.faq-container {
  max-width: 800px;
  margin: 0 auto;
}

.faq-item {
  margin-bottom: 16px;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  overflow: hidden;
  background: white;
}

.faq-question {
  width: 100%;
  padding: 24px;
  background: transparent;
  border: none;
  text-align: left;
  font-size: 1.125rem;
  font-weight: 500;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: background 0.2s ease;
}

.faq-question:hover {
  background: #f8fafc;
}

.faq-toggle {
  font-size: 1.5rem;
  font-weight: 300;
  color: #10b981;
  transition: transform 0.2s ease;
}

.faq-toggle.open {
  transform: rotate(45deg);
}

.faq-answer {
  padding: 0 24px 24px;
  color: #334155;
  line-height: 1.7;
}

.faq-answer p {
  margin: 0;
}
/* CTA Section */
.cta-section {
  padding: 100px 0;
  background: linear-gradient(135deg, #10b981 0%, #065f46 100%);
  text-align: center;
}

.cta-content h2 {
  color: white;
  margin-bottom: 16px;
  font-size: 2.5rem;
}

.cta-content p {
  color: rgba(255, 255, 255, 0.9);
  font-size: 1.25rem;
  margin-bottom: 32px;
}

.cta-content .btn-primary {
  background: white;
  color: #10b981;
}

.cta-content .btn-primary:hover {
  background: #f8fafc;
}

/* Footer */
.footer {
  background: #0f172a;
  color: #94a3b8;
  padding: 60px 0 0;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 48px;
  margin-bottom: 48px;
}

.footer-brand p {
  margin: 16px 0 24px;
  line-height: 1.6;
}

.social-links {
  display: flex;
  gap: 16px;
}

.social-links a {
  width: 40px;
  height: 40px;
  background: #1e293b;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.2s ease;
}

.social-links a:hover {
  background: #10b981;
}

.link-group h4 {
  color: white;
  margin-bottom: 16px;
}

.link-group ul {
  list-style: none;
}

.link-group li {
  margin-bottom: 8px;
}

.link-group a {
  color: #94a3b8;
  text-decoration: none;
  transition: color 0.2s ease;
}

.link-group a:hover {
  color: white;
}

.footer-bottom {
  border-top: 1px solid #1e293b;
  padding: 24px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-legal {
  display: flex;
  gap: 24px;
}

.footer-legal a {
  color: #94a3b8;
  text-decoration: none;
  transition: color 0.2s ease;
}

.footer-legal a:hover {
  color: white;
}

/* Responsividade */
@media (max-width: 1024px) {
  .hero-content,
  .about-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  /* Stack hero image above text on narrower desktops/tablets for better composition */
  .hero-image {
    order: -1;
    max-width: 720px;
    margin: 0 auto;
  }

  .hero-text h1 {
    font-size: 3rem;
    line-height: 1.06;
  }

  .hero {
    padding: 80px 0 60px;
    min-height: calc(100vh - 72px);
  }

  .footer-content {
    grid-template-columns: 1fr 1fr;
    gap: 32px;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 0 16px;
  }

  /* Mobile-friendly nav stacking */
  .nav {
    display: flex;
    flex-direction: column;
    gap: 12px;
    align-items: stretch;
  }

  .nav-menu {
    gap: 18px;
    justify-content: center;
    flex-wrap: wrap;
  }

  .nav-cta {
    justify-self: center;
    align-self: center;
  }

  /* Reduce hero footprint on mobile */
  .hero {
    padding: 88px 0 48px;
    min-height: auto;
  }

  h1 { font-size: 2.25rem; }
  h2 { font-size: 1.75rem; }

  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .hero-text {
    margin-bottom: 24px;
  }

  .hero-buttons {
    justify-content: center;
  }

  .hero-stats {
    justify-content: center;
    flex-wrap: wrap;
  }

  .hero-image {
    display: flex;
    justify-content: center;
    margin-top: 24px;
  }

  .hero-image img {
    max-width: 80%;
    height: auto;
  }

  .hero-card {
    position: static;
    margin-top: 16px;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }

  .service-card {
    padding: 28px 18px;
    border-radius: 16px;
  }

  .footer-content {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .footer-bottom {
    flex-direction: column;
    gap: 16px;
    text-align: center;
  }
}

@media (max-width: 480px) {
  .hero-buttons {
    align-items: center;
    gap: 12px;
  }

  .btn-primary, .btn-secondary {
    width: 100%;
    justify-content: center;
    padding: 12px 18px;
    font-size: 15px;
  }

  .hero-text h1 {
    font-size: 1.85rem;
    line-height: 1.08;
  }

  .hero-subtitle {
    font-size: 1rem;
  }
}
</style>
