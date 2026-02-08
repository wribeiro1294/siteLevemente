<script setup>
import { reactive, ref, watch, onBeforeUnmount } from 'vue'

const props = defineProps({
  show: Boolean,

  appsScriptUrl: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['update:show', 'submitted'])

const submitting = ref(false)
const submitted = ref(false)
const serverMessage = ref('')

const form = reactive({
  name: '',
  email: '',
  phone: '',
  message: ''
})


const firstInput = ref(null)
const emailInput = ref(null)
const emailInvalid = ref(false)

const isValidEmail = (email) => {
  if (!email) return false
  // simple RFC-like validation: no whitespace, contains @ and a dot after @
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return re.test(String(email).toLowerCase())
}

const close = () => {
  emit('update:show', false)
}

const submit = async (e) => {
  e.preventDefault()

  if (!form.name || !form.email) {
    alert('Por favor informe nome e e-mail')
    return
  }


  if (!props.appsScriptUrl || !props.appsScriptUrl.endsWith('/exec')) {
    alert('URL do Apps Script inválida')
    return
  }

  submitting.value = true
  serverMessage.value = ''

  const payload = {
    nome: form.name,
    email: form.email,
    telefone: form.phone,
    mensagem: form.message
  }


  try {

    const res = await fetch(props.appsScriptUrl, {
      method: 'POST',
      mode: 'cors',
      headers: {
        'Content-Type': 'text/plain;charset=UTF-8'
      },
      body: JSON.stringify(payload)
    })

    if (!res.ok) {
      const text = await res.text().catch(() => '')
      throw new Error(`HTTP ${res.status} - ${text}`)
    }

    let data = null
    let textBody = null
    try {
      data = await res.json()
    } catch (err) {
      textBody = await res.text().catch(() => '')
      console.warn('Response not JSON, body:', textBody)
    }

    const successFromBody = data?.success === true
    if (!successFromBody && data && data.success === false) {
      throw new Error(data?.message || 'Falha ao salvar na planilha')
    }

    if (!successFromBody && !data) {
      serverMessage.value = textBody ? String(textBody) : 'Enviado com sucesso.'
    } else if (successFromBody) {
      serverMessage.value = data.message || 'Enviado com sucesso 🎉'
    }

  submitted.value = true
  serverMessage.value = 'Enviado com sucesso 🎉'


  emit('submitted', { ...form })

  form.name = ''
  form.email = ''
  form.phone = ''
  form.message = ''

  } catch (err) {
    serverMessage.value = 'Erro ao enviar, tente novamente mais tarde'
    submitted.value = false
  } finally {
    submitting.value = false
  }
}

const onKey = (e) => {
  if (e.key === 'Escape') close()
}


const formatPhoneValue = (value) => {
  const digits = String(value || '').replace(/\D/g, '').slice(0, 11)
  if (!digits) return ''
  if (digits.length <= 2) return `(${digits}`
  if (digits.length <= 6) return `(${digits.slice(0,2)}) ${digits.slice(2)}`
  if (digits.length <= 10) return `(${digits.slice(0,2)}) ${digits.slice(2,6)}-${digits.slice(6)}`
  // 11 dígitos (DDD + 9xxxx-xxxx)
  return `(${digits.slice(0,2)}) ${digits.slice(2,7)}-${digits.slice(7)}`
}

const onPhoneInput = (e) => {
  const raw = e.target.value
  const formatted = formatPhoneValue(raw)
  form.phone = formatted
}

watch(() => props.show, (val) => {
  if (val) {
    setTimeout(() => firstInput.value?.focus(), 80)
    window.addEventListener('keydown', onKey)
  } else {
    window.removeEventListener('keydown', onKey)
    submitted.value = false
    serverMessage.value = ''
  }
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', onKey)
})
</script>

<template>
  <div v-if="props.show" class="modal-overlay" @click.self="close">
    <div class="modal" role="dialog" aria-modal="true" aria-label="Formulário de inscrição">
      <button class="modal-close" @click="close" aria-label="Fechar">×</button>
  <h3><span class="logo-left">LEVE</span>
            <span class="logo-right">MENTE</span></h3>
      <form v-if="!submitted" class="signup-form" @submit="submit">
        <label>
          Nome
          <input ref="firstInput" v-model="form.name" type="text" placeholder="Seu nome" required />
        </label>
        <label>
          Email
          <input
            v-model="form.email"
            ref="emailInput"
            type="email"
            placeholder="seu@exemplo.com"
            required
            :class="{ 'input--invalid': emailInvalid }"
            @input="emailInvalid = false; serverMessage = ''"
          />
        </label>
        <label>
          Telefone
          <input v-model="form.phone" @input="onPhoneInput" inputmode="tel" type="text" placeholder="(11) 9xxxx-xxxx" />
        </label>
        <label>
          Mensagem (opcional)
          <textarea v-model="form.message" rows="4" placeholder="Alguma informação adicional"></textarea>
        </label>

        <div v-if="serverMessage" class="server-message" role="status">{{ serverMessage }}</div>

        <div class="modal-actions">
          <button type="submit" class="btn-primary" :disabled="submitting">{{ submitting ? 'Enviando…' : 'Enviar inscrição' }}</button>
          <button type="button" class="btn-secondary" @click="close">Cancelar</button>
        </div>
      </form>

      <div v-else class="submission-result">
        <div class="signup-success" role="status">{{ serverMessage || 'Enviado com sucesso 🎉' }}</div>
        <div class="modal-actions" style="margin-top:16px">
          <button type="button" class="btn-primary" @click="close">Fechar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(2, 6, 23, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: var(--z-modal);
  padding: var(--space-4);
}

.modal {
  background: white;
  width: 100%;
  max-width: min(640px, calc(100vw - var(--space-8)));
  border-radius: 12px;
  padding: var(--space-6);
  box-shadow: 0 30px 60px rgba(2, 6, 23, 0.3);
  position: relative;
  max-height: calc(100vh - var(--space-8));
  overflow-y: auto;
}

.modal-close {
  position: absolute;
  top: var(--space-3);
  right: var(--space-3);
  background: transparent;
  border: none;
  font-size: 22px;
  cursor: pointer;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  transition: all var(--transition-fast);
  color: var(--color-text-muted);
}

.modal-close:hover {
  background: var(--color-gray-100);
  color: var(--color-text);
}

.modal h3 {
  margin-bottom: var(--space-2);
  color: var(--color-heading);
  font-size: var(--font-size-2xl);
  padding-right: var(--space-12);
}

.modal > p {
  margin-bottom: var(--space-6);
  color: var(--color-text-muted);
  line-height: 1.6;
}

.signup-form {
  display: grid;
  gap: var(--space-4);
}

.logo-left {
  color: #3f4337;
}

.logo-right {
  color: #afc09e;
  margin-left: 6px;
}

.signup-form label {
  display: flex;
  flex-direction: column;
  font-size: var(--font-size-sm);
  color: var(--color-text);
  font-weight: 500;
}

.signup-form input,
.signup-form textarea {
  margin-top: var(--space-2);
  padding: var(--space-3) var(--space-4);
  border-radius: 8px;
  border: 1px solid var(--color-border);
  background: var(--color-background-soft);
  font-size: var(--font-size-base);
  transition: all var(--transition-fast);
  font-family: inherit;
}

.signup-form input:focus,
.signup-form textarea:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(22, 163, 74, 0.1);
  background: white;
}

