<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import SignupModal from './components/SignupModal.vue'

// Mobile menu state
const isMobileMenuOpen = ref(false)

// Scroll state for header
const isScrolled = ref(false)

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}

// Handle scroll for header background
const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

// Dados para FAQ
const faqs = ref([
  {
    question: 'Sobre o projeto',
    answer: 'Esse não é mais um daqueles desafios que prometem a perda de peso em um prazo curto de tempo. É um projeto para a vida toda,dito isso é com imenso orgulho e satisfação que apresentamos o PROJETO LEVEMENTE A ideia surgiu baseada em experiências pessoais na luta contra a obesidade e com isso a percepção da necessidade de um acompanhamento completo, corpo e mente, para que não seja apenas mais uma promessa de mudança de vida esquecida no bloco de metas anual. Nosso objetivo é proporcionar sua transformação sustentável através de orientações, informações e autonomia',
    open: true
  },
  {
    question: 'Como funciona o programa?',
    answer: 'Serão 15 dias de acompanhamento com profissionais especializados em emagrecimento com conteúdos exclusivos sobre alimentação, atividade fisica e saúde mental. Você terá acesso a um cardápio, receitas práticas e fáceis, uma planilha de treinos para serem feitos em casa ou na academia e suporte psicológico para que essa jornada seja leve e mentalmente saudável. Após os 15 dias todo material compartilhado continuará sendo seu! E teremos premiações pra quem tiver o melhor desempenho durante esse período.',
    open: false
  },
  {
    question: 'Jornada',
    answer: 'INICIO: 23/02/2026   FIM: 09/03/2026',
    open: false
  },
  
  {
    question: 'Investimento',
    answer: 'R$ 49,90',
    open: false
  },
  {
    question: 'Como posso me inscrever?',
    answer: 'Preencha o nosso formulário e aguarde o nosso contato. ',
    open: false
  }
])

// Dados para serviços
const services = ref([
  {
    title: '',
    description: 'A importância do sono na recuperação e nos resultados de saúde.'
  },
  {
    title: '',
    description: 'Compras no supermercado: o que colocar no carrinho para uma rotina saudável.'
  },
  {
    title: '',
    description: 'Fome física vs. Fome emocional:aprendendo a diferenciar.'
  },
  {
    title: '',
    description: 'Folha de registro de todas as refeições, com local e data. PSICOEDUCAÇÃO SOBRE.'
  },
  {
    title: '',
    description: 'Benefícios dos alimentos integrais e como incluí-los na rotina.'
  },
  {
    title: '',
    description: 'Benefícios dos alimentos integrais e como incluí-los na rotinaComo transformar pequenas vitórias em grandes hábitos (reforço positivo).'
  },
   {
    title: '',
    description: 'Aula de alongamento e mobilidade para fazer em casa.'
  }
])

const toggleFaq = (index) => {
  faqs.value[index].open = !faqs.value[index].open
}

// Signup modal visibility
const showSignup = ref(false)

const onSignup = (data) => {
  console.log('Signup submitted', data)
}
</script>

<template>
  <!-- Header -->
  <header class="header" :class="{ 'header--scrolled': isScrolled }">
    <div class="container">
      <nav class="nav">
        <!-- Logo -->
        <div class="logo">
          <span class="logo-text">
            <span class="logo-left">LEVE</span>
            <span class="logo-right">MENTE</span>
          </span>
        </div>

        <!-- Desktop Navigation -->
        <ul class="nav-menu">
          <li><a href="#inicio" @click="closeMobileMenu">Início</a></li>
          <li><a href="#sobre" @click="closeMobileMenu">Sobre</a></li>
          <li><a href="#conteudos" @click="closeMobileMenu">Conteúdos</a></li>
          <li><a href="#faq" @click="closeMobileMenu">FAQ</a></li>
        </ul>

        <!-- Mobile Menu Button -->
        <button 
          class="mobile-menu-btn"
          :class="{ 'mobile-menu-btn--active': isMobileMenuOpen }"
          @click="toggleMobileMenu"
          aria-label="Toggle menu"
          aria-expanded="isMobileMenuOpen"
        >
          <span class="mobile-menu-btn__line"></span>
          <span class="mobile-menu-btn__line"></span>
          <span class="mobile-menu-btn__line"></span>
        </button>

        <!-- Mobile Navigation -->
        <div 
          class="mobile-nav"
          :class="{ 'mobile-nav--open': isMobileMenuOpen }"
        >
          <ul class="mobile-nav__menu">
            <li><a href="#inicio" @click="closeMobileMenu">Início</a></li>
            <li><a href="#sobre" @click="closeMobileMenu">Sobre</a></li>
            <li><a href="#conteudos" @click="closeMobileMenu">Conteúdos</a></li>
            <li><a href="#faq" @click="closeMobileMenu">FAQ</a></li>
          </ul>
        </div>

      </nav>
    </div>

    <!-- Mobile Menu Overlay -->
    <div 
      v-if="isMobileMenuOpen" 
      class="mobile-nav-overlay"
      @click="closeMobileMenu"
    ></div>
  </header>

  <!-- Hero Section -->
  <section id="inicio" class="hero section-hero">
    <div class="container">
      <div class="hero-content">
        <div class="hero-text fade-up" style="animation-delay: 120ms">
          <h1> <span class="highlight">Mudança</span> da mente com <span class="highlight">leveza</span>.</h1>
          <p class="hero-subtitle">
            Descubra o caminho para uma vida mais saudável, equilibrada e sustentável. 
            Nossa abordagem integra saúde mental e física para resultados reais e duradouros.
          </p>
          <div class="hero-buttons">
            <button class="btn-primary btn-hero" @click="showSignup = true">
              Comece sua jornada
            </button>
            <a href="#faq" class="btn-secondary">Saiba mais</a>
          </div>
        </div>
        
        <div class="hero-image fade-up" style="animation-delay: 240ms">
          <div class="hero-image-container">
            <img 
              src="https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" 
              alt="Pessoa praticando exercícios"
              loading="eager"
            />
            <div class="hero-card">
              <div class="card-icon">✨</div>
              <div class="card-content">
                <h4>Resultado Garantido</h4>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <!-- Sobre Section -->
  <section id="sobre" class="about section-standard">
    <div class="container">
      <div class="about-content">
        <div class="about-text fade-up">
          <div class="section-tag">Sobre nós</div>
          <h2>Transformando vidas através do equilíbrio</h2>
          <p class="text-lead">
            Te ajudaremos a ter uma rotina funcional, disciplina e constância. 
            Introduzindo hábitos saudáveis que irão sustentar todo o seu processo.
          </p>
          <div class="about-features">
            <div class="feature">
              <div class="feature-icon">✓</div>
              <span>Acompanhamento personalizado</span>
            </div>
            <div class="feature">
              <div class="feature-icon">✓</div>
              <span>Metodologia comprovada</span>
            </div>
            <div class="feature">
              <div class="feature-icon">✓</div>
              <span>Resultados mensuráveis</span>
            </div>
          </div>
        </div>
        <div class="about-image fade-up" style="animation-delay: 200ms">
          <img 
            src="https://images.unsplash.com/photo-1544367567-0f2fcb009e0b?ixlib=rb-4.0.3&auto=format&fit=crop&w=500&q=80" 
            alt="Equipe profissional"
            loading="lazy"
          />
        </div>
      </div>
      
      <!-- Team Section -->
      <div class="team-section">
        <h2 class="team-title text-center">Nossos Profissionais</h2>
        <div class="team-grid">
          <div class="team-card team-card--alt fade-up" style="animation-delay: 100ms">
            <div class="team-photo-wrapper">
              <img 
                src="/images/profissionais/thaissa.png" 
                alt="Thaissa - Nutricionista" 
                class="team-photo team-photo--thaissa" 
                loading="lazy"
              />
            </div>
            <div class="team-info">
              <h3>Thaissa</h3>
              <p>Nutricionista</p>
              <div class="team-social">
                <a 
                  href="https://www.instagram.com/thaissanut/" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  aria-label="Instagram da Thaissa"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
                    <path d="M7 2C4.243 2 2 4.243 2 7v10c0 2.757 2.243 5 5 5h10c2.757 0 5-2.243 5-5V7c0-2.757-2.243-5-5-5H7zm10 2c1.654 0 3 1.346 3 3v10c0 1.654-1.346 3-3 3H7c-1.654 0-3-1.346-3-3V7c0-1.654 1.346-3 3-3h10zM12 7a5 5 0 100 10 5 5 0 000-10zm0 2a3 3 0 110 6 3 3 0 010-6zM17.5 6.5a1 1 0 110 2 1 1 0 010-2z"/>
                  </svg>
                </a>
              </div>
            </div>
          </div>
          
          <div class="team-card team-card--alt fade-up" style="animation-delay: 200ms">
            <div class="team-photo-wrapper">
              <img 
                src="/images/profissionais/wilka.jpeg" 
                alt="Wilka - Psicóloga" 
                class="team-photo team-photo--wilka" 
                loading="lazy"
              />
            </div>
            <div class="team-info">
              <h3>Wilka</h3>
              <p>Psicóloga</p>
              <div class="team-social">
                <a 
                  href="https://www.instagram.com/wilkacordeiro/" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  aria-label="Instagram da Wilka"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
                    <path d="M7 2C4.243 2 2 4.243 2 7v10c0 2.757 2.243 5 5 5h10c2.757 0 5-2.243 5-5V7c0-2.757-2.243-5-5-5H7zm10 2c1.654 0 3 1.346 3 3v10c0 1.654-1.346 3-3 3H7c-1.654 0-3-1.346-3-3V7c0-1.654 1.346-3 3-3h10zM12 7a5 5 0 100 10 5 5 0 000-10zm0 2a3 3 0 110 6 3 3 0 010-6zM17.5 6.5a1 1 0 110 2 1 1 0 010-2z"/>
                  </svg>
                </a>
              </div>
            </div>
          </div>
          
          <div class="team-card team-card--alt fade-up" style="animation-delay: 300ms">
            <div class="team-photo-wrapper">
              <img 
                src="/images/profissionais/gabriel.png" 
                alt="Gabriel - Personal Trainer" 
                class="team-photo team-photo--gabriel"
                loading="lazy"
              />
            </div>
            <div class="team-info">
              <h3>Gabriel</h3>
              <p>Personal Trainer</p>
              <div class="team-social">
                <a 
                  href="https://www.instagram.com/gabriel_linharesm/" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  aria-label="Instagram do Gabriel"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
                    <path d="M7 2C4.243 2 2 4.243 2 7v10c0 2.757 2.243 5 5 5h10c2.757 0 5-2.243 5-5V7c0-2.757-2.243-5-5-5H7zm10 2c1.654 0 3 1.346 3 3v10c0 1.654-1.346 3-3 3H7c-1.654 0-3-1.346-3-3V7c0-1.654 1.346-3 3-3h10zM12 7a5 5 0 100 10 5 5 0 000-10zm0 2a3 3 0 110 6 3 3 0 010-6zM17.5 6.5a1 1 0 110 2 1 1 0 010-2z"/>
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>


    <!-- Serviços Section -->
  <section id="conteudos" class="services section-standard">
    <div class="container">
      <div class="section-header text-center">
        <h2>CONTEÚDOS COMO:</h2>
      </div>
      <div class="services-grid grid-auto-fit-md">
        <div 
          v-for="(service, index) in services" 
          :key="index" 
          class="service-card fade-up"
          :style="{ animationDelay: `${index * 100 + 200}ms` }"
        >
          <div class="service-content">
            <h3 v-if="service.title">{{ service.title }}</h3>
            <p>{{ service.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- FAQ Section -->
  <section id="faq" class="faq section-standard">
    <div class="container">
      <div class="section-header text-center">
        <h2>Perguntas Frequentes</h2>
      </div>
      <div class="faq-container">
        <div class="faq-list">
          <div 
            v-for="(faq, index) in faqs" 
            :key="index" 
            class="faq-item fade-up"
            :style="{ animationDelay: `${index * 100 + 200}ms` }"
          >
            <button 
              class="faq-question" 
              @click="toggleFaq(index)"
              :aria-expanded="faq.open"
              :aria-controls="`faq-answer-${index}`"
            >
              <span>{{ faq.question }}</span>
              <span class="faq-toggle" :class="{ 'open': faq.open }">+</span>
            </button>
            <div 
              v-show="faq.open" 
              class="faq-answer"
              :id="`faq-answer-${index}`"
            >
              <p>{{ faq.answer }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- CTA Section -->
  <section class="cta-section section-standard">
    <div class="container text-center">
      <div class="cta-content fade-up">
        <h2>Pronto para transformar sua vida?</h2>
        <p>Comece sua jornada de bem-estar hoje mesmo e descubra o seu melhor potencial.</p>
        <button class="btn-primary btn-hero" @click="showSignup = true">
          Começar agora
        </button>
      </div>
    </div>
  </section>

  <SignupModal 
    v-model:show="showSignup" 
    :appsScriptUrl="'https://script.google.com/macros/s/AKfycbx1zj8l1ixBnhzw7loNTP4fuCX8npyH5EPdM6aC2YR-KbPZKWqAvCKrUtgnMMFDVlXJ8g/exec'" 
    @submitted="onSignup" 
  />

  <!-- Footer -->
  <footer class="footer section-standard">
    <div class="container">
      <div class="footer-content">
        <div class="footer-brand">
          <div class="logo">
            <span class="logo-text">
              <span class="logo-left">LEVE</span>
              <span class="logo-right">MENTE</span>
            </span>
          </div>
          <p style="color:white">Transformando vidas através do equilíbrio entre corpo e mente. Sua jornada de bem-estar começa aqui.</p>
          <div class="social-links">
          </div>
        </div>
        
        <div class="link-group">
          <h4>Navegação</h4>
          <ul>
            <li><a href="#inicio">Início</a></li>
            <li><a href="#sobre">Sobre</a></li>
            <li><a href="#conteudos">Conteúdos</a></li>
            <li><a href="#faq">FAQ</a></li>
          </ul>
        </div>
        
        <div class="link-group">
          <h4>Contato</h4>
          <ul>
            <li>pjlevemente@gmail.com</li>
          </ul>
        </div>
      </div>
      
      <div class="footer-bottom">
        <p style="color:white">&copy; 2026 desenvolvido por TEMET DESENVOLVIMENTO.</p>
        <div class="footer-legal">
          <a href="#">Política de Privacidade</a>
          <a href="#">Termos de Uso</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
/* ============================================
   IMPORTS AND SETUP
   ============================================ */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

/* ============================================
   HEADER AND NAVIGATION
   ============================================ */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--color-border);
  z-index: var(--z-fixed);
  transition: all var(--transition-normal);
  height: var(--header-height);
}

.header--scrolled {
  background: rgba(255, 255, 255, 0.98);
  box-shadow: var(--shadow-md);
}

.nav {
  display: flex;
  align-items: center;
  /* cluster logo and links closer together */
  justify-content: flex-start;
  height: var(--header-height);
  position: relative;
}

/* Logo */
.logo-text {
  font-size: clamp(1.5rem, 4vw, 1.9rem);
  font-weight: 700;
  letter-spacing: 0.6px;
  display: inline-block;
  line-height: 1;
}

.logo-left {
  color: #3f4337;
}

.logo-right {
  color: #afc09e;
  margin-left: 6px;
}

/* Desktop Navigation */
.nav-menu {
  display: none;
  list-style: none;
  /* reduce gap so links are closer together */
  gap: var(--space-3);
  align-items: center;
  margin: 0;
  padding: 0;
  /* small left margin to visually separate from logo */
  margin-left: var(--space-4);
}

.nav-menu a {
  text-decoration: none;
  color: var(--color-text);
  font-weight: 500;
  font-size: var(--font-size-base);
  transition: all var(--transition-fast);
  padding: var(--space-2) var(--space-3);
  border-radius: 8px;
  position: relative;
}

.nav-menu a:hover {
  color: var(--color-primary-dark);
  background: var(--color-primary-50);
  transform: translateY(-1px);
}

/* Desktop CTA Button removed - styles cleaned up */

/* Mobile Menu Button */
.mobile-menu-btn {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 44px;
  height: 44px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 8px;
  z-index: var(--z-modal);
  transition: all var(--transition-normal);
}

.mobile-menu-btn__line {
  display: block;
  height: 3px;
  width: 100%;
  background: var(--color-text);
  border-radius: 2px;
  transition: all var(--transition-normal);
  transform-origin: center;
}

.mobile-menu-btn--active .mobile-menu-btn__line:nth-child(1) {
  transform: rotate(45deg) translate(6px, 6px);
}

.mobile-menu-btn--active .mobile-menu-btn__line:nth-child(2) {
  opacity: 0;
  transform: scale(0);
}

.mobile-menu-btn--active .mobile-menu-btn__line:nth-child(3) {
  transform: rotate(-45deg) translate(6px, -6px);
}

/* Mobile Navigation */
.mobile-nav {
  position: fixed;
  top: var(--header-height);
  left: 0;
  right: 0;
  background: var(--color-white);
  border-bottom: 1px solid var(--color-border);
  max-height: 0;
  overflow: hidden;
  transition: all var(--transition-normal);
  z-index: var(--z-dropdown);
}

.mobile-nav--open {
  max-height: calc(100vh - var(--header-height));
  box-shadow: var(--shadow-lg);
}

.mobile-nav__menu {
  list-style: none;
  padding: var(--space-4) 0;
  margin: 0;
}

.mobile-nav__menu li {
  padding: 0 var(--container-padding);
}

.mobile-nav__menu a {
  display: block;
  padding: var(--space-4) 0;
  color: var(--color-text);
  text-decoration: none;
  font-weight: 500;
  font-size: var(--font-size-lg);
  border-bottom: 1px solid var(--color-border);
  transition: all var(--transition-fast);
}

.mobile-nav__menu a:hover {
  color: var(--color-primary);
  padding-left: var(--space-2);
}

/* mobile nav CTA removed - no styles needed */

/* Mobile Navigation Overlay */
.mobile-nav-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  z-index: var(--z-modal-backdrop);
  opacity: 0;
  animation: fadeIn 0.3s ease forwards;
}