.signup-form textarea {
  resize: vertical;
  min-height: 100px;
}

.modal-actions {
  display: flex;
  gap: var(--space-3);
  margin-top: var(--space-6);
  flex-direction: column;
  align-items: stretch; 
}

.signup-success {
  margin-top: var(--space-4);
  color: var(--color-primary-dark);
  font-weight: 600;
  text-align: center;
  padding: var(--space-4);
  background: var(--color-primary-50);
  border-radius: 8px;
}

.server-message {
  margin-top: var(--space-4);
  font-size: var(--font-size-sm);
  color: var(--color-primary-dark);
  text-align: center;
  padding: var(--space-3);
  background: var(--color-primary-50);
  border-radius: 8px;
}

.submission-result .signup-success {
  text-align: center;
  padding: var(--space-4);
  border-radius: 8px;
  background: linear-gradient(180deg, rgba(16,185,129,0.06), rgba(6,95,70,0.04));
  color: var(--color-primary-dark);
  font-weight: 700;
  font-size: 1rem;
}

.brand-green {
  color: var(--color-primary);
  font-weight: 600;
}


/* Button styles: modal-specific overrides while keeping global button system */
.modal-actions .btn-primary,
.modal-actions .btn-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: var(--space-3) var(--space-5);
  border-radius: 10px;
  font-weight: 600;
  transition: all var(--transition-fast);
}

.modal-actions .btn-primary {
  width: 100%; /* mobile: full width */
  color: white;
}

.modal-actions .btn-primary[disabled] {
  opacity: 0.6;
  cursor: not-allowed;
  box-shadow: none;
}

.modal-actions .btn-secondary {
  width: 100%; /* mobile: full width */
  background: transparent;
  border: 1px solid var(--color-border);
  color: var(--color-text);
}

@media (min-width: 480px) {
  .modal-actions {
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
  }

  .modal-actions .btn-primary {
    width: auto;
    min-width: 180px;
  }

  .modal-actions .btn-secondary {
    width: auto;
  }
}

/* Responsive Design */
@media (min-width: 480px) {
  .modal {
    padding: var(--space-8);
  }
  
  .modal-actions {
    flex-direction: row;
  }
  
  .modal h3 {
    font-size: var(--font-size-3xl);
  }
}

@media (min-width: 768px) {
  .modal-overlay {
    padding: var(--space-8);
  }
  
  .modal {
    max-height: calc(100vh - var(--space-16));
  }
}

/* Improve touch targets on mobile */
@media (max-width: 479px) {
  .modal-close {
    width: 48px;
    height: 48px;
    font-size: 24px;
  }
  
  .signup-form input,
  .signup-form textarea {
    padding: var(--space-4);
    font-size: 16px; /* Prevents zoom on iOS */
  }
  
  .btn-primary,
  .btn-secondary {
    min-height: 48px;
    font-size: 16px;
  }
}

/* High contrast mode */
@media (prefers-contrast: high) {
  .modal {
    border: 2px solid var(--color-text);
  }
  
  .signup-form input,
  .signup-form textarea {
    border: 2px solid var(--color-text);
  }
}</style>