/* ============================================
   RESPONSIVE NAVIGATION BEHAVIOR
   ============================================ */

/* Show desktop nav on tablets and up */
@media (min-width: 768px) {
  .nav-menu {
    display: flex;
  }
  
  .mobile-menu-btn {
    display: none;
  }
  
  .mobile-nav {
    display: none;
  }
}

/* Adjust logo size for small screens */
@media (max-width: 479px) {
  .logo-text {
    font-size: 1.4rem;
  }
  
  .nav {
    padding: 0 var(--space-2);
  }
}

/* ============================================
   HERO SECTION
   ============================================ */
.hero {
  background: #d5ddc8;
  overflow: hidden;
  position: relative;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-10);
  align-items: center;
  min-height: calc(100vh - var(--header-height));
}

.hero-text {
  text-align: center;
  max-width: 100%;
}

.hero-text h1 {
  margin-bottom: var(--space-6);
  line-height: 1.1;
  font-size: var(--font-size-4xl);
  letter-spacing: -0.02em;
}

.highlight {
  background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-primary-dark) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  display: inline-block;
}

.hero-subtitle {
  font-size: var(--font-size-lg);
  color: var(--color-text-muted);
  margin-bottom: var(--space-8);
  line-height: 1.6;
  max-width: 100%;
}

.hero-buttons {
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
  align-items: center;
  margin-bottom: var(--space-8);
}

.hero-image {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.hero-image-container {
  position: relative;
  max-width: 100%;
  width: 100%;
}

.hero-image img {
  width: 100%;
  height: auto;
  border-radius: 16px;
  box-shadow: var(--shadow-xl);
  display: block;
}

.hero-card {
  position: absolute;
  bottom: -10px;
  right: -10px;
  background: white;
  padding: var(--space-4) var(--space-5);
  border-radius: 12px;
  box-shadow: var(--shadow-lg);
  display: flex;
  align-items: center;
  gap: var(--space-3);
  max-width: calc(100% - 20px);
}

.card-icon {
  font-size: 1.5rem;
  flex-shrink: 0;
}

.card-content h4 {
  margin: 0;
  font-size: var(--font-size-sm);
  white-space: nowrap;
}

/* ============================================
   HERO RESPONSIVE DESIGN
   ============================================ */

/* Small devices (480px and up) */
@media (min-width: 480px) {
  .hero-buttons {
    flex-direction: row;
    justify-content: center;
  }
  
  .hero-card {
    bottom: -15px;
    right: -15px;
    padding: var(--space-5) var(--space-6);
  }
  
  .card-content h4 {
    font-size: var(--font-size-base);
  }
}

/* Medium devices (768px and up) - Tablets */
@media (min-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr 1fr;
    gap: var(--space-12);
    text-align: left;
  }
  
  .hero-text {
    text-align: left;
  }
  
  .hero-buttons {
    justify-content: flex-start;
  }
  
  .hero-image {
    order: 2;
  }
  
  .hero-text {
    order: 1;
  }
}

/* Large devices (1024px and up) - Desktops */
@media (min-width: 1024px) {
  .hero-content {
    gap: var(--space-16);
  }
  
  .hero-card {
    bottom: -20px;
    right: -20px;
    padding: var(--space-6);
  }
  
  .card-icon {
    font-size: 2rem;
  }
  
  .card-content h4 {
    font-size: var(--font-size-lg);
  }
}

/* Extra large devices (1280px and up) - Large Desktops */
@media (min-width: 1280px) {
  .hero-content {
    gap: var(--space-20);
  }
}

/* 2XL devices (1536px and up) - TVs and very large screens */
@media (min-width: 1536px) {
  .hero-content {
    gap: var(--space-24);
  }
  
  .hero-text h1 {
    font-size: var(--font-size-5xl);
  }
  
  .hero-subtitle {
    font-size: var(--font-size-xl);
  }
}

/* FAQ Section */
.faq {
  background: white;
}

/* Reduce vertical gap between the 'Conteúdos' section and FAQ to bring them closer visually. */
.faq.section-standard {
  /* keep overall padding but reduce the top spacing specifically for this section */
  padding-top: clamp(1.5rem, 4vw, 3rem);
}

.faq-container {
  max-width: 800px;
  margin: 0 auto;
}

.faq-item {
  margin-bottom: var(--space-4);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  overflow: hidden;
  background: white;
  transition: all var(--transition-fast);
}

.faq-item:hover {
  border-color: var(--color-primary-200);
  box-shadow: var(--shadow-sm);
}

.faq-question {
  width: 100%;
  padding: var(--space-6);
  background: transparent;
  border: none;
  text-align: left;
  font-size: var(--font-size-lg);
  font-weight: 500;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  transition: all var(--transition-fast);
  color: var(--color-heading);
  gap: var(--space-4);
}

.faq-question:hover {
  background: var(--color-gray-50);
}

.faq-toggle {
  font-size: 1.5rem;
  font-weight: 300;
  color: var(--color-primary);
  transition: transform var(--transition-normal);
  flex-shrink: 0;
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.faq-toggle.open {
  transform: rotate(45deg);
}

.faq-answer {
  padding: 0 var(--space-6) var(--space-6);
  color: var(--color-text-muted);
  line-height: 1.7;
}

/* CTA Section */
.cta-section {
  background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-primary-dark) 100%);
  position: relative;
  overflow: hidden;
}

.cta-content h2 {
  color: white;
  margin-bottom: var(--space-4);
}

.cta-content p {
  color: rgba(255, 255, 255, 0.9);
  font-size: var(--font-size-lg);
  margin-bottom: var(--space-8);
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.cta-content .btn-primary {
  background: white;
  color: var(--color-primary);
}

.cta-content .btn-primary:hover {
  background: var(--color-gray-50);
  transform: translateY(-3px);
}

/* Footer */
.footer {
  background: var(--color-gray-900);
  color: var(--color-gray-400);
}

.footer-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-8);
  margin-bottom: var(--space-12);
}

.footer-brand {
  text-align: center;
}

.footer-brand p {
  margin: var(--space-4) 0 var(--space-6);
  line-height: 1.6;
}

.social-links {
  display: flex;
  gap: var(--space-4);
  justify-content: center;
}

.link-group {
  text-align: center;
}

.link-group h4 {
  color: white;
  margin-bottom: var(--space-4);
}

.link-group ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.link-group li {
  margin-bottom: var(--space-2);
}

.link-group a {
  color: var(--color-gray-400);
  text-decoration: none;
  transition: color var(--transition-fast);
}

.link-group a:hover {
  color: white;
}

.footer-bottom {
  border-top: 1px solid var(--color-gray-800);
  padding-top: var(--space-6);
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
  align-items: center;
  text-align: center;
}

.footer-legal {
  display: flex;
  gap: var(--space-6);
  flex-wrap: wrap;
  justify-content: center;
}

.footer-legal a {
  color: var(--color-gray-400);
  text-decoration: none;
  transition: color var(--transition-fast);
}

.footer-legal a:hover {
  color: white;
}

/* Responsive adjustments */
@media (max-width: 479px) {
  .faq-question {
    padding: var(--space-4);
    font-size: var(--font-size-base);
  }
  
  .faq-answer {
    padding: 0 var(--space-4) var(--space-4);
  }
}

@media (min-width: 768px) {
  .footer-content {
    grid-template-columns: 2fr 1fr 1fr;
    text-align: left;
  }
  
  .footer-brand {
    text-align: left;
  }
  
  .social-links {
    justify-content: flex-start;
  }
  
  .link-group {
    text-align: left;
  }
  
  .footer-bottom {
    flex-direction: row;
    justify-content: space-between;
    text-align: left;
  }
}

@media (min-width: 1024px) {
  .footer-content {
    grid-template-columns: 2fr 1fr 1fr 1fr;
  }
}
.hero {
  background: #d5ddc8;
  overflow: hidden;
  position: relative;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-10);
  align-items: center;
  min-height: calc(100vh - var(--header-height));
}

.hero-text {
  text-align: center;
  max-width: 100%;
}

.hero-text h1 {
  margin-bottom: var(--space-6);
  line-height: 1.1;
  font-size: var(--font-size-4xl);
  letter-spacing: -0.02em;
}

.highlight {
  background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-primary-dark) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  display: inline-block;
}

.hero-subtitle {
  font-size: var(--font-size-lg);
  color: var(--color-text-muted);
  margin-bottom: var(--space-8);
  line-height: 1.6;
  max-width: 100%;
}

.hero-buttons {
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
  align-items: center;
  margin-bottom: var(--space-8);
}

.hero-image {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.hero-image-container {
  position: relative;
  max-width: 100%;
  width: 100%;
}

.hero-image img {
  width: 100%;
  height: auto;
  border-radius: 16px;
  box-shadow: var(--shadow-xl);
  display: block;
}

.hero-card {
  position: absolute;
  bottom: -10px;
  right: -10px;
  background: white;
  padding: var(--space-4) var(--space-5);
  border-radius: 12px;
  box-shadow: var(--shadow-lg);
  display: flex;
  align-items: center;
  gap: var(--space-3);
  max-width: calc(100% - 20px);
}

.card-icon {
  font-size: 1.5rem;
  flex-shrink: 0;
}

.card-content h4 {
  margin: 0;
  font-size: var(--font-size-sm);
  white-space: nowrap;
}

/* ============================================
   HERO RESPONSIVE DESIGN
   ============================================ */

/* Small devices (480px and up) */
@media (min-width: 480px) {
  .hero-buttons {
    flex-direction: row;
    justify-content: center;
  }
  
  .hero-card {
    bottom: -15px;
    right: -15px;
    padding: var(--space-5) var(--space-6);
  }
  
  .card-content h4 {
    font-size: var(--font-size-base);
  }
}

/* Medium devices (768px and up) - Tablets */
@media (min-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr 1fr;
    gap: var(--space-12);
    text-align: left;
  }
  
  .hero-text {
    text-align: left;
  }
  
  .hero-buttons {
    justify-content: flex-start;
  }
  
  .hero-image {
    order: 2;
  }
  
  .hero-text {
    order: 1;
  }
}

/* Large devices (1024px and up) - Desktops */
@media (min-width: 1024px) {
  .hero-content {
    gap: var(--space-16);
  }
  
  .hero-card {
    bottom: -20px;
    right: -20px;
    padding: var(--space-6);
  }
  
  .card-icon {
    font-size: 2rem;
  }
  
  .card-content h4 {
    font-size: var(--font-size-lg);
  }
}

/* Extra large devices (1280px and up) - Large Desktops */
@media (min-width: 1280px) {
  .hero-content {
    gap: var(--space-20);
  }
}

/* 2XL devices (1536px and up) - TVs and very large screens */
@media (min-width: 1536px) {
  .hero-content {
    gap: var(--space-24);
  }
  
  .hero-text h1 {
    font-size: var(--font-size-5xl);
  }
  
  .hero-subtitle {
    font-size: var(--font-size-xl);
  }
}

/* Hero Section */
.hero {
  /* Make hero occupy the full viewport height minus the fixed header */
  padding: 24px 0 40px;
  min-height: calc(100vh - 72px);
  display: flex;
  align-items: center;
  background: #d5ddc8; /* Updated background color to #d5ddc8 */
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

  padding: clamp(48px, 8vw, 100px) 0;
  background: #065f46; /* Keep the green background */
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-header h2 {
  margin-bottom: 16px;
  color: white;
  font-size: 40px
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

.team {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 32px;
  margin-top: 40px;
}

/* Team Section */


.team-title {
  grid-column: span 3;
  text-align: center;
  margin-bottom: 32px;
  font-size: 2rem;
  color: #0f172a;
}

.team-card {
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.team-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

/* Alternative horizontal card: image on the left, info on the right */
.team-card--alt {
  display: flex;
  align-items: center;
  gap: 24px;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
  border-left: 6px solid var(--color-primary);
  text-align: left;
}

.team-card--alt .team-photo {
  width: 140px;
  height: 140px;
  object-fit: cover;
  object-position: center;
  border-radius: 12px;
  margin: 0;
  flex-shrink: 0;
}

.team-card--alt .team-info {
  padding-left: 4px;
}

.team-card--alt h3 {
  font-size: 1.5rem;
  margin-bottom: 8px;
  color: var(--color-heading);
}

.team-card--alt p {
  margin: 0 0 8px 0;
  color: var(--color-text-muted);
}

@media (max-width: 768px) {
  /* Compact horizontal card on small screens to match reference
     keep image at left (small square) and text at right, reduce padding/gap */
  .team-card--alt {
    flex-direction: row;
    align-items: center;
    text-align: left;
    padding: 10px 12px;
    gap: 12px;
    border-left-width: 0; /* remove thick left stripe */
    border-top: 4px solid var(--color-primary); /* subtle top accent to match visual */
    border-radius: 12px;
  }

  .team-card--alt .team-photo {
    width: 84px;
    height: 84px;
    border-radius: 10px;
    object-fit: cover;
    object-position: center 20%;
    margin: 0;
    flex-shrink: 0;
  }

  .team-card--alt .team-info {
    padding-left: 0;
    margin-top: 0;
  }

  .team-card--alt h3 {
    font-size: 1.125rem;
    margin-bottom: 4px;
  }

  .team-card--alt p {
    margin: 0;
    font-size: 0.95rem;
    color: var(--color-text-muted);
  }

  /* Reduce white-space around the grid */
  .team-grid {
    gap: 12px;
  }
}

/* Tighter cards for tablet and mobile: reduce image and padding so cards fit better */
@media (min-width: 769px) and (max-width: 1024px) {
  .team-card--alt {
    gap: 16px;
    padding: 16px;
  }

  .team-card--alt .team-photo {
    width: 120px;
    height: 120px;
  }

  .team-card--alt h3 {
    font-size: 1.25rem;
  }
}

@media (max-width: 768px) {
  /* Ensure other mobile overrides remain consistent with compact layout */
  .team-card--alt {
    padding: 10px 12px;
    border-left-width: 0;
    border-top-width: 4px;
  }

  .team-card--alt .team-photo {
    width: 84px;
    height: 84px;
  }

  .team-card--alt h3 {
    font-size: 1.125rem;
  }

  .team-card--alt p {
    font-size: 0.95rem;
  }
}

.team-photo {
  width: 100%;
  /* a touch taller so there's more vertical room when faces are framed low in source photos */
  height: 260px;
  object-fit: cover; /* crop to fill the box while preserving aspect ratio on larger screens */
  /* default: slightly favor the upper-middle of the photo so faces appear centered */
  object-position: center 20%;
  border-radius: 12px;
  margin-bottom: 16px;
  display: block;
}

.team-photo--thaissa { object-position: center 30%; }
.team-photo--wilka   { object-position: center 18%; }
.team-photo--gabriel { object-position: center 12%; }

/* On small screens, prefer showing the full image instead of cropping */
@media (max-width: 768px) {
  .team-photo {
    height: auto; /* allow image to scale naturally */
    /* On small screens prefer cover with top alignment so faces remain visible while preserving card layout */
    object-fit: cover;
    object-position: center 18%;
    max-height: 360px; /* limit extreme heights */
  }

  .team-card {
    padding: 16px; /* reduce padding for smaller viewports */
  }
}

@media (max-width: 420px) {
  .team-photo {
    max-height: 260px;
  }
}

.team-social {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 8px;
}

.team-social a {
  color: #065f46;
  font-size: 1.25rem;
  transition: color 0.2s ease;
}

.team-social a:hover {
  color: #10b981;
}

/* FAQ Section */
.faq {
  padding: 100px 0;
  background: white;
}

/* FAQ heading uses the site primary green to match brand */
.faq .section-header h2 {
  color: #334155;
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

/* Media Queries for Responsiveness */
@media (max-width: 768px) {
  .hero-content {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .hero-image {
    margin-top: 16px;
  }

  .services-grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }

  .about-content {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }


  .about-features {
    display: flex;
    flex-direction: row;
    gap: 18px;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    margin-bottom: 24px;
  }

  .about-features .feature {
    flex: 0 0 auto;
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 6px 8px;
  }

  .about-features .feature .feature-icon {
    width: 32px;
    height: 32px;
    font-size: 16px;
  }

  .about-image {
    margin-top: 16px;
  }

  .team {
    display: flex;
    flex-direction: column;
    gap: 24px;
  }

  .team-card {
    align-items: center;
    text-align: center;
    padding: 12px; /* compact card padding on mobile */
  }

  /* Make the alt cards much more compact on small screens: smaller image, smaller gap */
  .team-card--alt {
    padding: 10px;
    border-left-width: 0; /* remove accent stripe on narrow viewports */
  }

  .team-card--alt .team-photo {
    width: 96px;
    height: 96px;
    border-radius: 8px;
    margin: 0 auto 12px;
  }

  .team-grid {
    gap: var(--space-4);
  }

  .faq-container {
    padding: 0 16px;
  }

  h1 {
    font-size: 2.5rem;
  }

  h2 {
    font-size: 2rem;
  }

  .btn-primary, .btn-secondary {
    font-size: 14px;
    padding: 10px 20px;
  }
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

  /* nav-cta removed */

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
